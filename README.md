# PerformanceNavigationTiming firstMeaningfulPaint

First Meaningful Paint is the time when a page's primary content has appeared on the screen.

Which content is primary is subjective, and knowing when content has appeared on the screen precisely is impossible on user's devices.
We propose an approximation of First Meaningful Paint based on signals from page layout.

## Computation ##
We approximate First Meaningful Paint as the end time of the paint following the layout with the highest "Layout Significance".

### Layout Significance ###

For each layout, we compute the `layout significance`.
```
if a textual web font is loading:
  layout_significance = 0
else:
  previous_layout = last layout without a loading textual webfont
  new_box_count = number of new CSS Boxes* since previous_layout
  layout_significance = new_box_count / max(1, page_height / screen_height)
```

[*CSS Boxes](https://www.w3.org/TR/css3-box/)

To determine if a web font is textual, we use a heuristic. If a web font has more than 200 characters, we consider it textual.

Including page height / screen height in the calculation enables us to decrease the weight of layouts which are likely only adding content below the fold.

## Web API ##
First Meaningful Paint will be added to the [PerformanceNavigationTiming](https://www.w3.org/TR/navigation-timing-2/#sec-PerformanceNavigationTiming) interface in the [Navigation Timing API](https://www.w3.org/TR/navigation-timing-2/).

```javascript
window.onLoad = () => { 
  var navigationTiming = performance.getEntriesByType("navigation")[0];
  var first_meaningful_paint = navigationTiming.firstMeaningfulPaint;
  console.log("Time to First Meaningful Paint: " + first_meaningful_paint);
}
```

## TODO ##
* Clarify what we mean by the "end of paint".
