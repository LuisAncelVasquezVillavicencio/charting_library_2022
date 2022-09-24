## Time Scale API

### coordinateToTime(x)

Returns time associated with given `x` coordinate.

### barSpacingChanged()

Users will be notified every time `barSpacing` value is changed. This typically occurs when zooming in/out on the chart.

### rightOffsetChanged()

Users will be notified every time `rightOffset` value is changed. This typically occurs when scrolling left/right on the chart.

### setRightOffset(offset)

To set a new right offset.

### setBarSpacing(newBarSpacing)

To set a new bar spacing.

### rightOffset()

Returns the current right offset.

### barSpacing()

Returns the current bar spacing.

### width()

Returns the current width of the chart in pixels.

### defaultRightOffset()

Returns a [WatchedValue](WatchedValue) object that can be used to read/set/watch the default right offset (margin) value.
