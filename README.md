d3.svg.multibrush
===================

Supports the same interaction modes as d3.svg.brush but with multiple extents. Extents can overlap. Extents on the x-axis are fairly well tested because that is our use-case. Extents on the y-axis and combined x-/y-extents should work but are not well tested currently.


Differences from the [d3.svg.brush API](https://github.com/mbostock/d3/wiki/SVG-Controls#wiki-brush):


multibrush.**extent**([values])

Since multiple extents are supported, [values] is an array of arrays. The arrays are in the same format as used by d3.svg.brush.extent(). The return value will also be an array of arrays. If no extents are defined (or all extents are empty), it will be the empty array.


multibrush.**empty**([index])

multibrush.empty() will return true if no extents are defined or if all extents are empty. If an index is provided, will return true if the extent at that index is empty. Note that this is not necessarily the same index as in the array returned by multibrush.extent() because empty extents are excluded from the returned array. The index corresponds to the order in which extents were created on the brush.


multibrush.**resizeAdaption**([function])

A function that will be called on the d3.selection of a resizer when a new extent is created. Since we dynamically create and destroy extents and resizers, you need to define any formatting or custom classes here. Example:

```js
multibrush.resizeAdaption(
  function (selection) {
    selection.append("path")
      .attr("transform", "translate(0, " + -(12.5) + ")");
							
    selection.select("rect").attr("height", 50);
  )
);
```


multibrush.**extentAdaption**([function])

A function that will be called on the d3.selection of an extent when a new extent is created. Since we dynamically create and destroy extents and resizers, you need to define any formatting or custom classes here. Example:

```js
multibrush.extentAdaption(
  function (selection) {
    selection.attr("height", 50)
		  .attr("fill", 'white')
	  	.attr("fill-opacity", ".500");
  })
);
```
