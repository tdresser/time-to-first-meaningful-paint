# time-to-first-meaningful-paint

First Meaningful Paint is the time when page's primary content appeared on the screen.

Which content is primary is subjective, and knowing when content has appeared on the screen precisely is impossible on user's devices.
We propose an approximation of First Meaningful Paint based on signals from page layout.

## Computation ##
We approximate First Meaningful Paint as the start time of the paint following the layout with the highest "Layout Significance".

### Layout Significance ###

For each layout, we compute the `layout significance`.
```
if a textual web font is loading:
  layout significance = 0
else:
  layout significance = number of new DOM nodes since last layout / max(1, page height / screen height)
```

To determine if a web font is textual, we use a heuristic. If a web font has more than 200 characters, we consider it textual.

## Web API ##
First Meaningful Paint will be added to the [PerformanceNavigationTiming](https://www.w3.org/TR/navigation-timing-2/#sec-PerformanceNavigationTiming) interface in the [Navigation Timing API](https://www.w3.org/TR/navigation-timing-2/).

```javascript
window.onLoad = () => { 
  var navigationTiming = performance.getEntriesByType("navigation")[0];
  var first_meaningful_paint = navigationTiming.firstMeaningfulPaint;
  console.log("Time to First Meaningful Paint: " + first_meaningful_paint);
}
```

#TODO#
* Can we use DOM nodes instead of layout nodes?
* Should we measure until the start of paint, or the end?
