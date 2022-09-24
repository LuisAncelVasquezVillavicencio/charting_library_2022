Here is a list of methods supported by the chart.

**Before version 1.4.** You can call these methods using widget object returned to you by widget's constructor.

**Starting from version 1.5.** You can call these methods using chart object returned to you by widget's methods [chart(index)](Widget-Methods#chart-chartindex) or [activeChart()](Widget-Methods#chart-activechart).

## Methods

* [Subscribing To Chart Events](#subscribing-to-chart-events)
  * [onDataLoaded()](#ondataloaded)
  * [onSymbolChanged()](#onsymbolchanged)
  * [onIntervalChanged()](#onintervalchanged)
  * [onChartTypeChanged()](#oncharttypechanged)
  * [dataReady(callback)](#datareadycallback)
  * [crossHairMoved()](#crosshairmoved)
  * [onVisibleRangeChanged()](#onvisiblerangechanged)
* [Chart Actions](#chart-actions)
  * [setVisibleRange(range, options)](#setvisiblerangerange-options)
  * [setSymbol(symbol, callback)](#setsymbolsymbol-callback)
  * [setResolution(resolution, callback)](#setresolutionresolution-callback)
  * [resetData()](#resetdata)
  * [executeActionById(action)](#executeactionbyidactionid)
  * [getCheckableActionState(action)](#getcheckableactionstateactionid)
  * [refreshMarks()](#refreshmarks)
  * [clearMarks()](#clearmarks)
  * [setChartType(type)](#setcharttypetype)
  * [setTimezone(timezone)](#settimezonetimezone)
  * [getTimezone()](#gettimezone)
  * [getTimezoneApi()](#gettimezoneapi)
* [Studies And Shapes](#studies-and-shapes)
  * [getAllShapes()](#getallshapes)
  * [getAllStudies()](#getallstudies)
  * [setEntityVisibility(id, isVisible)](#setentityvisibilityid-isvisible) [obsolete]
  * [createStudy(name, forceOverlay, lock, inputs, overrides, options)](#createstudyname-forceoverlay-lock-inputs-overrides-options)
  * [getStudyById(entityId)](#getstudybyidentityid)
  * [getSeries()](#getseries)
  * [showPropertiesDialog(entityId)](#showpropertiesdialogentityId)
  * [createShape(point, options)](#createshapepoint-options)
  * [createMultipointShape(points, options)](#createmultipointshapepoints-options)
  * [getShapeById(entityId)](#getshapebyidentityid)
  * [removeEntity(entityId)](#removeentityentityid-options)
  * [removeAllShapes()](#removeallshapes)
  * [removeAllStudies()](#removeallstudies)
  * [getPanes()](#getpanes)
* [Z-order operations](#z-order-operations)
  * [availableZOrderOperations(entities)](#availablezorderoperationsentities)
  * [sendToBack(entities)](#sendtobackentities)
  * [bringToFront(entities)](#bringtofrontentities)
  * [bringForward(entities)](#bringforwardentities)
  * [sendBackward(entities)](#sendbackwardentities)
* [Study Templates](#study-templates)
  * [createStudyTemplate(options)](#createstudytemplateoptions)
  * [applyStudyTemplate(template)](#applystudytemplatetemplate)
* [Trading Primitives](#trading-primitives)
  * [createOrderLine()](#createorderlineoptions)
  * [createPositionLine()](#createpositionlineoptions)
  * [createExecutionShape()](#createexecutionshapeoptions)
* [Getters](#getters)
  * [symbol()](#symbol)
  * [symbolExt()](#symbolExt)
  * [resolution()](#resolution)
  * [getVisibleRange()](#getvisiblerange)
  * [getVisiblePriceRange()](#getvisiblepricerange)
  * [scrollPosition()](#scrollposition)
  * [defaultScrollPosition()](#defaultscrollposition)
  * [priceFormatter()](#priceformatter)
  * [chartType()](#charttype)
  * [getPriceToBarRatio()](#getpricetobarratio)
  * [isPriceToBarRatioLocked()](#ispricetobarratiolocked)
  * [getAllPanesHeight()](#getAllPanesHeight)
  * [setAllPanesHeight(heights)](#setAllPanesHeightheights)
  * [maximizeChart()](#maximizeChart)
  * [restoreChart()](#restoreChart)
* [Other](#other)
  * [exportData(options)](#exportdataoptions)
  * [selection()](#selection)
  * [setZoomEnabled(enabled)](#setzoomenabledenabled)
  * [setScrollEnabled(enabled)](#setscrollenabledenabled)
  * [getTimeScale()](#gettimescale)
  * [isSelectBarRequested()](#isselectbarrequested)
  * [requestSelectBar()](#requestselectbar)
  * [cancelSelectBar()](#cancelselectbar)
  * [setPriceToBarRatio(value, options)](#setpricetobarratiovalue-options)
  * [setPriceToBarRatioLocked(value, options)](#setpricetobarratiolockedvalue-options)

## Subscribing To Chart Events

### onDataLoaded()

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when new history bars are loaded. You can also use the same object to unsubscribe from the event.

Example:

```javascript
widget.activeChart().onDataLoaded().subscribe(
    null,
    () => console.log('New history bars are loaded'),
    true
);
```

### onSymbolChanged()

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when the symbol is changed. You can also use the same object to unsubscribe from the event.

Example:

```javascript
widget.activeChart().onSymbolChanged().subscribe(null, () => console.log('The symbol is changed'));
```

### onIntervalChanged()

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when the interval is changed. You can also use the same object to unsubscribe from the event.
When the event is fired it will provide the following arguments:

1. `interval`: new interval
1. `timeframeObj`: object with the only field `timeframe`.

    It contains a timeframe or dates range. It presents if the user clicks on the timeframe panel or changes the dates range.

    Otherwise `timeframe` is `undefined` and you can change it to display a certain range of bars. Valid timeframe is a `TimeFrameValue` object.

    `TimeFrameValue` can be:
    1. a timeframe object, `{type, value}`:
        * `type`: `period-back`.
        * `value`: valid timeframe is a number with letter D for days and M for months.
    2. a range object, `{type, from, to}`
        * `type`: `time-range`.
        * `from`, `to`: UNIX timestamps, UTC.

Example:

```javascript
widget.activeChart().onIntervalChanged().subscribe(null, (interval, timeframeObj) => timeframeObj.timeframe = { value: "12M", type: "period-back" });

widget.activeChart().onIntervalChanged().subscribe(null,
    (interval, timeframeObj) => timeframeObj.timeframe = { from: new Date('2015-01-01').getTime() / 1000, to: new Date('2017-01-01').getTime() / 1000, type: "time-range" }
);
```

### onChartTypeChanged()

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when the chart type is changed. You can also use the same object to unsubscribe from the event.
When the event is fired it will provide the `chartType` argument, possible values are described [here](#setcharttypetype).

Example:

```javascript
widget.activeChart().onChartTypeChanged().subscribe(null, (chartType) => console.log('The type of chart is changed'));
```

### dataReady()

The function returns `true` if bars are already loaded and `false` otherwise.

Example:

```javascript
if (widget.activeChart().dataReady()) {
    /* do something */
}
```

### dataReady(callback)

1. `callback`: function(onReadyCallback)

The Charting Library will immediately call the callback function if bars are already loaded or when the bars are received.

Example:

```javascript
widget.activeChart().dataReady(() => {
    /* draw shapes */
});
```

### crossHairMoved()

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when visible time range is changed. You can also use the same object to unsubscribe from the event.

When the event is fired it will provide the following arguments:

1. `params`: object `{time price}`
    * `time`: unix timestamps, UTC.
    * `price`: number.

Example:

```javascript
widget.activeChart().crossHairMoved().subscribe(
    null,
    ({ time, price }) => console.log(time, price)
);
```

### onVisibleRangeChanged()

*Since version 1.13.*

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when visible time range is changed. You can also use the same object to unsubscribe from the event.

When the event is fired it will provide the following arguments:

1. `range`: object, `{from to}`
    * `from`, `to`: unix timestamps, UTC.

Example:

```javascript
widget.activeChart().onVisibleRangeChanged().subscribe(
    null,
    ({ from, to }) => console.log(from, to)
);
```

## Chart Actions

### setVisibleRange(range, options)

1. `range`: object, `{ from, to }`
    * `from`, `to`: unix timestamps, UTC
1. `options`: `{ applyDefaultRightMargin, percentRightMargin }`
    * `applyDefaultRightMargin`: indicates whether the library should apply the default right margin to the right border if it points on the last bar.
    * `percentRightMargin`: indicates whether the library should apply the percent right margin to the right border if it points on the last bar.

Forces the chart to adjust its parameters (scroll, scale) to make the selected time period fit the widget.

Returns a Promise object, which will be resolved after visible range is applied.

This method was introduced in version `1.2`.

```javascript
widget.activeChart().setVisibleRange(
    { from: 1420156800, to: 1451433600 },
    { percentRightMargin: 20 }
).then(() => console.log('New visible range is applied'));
```

### setSymbol(symbol, callback)

1. `symbol`: string
1. `callback`: function(), optional

Makes the chart change its symbol. Callback function is called once the data for the new symbol is loaded.

```javascript
widget.activeChart().setSymbol('IBM');
```

### setResolution(resolution, callback)

1. `resolution`: string. Format is described in another [article](Resolution).
1. `callback`: function(), optional

Makes the chart change its resolution. Callback function is called once new data is loaded.

```javascript
widget.activeChart().setResolution('2M');
```

### resetData()

Makes the chart re-request data from the data feed. The function is often called when chart's data has changed.

Before calling this function you should call [`onResetCacheNeededCallback` from `subscribeBars`](JS-Api#subscribebarssymbolinfo-resolution-onrealtimecallback-subscriberuid-onresetcacheneededcallback).

```javascript
widget.activeChart().resetData();
```

### executeActionById(actionId)

*Starting from version 1.3.*

1. `actionId`: string

Executes an action according to its id.

**Shows a dialog:**

* `chartProperties`
* `compareOrAdd`
* `scalesProperties`
* `paneObjectTree`
* `insertIndicator`
* `symbolSearch`
* `changeInterval`
* `gotoDate`

**Other actions:**

* `timeScaleReset`
* `chartReset`
* `seriesHide`
* `studyHide`
* `lineToggleLock`
* `lineHide`
* `scaleSeriesOnly`
* `drawingToolbarAction`
* `stayInDrawingModeAction`
* `hideAllMarks`
* `showCountdown` - for intraday resolutions only
* `showSeriesLastValue`
* `showSymbolLabelsAction`
* `showStudyLastValue`
* `showStudyPlotNamesAction`
* `undo`
* `redo`
* `paneRemoveAllStudiesDrawingTools`

Examples:

```javascript
// < ... >
widget.activeChart().executeActionById("undo");
// < ... >
widget.activeChart().executeActionById("drawingToolbarAction"); // hides or shows the drawing toolbar
// < ... >
```

### getCheckableActionState(actionId)

*Starting from version 1.7.*

1. `actionId`: string

Get a checkable action state (e.g. `stayInDrawingModeAction`, `showSymbolLabelsAction`) according to its ID (see the IDs of actions above)

```javascript
if (widget.activeChart().getCheckableActionState("drawingToolbarAction")) {
    /* do something */
};
```

### refreshMarks()

When you call this method the Library re-requests Bar marks and Timescale marks.

```javascript
widget.activeChart().refreshMarks();
```

### clearMarks()

When you call this method the Library removes all visible marks.

```javascript
widget.activeChart().clearMarks();
```

### setChartType(type)

1. `type`: number

Sets the main series style.

| Style | JavaScript type | Typescript Enum | Charting Library | Trading Terminal |
| --- | --- | --- | :---: | :---: |
| Bar | 0 | ChartStyle.Bar | ✓ | ✓ |
| Candle | 1 | ChartStyle.Candle | ✓ | ✓ |
| Line | 2 | ChartStyle.Line | ✓ | ✓ |
| Area | 3 | ChartStyle.Area | ✓ | ✓ |
| Renko | 4 | ChartStyle.Renko | | ✓ |
| Kagi | 5 | ChartStyle.Kagi | | ✓ |
| PnF | 6 | ChartStyle.PnF | | ✓ |
| Line Break | 7 | ChartStyle.LineBreak | | ✓ |
| Heikin-Ashi | 8 | ChartStyle.HeikinAshi | ✓ | ✓ |
| Hollow Candle | 9 | ChartStyle.HollowCandle | ✓ | ✓ |
| Baseline | 10 | ChartStyle.Baseline | ✓ | ✓ |
| Hi-Lo | 12 | ChartStyle.HiLo | ✓ | ✓ |
| Column | 13 | ChartStyle.Column | ✓ | ✓ |

```javascript
widget.activeChart().setChartType(12);
```

### setTimezone(timezone)

1. `timezone`: string

See [timezone](Widget-Constructor#timezone) for more information.

Example:

```javascript
widget.activeChart().setTimezone('Asia/Singapore');
```

Makes the chart change its timezone.

**Deprecated**: Use [setTimezone](Timezone-Api#settimezonetimezoneid-options) instead. This is going to be removed in future releases.

### getTimezone()

*Since version 1.15.*

Returns the current [timezone](Widget-Constructor#timezone) of the chart.

```javascript
console.log(widget.activeChart().getTimezone());
```

**Deprecated**: Use [getTimezone](Timezone-Api#gettimezone) instead. This is going to be removed in future releases.

### getTimezoneApi()

*Since version 22.*

Returns a [TimezoneApi](Timezone-Api) that allows you to interact with the chart's timezone.

### canZoomOut()

*Since version 1.14.*

When you call this method, the Library checks if there are any zoom events to undone.

```javascript
console.log(widget.activeChart().canZoomOut());
```

### zoomOut()

*Since version 1.14.*

When you call this method, it simulates a click on the "Zoom Out" button. It works only if the chart is zoomed. Use `canZoomOut` to check if you can call this method.

```javascript
if(widget.activeChart().canZoomOut()) {
    widget.activeChart().zoomOut();
};
```

## Studies And Shapes

### getAllShapes()

Returns an array of all created shape objects. Each object has the following fields:

* `id`: id of a shape
* `name`: name of a shape

```javascript
widget.activeChart().getAllShapes().forEach(({ name }) => console.log(name));
```

### getAllStudies()

Returns an array of all created shape objects. Each object has the following fields:

* `id`: id of a study
* `name`: name of a study

```javascript
widget.activeChart().getAllStudies().forEach(({ name }) => console.log(name));
```

### setEntityVisibility(id, isVisible)

Sets visibility of an entity with a passed ID.

```javascript
widget.activeChart().setEntityVisibility(id, false); // Hide the entity with id
```

**Deprecated**: Use a shape/study API instead (`getShapeById`/`getStudyById`). This is going to be removed in future releases.

### createStudy(name, forceOverlay, lock, inputs, overrides, options)

1. `name`: string, name of an indicator as shown in the `Indicators` widget
1. `forceOverlay`: forces the Charting Library to place the created study on the main pane
1. `lock`: boolean, shows whether a user will be able to remove/change/hide the study or not
1. `inputs`: (starting from version `1.2` **Deprecated**) an array of study inputs. This array is expected to contain input values in the same order as in the study properties dialog.
**From version v22** it's an object containing named properties from the study properties dialog.
1. `overrides`: (starting from version `1.2`) an object [containing properties](Studies-Overrides) you'd like to set for your new study. Note that you should not specify the study name. Start a property path with a plot name.
1. `options`: object with the the following keys:
    * `checkLimit` - if it is `true` then the study limit dialog will be shown if the limit is exceeded.
    * `priceScale` - preferred price scale for the study. Possible values are:
        * `new-left` - attach the study to a new left price scale
        * `new-right` - attach the study to a new right price scale
        * `no-scale` - do not attach the study to any price scale. The study will be added in 'No Scale' mode
        * `as-series` - attach the study to the price scale where the main series is attached (it is only applicable the study is added to the pane with the main series)
    * `disableUndo` - prevents adding of the action to the undo stack

See [here](Panes-And-Scales-Behavior) more information about panes and scales behavior in relation to studies.

Returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) to `entityId` of the created study.

**Starting from v 1.12 the function returns the result immediately. Callback is kept to maintain compatibility.**

Creates a study on the main symbol. Here are the examples:

**Deprecated**:

* `widget.activeChart().createStudy('MACD', false, false, [14, 30, "close", 9])`
* `widget.activeChart().createStudy('Moving Average Exponential', false, false, [26])`
* `widget.activeChart().createStudy('Stochastic', false, false, [26], {"%d.color" : "#FF0000"})`
* `widget.activeChart().createStudy('Price Channel', true, false, [26], null, {checkLimit: false, priceScale: 'new-left'})`

**From version 22**:

* `widget.activeChart().createStudy('MACD', false, false, { in_0: 14, in_1: 30, in_3: 'close', in_2: 9 })`
* `widget.activeChart().createStudy('Moving Average Exponential', false, false, { length: 26 })`
* `widget.activeChart().createStudy('Stochastic', false, false, { in_0: 26 }, {"%d.color" : "#FF0000"})`
* `widget.activeChart().createStudy('Price Channel', true, false, { in_0: 26 }, null, {checkLimit: false, priceScale: 'new-left'})`

**Remark**: The `Compare` study has 2 inputs: `[dataSource, symbol]`. Supported `dataSource` values are: `["close", "high", "low", "open"]`.

**Remark 2**: You use `Overlay` study when you choose to `Add` series on the chart. This study has a single input -- `symbol`. Here is an example of adding a symbol:

```javascript
widget.activeChart().createStudy('Overlay', false, false, ['AAPL']);
```

**Remark 3**: You also use the `Compare` study when you choose to compare different financial instruments. This study has two inputs -- `source` and `symbol`. Here is an example:

```javascript
widget.activeChart().createStudy('Compare', false, false, ["open", 'AAPL']);
```

### getStudyById(entityId)

1. `entityId`: object. Value that is returned when a study is created via API.

Returns an instance of the [StudyApi](Study-Api) that allows you to interact with the study.

```javascript
widget.activeChart().getStudyById(id).setVisible(false);
```

### getSeries()

Returns an instance of the [SeriesApi](Series-Api) that allows you to interact with the main series.

```javascript
widget.activeChart().getSeries().setVisible(false);
```

### showPropertiesDialog(entityId)

1. `entityId`: object. Value that is returned when a study or shape is created via API.

Shows the properties dialog for specified study or shape for user interaction.

```javascript
const chart = widget.activeChart();
chart.showPropertiesDialog(chart.getAllShapes()[0].id);`
```

### createShape(point, options)

This is a shorthand for [createMultipointShape](#createmultipointshapepoints-options) method, which can be used for [shapes](Shapes-and-Overrides) based on one point.

1. `point`: object `{time, [price], [channel]}`
    * `time`: unix time. It's the only mandatory key in this function argument.
    * `price`: If you specify `price`, then the shape will be placed at the same price level.
        If not, then the shape will be placed close to the bar according the `channel` value.
    * `channel`: If the price is not set then `channel` value defines where the shape is placed relative to the bar. Possible values are `open`, `high`, `low`, `close`.
        If no channel is specified then 'open' is a default value.
1. `options`: object `{shape, [text], [lock], [overrides]}`, it is the same as in [createMultipointShape](#createmultipointshapepoints-options) method.
    * `shape` may be one of the following identifiers that require only one point:
        `arrow_up` | `arrow_down` | `flag` | `vertical_line` | `horizontal_line` | `long_position` | `short_position` | `icon`

        `flag` is the default value.
    * `text` is an optional argument. It's the text that will be included in the shape if it's supported. Additional field `showLabel` in overrides may be necessary.
    * `lock` shows whether a user will be able to remove/change/hide the shape or not.
    * `disableSelection` prevents selecting of the shape
    * `disableSave` prevents saving the shape on the chart
    * `disableUndo` prevents adding of the action to the undo stack
    * `overrides` is an object containing properties you'd like to set for your new shape.
    * `zOrder` can have the following values `top`, `bottom`.
        `top` places the line tool on top of all other chart objects while `bottom` places the line tool behind all other chart objects.
        If not specified the line tool is placed on top of all existing chart objects.
    * `showInObjectsTree`: Displays the shape in the Objects Tree dialog. The default value is `true`.
    * `ownerStudyId`: optional argument of `EntityId` type. It can be used to bind a line tool to a study. For instance, it can be used to create a shape on an additional pane.

The function returns `entityId` - unique ID of the shape if the creation was successful and `null` if it wasn't.

This call creates a shape at a specific point on the chart provided that it's within the main series area.

```javascript
widget.activeChart().createShape({ time: 1514764800 }, { shape: 'vertical_line' });
```

### createMultipointShape(points, options)

1. `points`: is an array of object with the following keys `[{time, [price], [channel]},...]`
    * `time`: unix time. It's the only mandatory key in this function argument.
    * `price`: If you specify `price`, then the shape will be placed at the same price level.
        If not, then the shape will be placed close to the bar according the `channel` value.
    * `channel`: If the price is not set then `channel` value defines where the shape is placed relative to the bar. Possible values are `open`, `high`, `low`, `close`.
        If no channel is specified, 'open' is a default value.
1. `options`: object `{shape, [text], [lock], [overrides]}`
    * `shape` may be one of the [identifiers](Shapes-and-Overrides)
    * `text` is an optional argument. It's the text that will be included in the shape if it's supported. Additional field `showLabel` in overrides may be necessary.
    * `lock` shows whether a user will be able to remove/change/hide the shape or not.
    * `disableSelection` prevents selecting of the shape
    * `disableSave` prevents saving the shape on the chart
    * `disableUndo` prevents adding of the action to the undo stack
    * `overrides` is an object containing properties you'd like to set for your new shape.
    * `zOrder` can have the following values `top`, `bottom`.
        `top` places the line tool on top of all other chart objects while `bottom` places the line tool behind all other chart objects.
        If not specified the line tool is placed on top of all existing chart objects.
    * `showInObjectsTree`: Displays the shape in the Objects Tree dialog. The default value is `true`.
    * `ownerStudyId`: optional argument of `EntityId` type. It can be used to bind a line tool to a study. For instance, it can be used to create a shape on an additional pane.
    * `filled`: **defaults to true**. If true, and the shape supports it, fills the shape with color.

The function returns `entityId` - unique ID of the shape if the creation was successful and `null` if it wasn't.

Check out [Shapes and Overrides](Shapes-and-Overrides) for more information.

This call creates a shape at a specific point on the chart provided that it's within the main series area.

```javascript
const from = Date.now() / 1000 - 500 * 24 * 3600; // 500 days ago
const to = Date.now() / 1000;
widget.activeChart().createMultipointShape(
    [{ time: from, price: 150 }, { time: to, price: 150 }],
    {
        shape: "trend_line",
        lock: true,
        disableSelection: true,
        disableSave: true,
        disableUndo: true,
        text: "text",
    }
);

```

### getShapeById(entityId)

1. `entityId`: object. The value that is returned when a shape is created via API

Returns an instance of the [ShapeApi](Shape-Api) that allows you to interact with the shape.

```javascript
widget.activeChart().getShapeById(id).bringToFront();
```

### removeEntity(entityId, options)

1. `entityId`: object. It's the value that was returned when the entity (shape or study) was created.
1. `options` is an *optional* object added in version 17 with one field:
    * `disableUndo` - boolean flag that shows the undo action availability.

Removes the specified entity.

```javascript
widget.activeChart().removeEntity(id);
```

### removeAllShapes()

Removes all the shapes from the chart.

```javascript
widget.activeChart().removeAllShapes();
```

### removeAllStudies()

Removes all the studies from the chart.

```javascript
widget.activeChart().removeAllStudies();
```

### getPanes()

Returns an array of instances of the [PaneApi](Pane-Api) that allows you to interact with the panes.

```javascript
widget.activeChart().getPanes()[1].moveTo(0);
```

### shapesGroupController()

Returns an [API](Shapes-Group-Api) that can be used to work with groups of shapes.

```javascript
widget.activeChart().shapesGroupController().createGroupFromSelection();
```

## Z-order operations

### availableZOrderOperations(entities)

1. `entities` is an array of identifiers

Returns an object with operations available for the specified set of objects.

This structure has the following fields:

* `bringForwardEnabled`: true if one can bring specified entities forward
* `bringToFrontEnabled`: true if one can bring specified entities to front
* `sendBackwardEnabled`: true if one can send specified entities backward
* `sendToBackEnabled`: true if one can send specified entities to back

```javascript
widget.activeChart().availableZOrderOperations([id]);
```

### sendToBack(entities)

1. `entities` is an array of identifiers

Sends specified entities to back.

```javascript
widget.activeChart().sendToBack([id]);
```

### bringToFront(entities)

1. `entities` is an array of identifiers

Brings specified entities to front.

```javascript
widget.activeChart().bringToFront([id]);
```

### bringForward(entities)

1. `entities` is an array of identifiers

Brings specified entities one step forward (makes it higher).

```javascript
widget.activeChart().bringForward([id]);
```

### sendBackward(entities)

1. `entities` is an array of identifiers

Sends specified entities one step backward (makes it lower).

```javascript
widget.activeChart().sendBackward([id]);
```

## Study Templates

### createStudyTemplate(options)

1. `options`: object `{ saveSymbol, saveInterval }`
    * `saveSymbol`: boolean
    * `saveInterval`: boolean

Saves the study template to JS object. Charting Library will call your callback function and pass the state object as an argument.

This call is a part of low-level [save/load API](Saving-and-Loading-Charts).

```javascript
const options = { saveSymbol: true, saveInterval: true };
const template = widget.activeChart().createStudyTemplate(options);
```

### applyStudyTemplate(template)

1. `template`: object

Loads the study template from the `template` object.

This call is a part of low-level [save/load API](Saving-and-Loading-Charts).

```javascript
widget.activeChart().applyStudyTemplate(template);
```

## Trading Primitives

### createOrderLine(options)

1. `options` is a non-required object with one possible key - `disableUndo` which can be `true` or `false`.
    For compatibility reasons the default value is set to `false`.

Creates a new trading order on the chart and returns an API-object that you can use to adjust its properties and behavior.

It is strongly recommended to read [this article](Trading-Primitives) before using this call.

API object methods:

* `remove()`: Removes the position from the chart. You can’t this API-object after the call.
* `onModify(callback)` / `onModify(data, callback)`
* `onMove(callback)` / `onMove(data, callback)`
* `onCancel(callback)` / `onCancel(data, callback)`

API object has a set of properties listed below. Each property should be used through respective accessors.
For example, if you wish to work with the `Extend Left` property, then use `getExtendLeft()` of `setExtendLeft()` methods.

**General properties**:

Property|Type|Supported Values|Default Value
---|---|---|---
Price|Double|Double|0.0
Text|String|String|""
Tooltip|String|String|""
Modify Tooltip|String|String|""
Cancel Tooltip|String|String|""
Quantity|String|String|""
Editable|Boolean|Boolean|true
Cancellable|Boolean|Boolean|true

**Horizontal line properties**:

Property|Type|Supported Values|Default Value
---|---|---|---
Extend Left|Boolean|"inherit" or Boolean|True
Line Length|Integer|"inherit" or 0 .. 100|0
Line Style|Integer|"inherit" or 0 .. 2|2
Line Width|Integer|"inherit" or 1 .. 4|1

**Fonts**:

Property|Type|Default Value
---|---|---
Body Font|String|"bold 7pt Verdana"
Quantity Font|String|"bold 7pt Verdana"

**Colors**:

Property|Type|Default Value
---|---|---
Line Color|String|"rgb(255, 0, 0)"
Body Border Color|String|"rgb(255, 0, 0)"
Body Background Color|String|"rgba(255, 255, 255, 0.75)"
Body Text Color|String|"rgb(255, 0, 0)"
Quantity Border Color|String|"rgb(255, 0, 0)"
Quantity Background Color|String|"rgba(255, 0, 0, 0.75)"
Quantity Text Color|String|"rgb(255, 255, 255)"
Cancel Button Border Color|String|"rgb(255, 0, 0)"
Cancel Button Background Color|String|"rgba(255, 255, 255, 0.75)"
Cancel Button Icon Color|String|"rgb(255, 0, 0)"

Example:

```javascript
widget.activeChart().createOrderLine()
    .setTooltip("Additional order information")
    .setModifyTooltip("Modify order")
    .setCancelTooltip("Cancel order")
    .onMove(function() {
        this.setText("onMove called");
    })
    .onModify("onModify called", function(text) {
        this.setText(text);
    })
    .onCancel("onCancel called", function(text) {
        this.setText(text);
    })
    .setText("STOP: 73.5 (5,64%)")
    .setQuantity("2");
```

### createPositionLine(options)

1. `options` is an object with one possible key - `disableUndo` which can be `true` or `false`.
    For compatibility reasons the default value is set to `false`.

Creates a new trading position on the chart and returns an API-object that you can use to adjust its properties and behavior.

It is strongly recommended to read [this article](Trading-Primitives) before using this call.

API object methods:

* `remove()`: Removes the position from the chart. You can’t use this API-object after the call.
* `onClose(callback)` / `onClose(data, callback)`
* `onModify(callback)` / `onModify(data, callback)`
* `onReverse(callback)` / `onReverse(data, callback)`

API object has a set of properties listed below. Each property should be used through respective accessors.
For example, if you wish to work with `Extend Left` property, use `getExtendLeft()` of `setExtendLeft()` methods.

**General properties**:

Property|Type|Supported Values|Default Value
---|---|---|---
Price|Double|Double|0.0
Text|String|String|""
Tooltip|String|String|""
Protect Tooltip|String|String|""
Reverse Tooltip|String|String|""
Close Tooltip|String|String|""
Quantity|String|String|""

**Horizontal line properties**:

Property|Type|Supported Values|Default Value
---|---|---|---
Extend Left|Boolean|"inherit" or Boolean|True
Line Length|Integer|"inherit" or 0 .. 100|0
Line Style|Integer|"inherit" or 0 .. 2|2
Line Width|Integer|"inherit" or 1 .. 4|1

**Fonts**:

Property|Type|Default Value
---|---|---
Body Font|String|"bold 7pt Verdana"
Quantity Font|String|"bold 7pt Verdana"

**Colors**:

Property|Type|Default Value
---|---|---
Line Color|String|"rgb(0, 113, 224)"
Body Border Color|String|"rgb(0, 113, 224)"
Body Background Color|String|"rgba(255, 255, 255, 0.75)"
Body Text Color|String|"rgb(0, 113, 224)"
Quantity Border Color|String|"rgb(0, 113, 224)"
Quantity Background Color|String|"rgba(0, 113, 224, 0.75)"
Quantity Text Color|String|"rgb(255, 255, 255)"
Reverse Button Border Color|String|"rgb(0, 113, 224)"
Reverse Button Background Color|String|"rgba(255, 255, 255, 0.75)"
Reverse Button Icon Color|String|"rgb(0, 113, 224)"
Close Button Border Color|String|"rgb(0, 113, 224)"
Close Button Background Color|String|"rgba(255, 255, 255, 0.75)"
Close Button Icon Color|String|"rgb(0, 113, 224)"

Example:

```javascript
widget.chart().createPositionLine()
    .onModify(function() {
        this.setText("onModify called");
    })
    .onReverse("onReverse called", function(text) {
        this.setText(text);
    })
    .onClose("onClose called", function(text) {
        this.setText(text);
    })
    .setText("PROFIT: 71.1 (3.31%)")
    .setTooltip("Additional position information")
    .setProtectTooltip("Protect position")
    .setCloseTooltip("Close position")
    .setReverseTooltip("Reverse position")
    .setQuantity("8.235")
    .setPrice(160)
    .setExtendLeft(false)
    .setLineStyle(0)
    .setLineLength(25);
```

### createExecutionShape(options)

1. `options` is an object with one possible key - `disableUndo` which can be `true` or `false`.
    For compatibility reasons the default value is set to `false`.

Creates a new trade execution on the chart and returns an API-object that you can use to control the execution properties.

It is strongly recommended to read [this article](Trading-Primitives) before using this call.

API object has a set of properties listed below. Each property should be used through respective accessors.
For example, if you wish to work with `Extend Left` property, then use `getExtendLeft()` of `setExtendLeft()` methods.

API object methods:

* `remove()`: Removes the execution shape from the chart. You can’t use this API-object after the call.

**General properties**:

Property|Type|Supported Values|Default Value
---|---|---|---
Price|Double|Double|0.0
Time|Integer|Unix time|0
Direction|String|"buy" or "sell"|"buy"
Text|String|String|"execution"
Tooltip|String|String|
Arrow Height|Integer|Integer|8
Arrow Spacing|Integer|Integer|1

**Fonts**:

Property|Type|Default Value
---|---|---
Font|String|"8pt Verdana"

**Colors**:

Property|Type|Default Value
---|---|---
Text Color|String|"rgb(0, 0, 0)""
Arrow Color|String|"rgba(0, 0, 255)"

Example:

```javascript
widget.activeChart().createExecutionShape()
    .setText("@1,320.75 Limit Buy 1")
    .setTooltip("@1,320.75 Limit Buy 1")
    .setTextColor("rgba(0,255,0,0.5)")
    .setArrowColor("#0F0")
    .setDirection("buy")
    .setTime(widget.activeChart().getVisibleRange().from)
    .setPrice(160);
```

## Getters

### symbol()

Returns the current symbol of the chart.

```javascript
console.log(widget.activeChart().symbol());
```

### symbolExt()

Returns the current symbol information of the chart. The object has the following fields:

* `symbol`: is the same as the result of [symbol()](#symbol) method
* `full_name`: the full name of the symbol
* `exchange`: the exchange of the symbol
* `description`: the description of the symbol
* `type`: the type of the symbol

```javascript
console.log(widget.activeChart().symbolExt().full_name);
```

### resolution()

Returns the chart's time interval. The format is described in this [article](Resolution).

```javascript
console.log(widget.activeChart().resolution());
```

### getVisibleRange()

Returns the object `{from, to}`. `from` and `to` are Unix timestamps in the UTC timezone.

```javascript
console.log(widget.activeChart().getVisibleRange());
```

### getVisiblePriceRange()

*Starting from version 1.7.*

Deprecated, use [Price Scale API](Price-Scale-Api#getVisiblePriceRange) instead.

Returns the object `{from, to}`. `from` and `to` are boundaries of the price scale visible range in main series area.

```javascript
console.log(widget.activeChart().getVisiblePriceRange());
```

### scrollPosition()

*Starting from version 1.15.*

**Deprecated**: Use [rightOffset](Time-Scale-Api#rightoffset) instead.

Returns the distance from the right edge of the chart to the last bar, measured in bars.
This is actually the current scrolling position of the chart, including the right margin.

```javascript
console.log(widget.activeChart().scrollPosition());
```

### defaultScrollPosition()

*Starting from version 1.15.*

**Deprecated**: Use [defaultRightOffset](Time-Scale-Api#defaultrightoffset) instead.

Returns the default distance from the right edge of the chart to the last bar, measured in bars.

```javascript
console.log(widget.activeChart().defaultScrollPosition());
```

### priceFormatter()

Returns the object with `format` function that you can use to format the prices.

```javascript
widget.activeChart().priceFormatter().format(123);
```

### chartType()

Returns the main series style type.

```javascript
console.log(widget.activeChart().chartType());
```

### getPriceToBarRatio()

Returns the Price To Bar ratio or null if none is defined.

```javascript
console.log(widget.activeChart().getPriceToBarRatio());
```

### isPriceToBarRatioLocked()

Returns the state of the Price to Bar ratio option.

```javascript
console.log(widget.activeChart().isPriceToBarRatioLocked());
```

### getAllPanesHeight()

Returns all panes' heights in an array.

```javascript
console.log(widget.activeChart().getAllPanesHeight());
```

### setAllPanesHeight(heights)

1. `heights` is an array of numbers

Set the height for each panes in the order provided by the array.

```javascript
console.log(widget.activeChart().setAllPanesHeight([250, 400, 200]));
```

### maximizeChart()

Maximize to its full size currently selected chart.

```javascript
widget.activeChart().maximizeChart();
```

### restoreChart()

Restore to its initial size currently selected chart.

```javascript
widget.activeChart().restoreChart();
```

## Other

### exportData(options)

*Starting from version 1.14.*

1. `options` (optional) is an object, which can contain the following properties:
    * `from` (`number`) - date of the first exporting bar (UNIX timestamp in seconds).
        By default the time of the leftmost loaded bar is used.
    * `to` (`number`) - date of the last exporting bar (UNIX timestamp in seconds).
        By default the time of the rightmost (real-time) bar is used.
    * `includeTime` (`boolean`, default `true`) - defines whether each item of the exported data should contain time.
    * `includeUserTime` (`boolean`, default `false`) - defines whether each item of the exported data should contain [user time](#user-time).
    * `includeSeries` (`boolean`, default `true`) - defines whether the exported data should contain the main series (open, high, low, close).
    * `includedStudies` - which studies should be included in the exported data
        (by default, the value is `'all'` which means that all studies are included, but if you want to export only some of them then you can assign an array of [studies' ids](#getallstudies)).
    * `includeDisplayedValues` (`boolean`, default `false`) - returns formatted values for every value according to data source's formatter and params.

Exports data from the chart, returns a Promise object. This method doesn't load data. The result has the following structure:

* `schema` is an array of field descriptors, each descriptor might be one the following types:
  * `TimeFieldDescriptor` - description of the time field. It contains only one field - `type` with the `'time'` value.
  * `UserTimeFieldDescriptor` - description of the user time field. It contains only one field - `type` with the `'userTime'` value.
  * `SeriesFieldDescriptor` - description of a series field. It contains the following fields:
    * `type` (`'value'`)
    * `sourceType` (`'series'`)
    * `plotTitle` (`string`) - the name of the plot (open, high, low, close).
    * `sourceTitle` (`string`) - title of the series
  * `StudyFieldDescriptor` - description of a study field. It contains the following fields:
    * `type` (`'value'`)
    * `sourceType` (`'study'`)
    * `sourceId` (`string`) - id of the study
    * `sourceTitle` (`string`) - title of the study
    * `plotTitle` (`string`) - title of the plot

* `data` is an array of [Float64Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array)s.
   Each `Float64Array` array has the same length as `schema` array and represents the associated field's item.

* `displayedData` is an array of arrays of strings (i.e. `string[][]`).
   Each inner array has the same length as `schema` array and represents the display value of the associated field element.
   Note that this array will be empty if `includeDisplayedValues` option is `false`.

**Examples:**

1. `widget.activeChart().exportData({ includeTime: false, includedStudies: [] })` - to export series' data only.
1. `widget.activeChart().exportData({ includedStudies: [] })` - to export series' data with times.
1. `widget.activeChart().exportData({ includeTime: false, includeUserTime: true, includedStudies: [] })` - to export series' data with [user time](#user-time).
1. `widget.activeChart().exportData({ includeTime: false, includeSeries: false, includedStudies: ['STUDY_ID'] })` - to export data for the study with the id `STUDY_ID`.
1. `widget.activeChart().exportData({ includeUserTime: true })` - to export all available data from the chart.
1. `widget.activeChart().exportData({ includeTime: false, to: Date.UTC(2018, 0, 1) / 1000 })` - to export series' data before `2018-01-01`.
1. `widget.activeChart().exportData({ includeTime: false, from: Date.UTC(2018, 0, 1) / 1000 })` - to export series' data in the range before `2018-01-01`.
1. `widget.activeChart().exportData({ includeTime: false, from: Date.UTC(2018, 0, 1) / 1000, to: Date.UTC(2018, 1, 1) / 1000 })` - to export series' data in the range between `2018-01-01` and `2018-02-01`.
1. `widget.activeChart().exportData({ includeDisplayedValues: true })` - to export all displayed data on the chart.

#### User time

User time is the time that is displayed to the user on the chart, taking into account the selected time zone and resolution.

### selection()

*Starting from version 1.15.*

Returns [SelectionApi](Selection-Api) to that can be used to change the chart selection and subscribe to chart selection changes.

```javascript
widget.activeChart().selection().clear();
```

### setZoomEnabled(enabled)

*Starting from version 1.15.*

Enables (if the parameter is true) or disables (if the parameter is false) zooming of the chart.

```javascript
widget.activeChart().setZoomEnabled(false);
```

### setScrollEnabled(enabled)

*Starting from version 1.15.*

Enables (if the parameter is true) or disables (if the parameter is false) scrolling of the chart.

```javascript
widget.activeChart().setScrollEnabled(false);
```

### getTimeScale()

*Starting from version 18.*

Returns an instance of the [TimeScaleApi](Time-Scale-Api) with methods associated with the time axis.

```javascript
var time = widget.activeChart().getTimeScale().coordinateToTime(100);
```

### isSelectBarRequested()

*Starting from version 18.*

Returns whether the bar selection mode is active or not.

```javascript
var isRequested = widget.activeChart().isSelectBarRequested();
```

### requestSelectBar()

*Starting from version 18.*

Switches the chart state to the bar selection mode. For example, it is used to start Bar Replay.

Returns a Promise object, which will be resolved with a time (unix timestamp) of the bar selected by a user, or will be rejected if the bar selection was either already requested or cancelled (by a user action or by the [`cancelSelectBar()`](#cancelselectbar) method).

```javascript
widget.activeChart().requestSelectBar()
    .then(function(time) {
        console.log('user selects bar with time', time);
    })
    .catch(function() {
        console.log('bar selection was rejected');
    });
```

### cancelSelectBar()

*Starting from version 18.*

Cancels active select bar request if it exists, or do nothing otherwise.

```javascript
widget.activeChart().cancelSelectBar();
```

### setPriceToBarRatio(value, options)

1. `value` is the new ratio to set (number)
2. `options` is an object only containing the `disableUndo` boolean property

Set a new ratio along with some options.

```javascript
widget.activeChart().setPriceToBarRatio(0.4567, { disableUndo: true });
```

### setPriceToBarRatioLocked(value, options)

1. `value` is used to lock/unlock the Price To Bar Ratio (boolean)
2. `options` is an object only containing the `disableUndo` boolean property

Set/unset the lock property along with some options.

```javascript
widget.activeChart().setPriceToBarRatioLocked(true, { disableUndo: false });
```

## See Also

* [Widget Methods](Widget-Methods)
* [Widget Constructor](Widget-Constructor)
* [Saving and Loading Charts](Saving-and-Loading-Charts)
* [Overriding Studies' Defaults](Studies-Overrides)
* [Overriding Chart's Defaults](Overrides)
