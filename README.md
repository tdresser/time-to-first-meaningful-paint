# time-to-first-meaningful-paint

First Meaningful Paint is the time when page's primary content appeared on the screen.

Which content is primary is subjective, and knowing when content has appeared on the screen precisely is impossible on user's devices.
We propose an approximation of First Meaningful Paint based on signals from page layout.

## Computation ##
TODO - figure out if we want the start time or the end time of the paint.
We approximate First Meaningful Paint as the start time of the paint following the layout with the highest "Layout Significance".

### Layout Significance ###

TODO - we currently use layout objects, but should probably use DOM nodes.
  
`layout significance = number of new DOM nodes since last paint / max(1, page height / screen height)`

TODO - incorporate web fonts here.

## Web API ##
First Meaningful Paint will be added to the [PerformanceNavigationTiming](https://www.w3.org/TR/navigation-timing-2/#sec-PerformanceNavigationTiming) interface in the [Navigation Timing API](https://www.w3.org/TR/navigation-timing-2/).

```javascript
window.onLoad = () => { 
  var navigationTiming = performance.getEntriesByType("navigation")[0];
  var first_meaningful_paint = navigationTiming.firstMeaningfulPaint;
  console.log("Time to First Meaningful Paint: " + first_meaningful_paint);
}
```
