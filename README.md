# time-to-first-meaningful-paint

First Meaningful Paint is the time when page's primary content appeared on the screen.

Which content is primary is subjective, and knowing when content has appeared on the screen precisely is impossible on user's devices.
We propose an approximation of First Meaningful Paint based on signals from page layout.

## Computation ##
We approximate First Meaningful Paint as the start time of the paint following the layout with the highest "Layout Significance".

### Layout Significance ###

TODO - replace layout object with a UA independent term
  
`layout significance = number of new layout objects since last paint / max(1, page height / screen height)`

TODO - incorporate web fonts here.

## Web API ##
First Meaningful Paint will be exposed through the Navigation Timing API.

```javascript
window.onLoad = () => { 
  var first_meaningful_paint = performance.timing.firstMeaningfulPaint;
  var navigation_start = performance.timing.navigationStart;
  console.log("Time to First Meaningful Paint: " + (first_meaningful_paint - navigation_start));
}
```
