You may specify Charting library widget parameters when calling its constructor. Here is an example of a call.

```javascript
new TradingView.widget({
    symbol: 'A',
    interval: '1D',
    timezone: "America/New_York",
    container: "tv_chart_container",
    locale: "ru",
    datafeed: new Datafeeds.UDFCompatibleDatafeed("https://demo_feed.tradingview.com"),
    library_path: "charting_library/"
});
```

Below is a complete list of supported parameters. Use [Widget methods](Widget-Methods) if you wish to modify the parameters after the creation of the Charting Library.

`* - Required`

## Parameters

* Library and Trading Terminal
  * [symbol, interval*](#symbol-interval)
  * [container*](#container)
  * [datafeed*](#datafeed)
  * [library_path*](#library_path)
  * [timeframe](#timeframe)
  * [timezone](#timezone)
  * [debug](#debug)
  * [width, height](#width-height)
  * [fullscreen](#fullscreen)
  * [autosize](#autosize)
  * [symbol_search_request_delay](#symbol_search_request_delay)
  * [auto_save_delay](#auto_save_delay)
  * [toolbar_bg](#toolbar_bg)
  * [study_count_limit](#study_count_limit)
  * [studies_access](#studies_access)
  * [drawings_access](#drawings_access)
  * [saved_data](#saved_data)
  * [saved_data_meta_info](#saved_data_meta_info)
  * [locale](#locale)
  * [numeric_formatting](#numeric_formatting)
  * [custom_formatters](#custom_formatters)
  * [overrides](#overrides)
  * [disabled_features, enabled_features](#disabled_features-enabled_features)
  * [snapshot_url](#snapshot_url)
  * [custom_indicators_getter](#custom_indicators_getter)
  * [preset](#preset)
  * [studies_overrides](#studies_overrides)
  * [time_frames](#time_frames)
  * [charts_storage_url, client_id, user_id](#charts_storage_url-client_id-user_id)
  * [charts_storage_api_version](#charts_storage_api_version)
  * [load_last_chart](#load_last_chart)
  * [theme](#theme)
  * [custom_css_url](#custom_css_url)
  * [custom_font_family](#custom_font_family)
  * [loading_screen](#loading_screen)
  * [favorites](#favorites)
  * [save_load_adapter](#save_load_adapter)
  * [settings_adapter](#settings_adapter)
  * [compare_symbols](#compare_symbols)
  * [additional_symbol_info_fields](#additional_symbol_info_fields)
  * [header_widget_buttons_mode](#header_widget_buttons_mode)
  * [time_scale](#time_scale)
  * [custom_translate_function](#custom_translate_function)
  * [symbol_search_complete](#symbol_search_complete)
  * [context_menu](#context_menu)
  * [settings_overrides](#settings_overrides)
* Trading Terminal only
  * [widgetbar](#widgetbar)
  * [rss_news_feed](#rss_news_feed)
  * [news_provider](#news_provider)
  * [broker_factory](#broker_factory)
  * [broker_config](#broker_config)

## Library and Trading Terminal

### symbol, interval*

The default symbol & time interval of your chart. The `interval` value is described in the [Section](Resolution).

```javascript
symbol: 'A',
interval: '1D',
```

### container*

The `container` can either be a reference to an attribute of a DOM element inside which the iframe with the chart will be placed or the `HTMLElement` itself.

```javascript
container: "tv_chart_container",
```

or

```javascript
container: document.getElementById("tv_chart_container"),
```

### datafeed*

JavaScript object that implements the ([JS API](JS-Api)) interface to supply the chart with data.

```javascript
datafeed: new Datafeeds.UDFCompatibleDatafeed("https://demo_feed.tradingview.com")
```

### timeframe

Sets the default timeframe of the chart. Timeframe is a period of bars that will be loaded and shown on the screen.
Valid timeframe is a number with a letter D for days and M for months.

```javascript
timeframe: '3M',
```

### timezone

Default timezone of the chart. The time on the timescale is displayed according to this timezone.
See the [list of supported timezones](Symbology#timezone) for available values. Set it to `exchange` to use the exchange timezone. Use the [overrides](#overrides) section if you wish to override the default value.

```javascript
timezone: "America/New_York",
```

### debug

Setting this property to `true` will make the chart write detailed API logs into the browser console. Alternatively, you can use the `charting_library_debug_mode` featureset to enable it.

```javascript
debug: true,
```

### library_path

A path to a `static` folder.

```javascript
library_path: "charting_library/",
```

### width, height

The desired size of a widget. Please make sure that there is enough space for the widget to be displayed correctly.

```javascript
width: 300,
height: 600,
```

**Remark**: If you want the chart to use all the available space use the `fullscreen` parameter instead of setting it to '100%'.

### fullscreen

*Default:* `false`

Boolean value showing whether the chart should use all the available space in the window.

```javascript
fullscreen: true,
```

### autosize

*Default:* `false`

Boolean value showing whether the chart should use all the available space in the container and resize when the container itself is resized.

```javascript
autosize: true,
```

### symbol_search_request_delay

A threshold delay in milliseconds that is used to reduce the number of symbol search requests when the user is typing a name of a symbol in the search box.

```javascript
symbol_search_request_delay: 1000,
```

### auto_save_delay

A threshold delay in seconds that is used to reduce the number of `onAutoSaveNeeded` calls.

```javascript
auto_save_delay: 5,
```

### toolbar_bg

Background color of the toolbars.

```javascript
toolbar_bg: '#f4f7f9',
```

### study_count_limit

*Starting from version 1.5.*

Maximum amount of studies on the chart of a multichart layout. Minimum value is 2.

```javascript
study_count_limit: 5,
```

### studies_access

*Starting from version 1.1.*

An object with the following structure:

```javascript
studies_access: {
    type: "black" | "white",
    tools: [
        {
            name: "<study name>",
            grayed: true
        },
        < ... >
    ]
}
```

* `type` is the list type. Supported values are: `black` (all listed items should be disabled), `white` (only the listed items should be enabled).
* `tools` is an array of objects. Each object could have the following properties:
  * `name` (*Mandatory*) is the name of a study. Use the same names as in the pop-ups of indicators.
  * `grayed` is a boolean showing whether this study should be visible but look as if it's disabled. If the study is grayed out and user clicks it, then the `onGrayedObjectClicked` function is called.

### drawings_access

*Starting from version 1.1.*

This property has the same structure as the `studies_access`argument that is described above. Use the same names as you see in the UI.

```javascript
drawings_access: {
    type: 'black',
    tools: [
        {
            name: 'Trend Line',
            grayed: true
        },
    ]
},
```

**Remark**: There is a special case for font-based drawings. Use the "Font Icons" name for them. Those drawings cannot be enabled or disabled separately - the entire group will have to be either enabled or disabled.

### saved_data

JS object containing saved chart content. Use this parameter when creating the widget if you have a saved chart already. If you want to load the chart content when the chart is initialized then use [load() method](https://github.com/tradingview/charting_library/wiki/Widget-Methods#loadstate) of the widget.

### saved_data_meta_info

JS object containing saved chart content meta info. This object should have the following fields:

* `uid`: unique integer identifier of the chart
* `name`: saved chart name
* `description`: saved chart description

### locale

Locale to be used by Charting Library. See [Localization](Localization) section for details.

```javascript
locale: 'en',
```

### numeric_formatting

The object containing formatting options for numbers. The only possible option is `decimal_sign` currently.

```javascript
numeric_formatting: { decimal_sign: "," },
```

### custom_formatters

It is an object that contains the following fields:

1. timeFormatter
2. dateFormatter
3. tickMarkFormatter
4. priceFormatterFactory

You can use these formatters to adjust the display format of the date and time values.
`timeFormatter` and `dateFormatter` are objects that include functions such as `format` and `formatLocal`:

```javascript
function format(date)
function formatLocal(date)
```

These functions should return the text that specifies date or time. `formatLocal` should convert date and time to local timezone.

`tickMarkFormatter` is a function with the following signature:

```typescript
function tickMarkFormatter(date: Date, tickMarkType: TickMarkType): string;

/**
 * Represents the type of a tick mark on the time axis.
 */
type TickMarkType =
    /**
     * The start of the year (e.g. it's the first tick mark in a year).
     */
    | 'Year'
    /**
     * The start of the month (e.g. it's the first tick mark in a month).
     */
    | 'Month'
    /**
     * A day of the month.
     */
    | 'DayOfMonth'
    /**
     * A time without seconds.
     */
    | 'Time'
    /**
     * A time with seconds.
     */
    | 'TimeWithSeconds';
```

`priceFormatterFactory` is a function with the following signature:

```typescript
function priceFormatterFactory(symbolInfo: ISymbolInfo | null, minTick: string): ISymbolValueFormatter;

interface ISymbolValueFormatter {
    format(price: number, signPositive?: boolean): string;
}

```

Example:

```javascript
custom_formatters: {
    timeFormatter: {
        format: (date) => {
            const _format_str = '%h:%m';
            return _format_str
                .replace('%h', date.getUTCHours(), 2)
                .replace('%m', date.getUTCMinutes(), 2)
                .replace('%s', date.getUTCSeconds(), 2);
        }
    },
    dateFormatter: {
        format: (date) => {
            return date.getUTCFullYear() + '/' + (date.getUTCMonth() + 1) + '/' + date.getUTCDate();
        }
    },
    tickMarkFormatter: (date, tickMarkType) => {
        switch (tickMarkType) {
            case 'Year':
                return 'Y' + date.getUTCFullYear();

            case 'Month':
                return 'M' + (date.getUTCMonth() + 1);

            case 'DayOfMonth':
                return 'D' + date.getUTCDate();

            case 'Time':
                return 'T' + date.getUTCHours() + ':' + date.getUTCMinutes();

            case 'TimeWithSeconds':
                return 'S' + date.getUTCHours() + ':' + date.getUTCMinutes() + ':' + date.getUTCSeconds();
        }

        throw new Error('unhandled tick mark type ' + tickMarkType);
    },
    priceFormatterFactory: (symbolInfo, minTick) => {
        if (symbolInfo?.fractional || minTick !== 'default' && minTick.split(',')[2] === 'true') {
            return {
                format: (price, signPositive) => {
                    // return the appropriate format
                },
            };
        }
        return null; // this is to use default formatter;
    },
}
```

**Remark**: `tickMarkFormatter` must display the UTC date, and not the date corresponding to your local timezone.

### overrides

The object that contains new values for default widget properties.
You can override most of the Charting Library properties (which also may be edited by user through UI) using `overrides` parameter of Widget constructor. `overrides` is supposed to be an object. The keys of this object are the names of overridden properties. The values of these keys are the new values of the properties. Example:

```javascript
overrides: {
    "mainSeriesProperties.style": 2
}
```

This code will change the default series style to "line". All customizable properties are listed in [separate article](Overrides). You can use [Drawings-Overrides](Drawings-Overrides) starting from v 1.5.

### disabled_features, enabled_features

The array containing names of features that should be enabled/disabled by default. `Feature` means part of the functionality of the chart (part of the UI/UX). Supported features are listed [here](Featuresets).

Example:

```javascript
disabled_features: ["header_widget", "left_toolbar"],
enabled_features: ["move_logo_to_main_pane"],
```

### snapshot_url

This URL is used to send a POST request with binary chart snapshots when a user presses the snapshot button.
This POST request contains `multipart/form-data` with the field `preparedImage` that represents binary data of the snapshot image in `image/png` format.

This endpoint should return the full URL of the saved image in the the response.

```javascript
snapshot_url: "https://myserver.com/snapshot",
```

### custom_indicators_getter

Function that returns a Promise object with an array of your custom indicators.

`PineJS` variable will be passed as the first argument of this function and can be used inside your indicators to access internal helper functions.

See more details [here](Creating-Custom-Studies).

```javascript
custom_indicators_getter: function(PineJS) {
    return Promise.resolve([
        // *** your indicator object, created from the template ***
    ]);
},
```

### preset

`preset` is a name of predefined widget settings. For now, the only value supported in the `preset` is  `mobile`. The example of this `preset` is [available here](https://charting-library.tradingview-widget.com).

```javascript
preset: "mobile",
```

### studies_overrides

Use this option to customize the style or inputs of the indicators. You can also customize the styles and inputs of the `Compare` series using this argument. See more details [here](Studies-Overrides)

```javascript
studies_overrides: {
    "volume.volume.color.0": "#00FFFF",
},
```

### time_frames

List of visible timeframes that can be selected at the bottom of the chart. See [this topic](Time-Frames) to learn more about timeframes. Timeframe is an object containing following properties:

* `text` - a string with the following format: `<integer><y|m|d>` ( \d+(y|m|d) as Regex ). It defines the range to be set.
* `resolution` - a string with the format described [here](Resolution). It defines the resolution to be set.
* `description` (optional) - a string that is displayed in the pop-up menu. If it isn't set then the `title` property is used.
* `title` (optional) - a string representation of the time frame. If it is not set then the title is generated based on the `text` property.

Example:

```javascript
time_frames: [
    { text: "50y", resolution: "6M", description: "50 Years" },
    { text: "3y", resolution: "1W", description: "3 Years", title: "3yr" },
    { text: "8m", resolution: "1D", description: "8 Month" },
    { text: "3d", resolution: "5", description: "3 Days" },
    { text: "1000y", resolution: "1W", description: "All", title: "All" },
]
```

### charts_storage_url, client_id, user_id

These arguments are related to the high-level API for saving/loading the charts. See more details [here](Saving-and-Loading-Charts).

```javascript
charts_storage_url: 'http://storage.yourserver.com',
client_id: 'yourserver.com',
user_id: 'public_user_id',
```

### charts_storage_api_version

A version of your backend. Supported values are: `"1.0"` | `"1.1"`. Study Templates are supported starting from version `"1.1"`.

```javascript
charts_storage_api_version: "1.1",
```

### load_last_chart

Set this parameter to `true` if you want the library to load the last saved chart for a user (you should implement [save/load](Saving-and-Loading-Charts) first to make it work).

```javascript
load_last_chart: true,
```

### theme

*Starting from version 1.13.*

Adds custom theme color for the chart. Supported values are: `"Light"` | `"Dark"`.

```javascript
theme: "Light",
```

### custom_css_url

*Starting from version 1.4.*

Adds your custom CSS to the chart. `url` should be an absolute or relative path to the `static` folder.

```javascript
custom_css_url: 'css/style.css',
```

### custom_font_family

Change the font family used on the chart. The value should be in the same format as the `font-family` property in CSS.
If you want to use a font that is not available by default on your system, you need to first load the font in your [custom CSS](#custom_css_url).

E.g. importing a google font in your custom CSS:

```css
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@500&display=swap');
```

Add `custom_font_family` to your widget options:

```javascript
custom_font_family: "'Inconsolata', monospace",
```

### loading_screen

*Starting from version 1.12.*

Customization of the loading spinner. Value is an object with the following possible keys:

* `backgroundColor`
* `foregroundColor`

Example:

```javascript
loading_screen: { backgroundColor: "#000000" }
```

### favorites

Items that should be marked as favorite by default. This option requires that the usage of localstorage is disabled (see [featuresets](Featuresets) to know more). The `favorites` property is supposed to be an object. The following properties are supported:

* **intervals**: an array of time intervals that are marked as favorite. Example: `["D", "2D"]`
* **chartTypes**: an array of chart types that are marked as favorite. The names of chart types are identical to chart's UI in the English version. Example: `["Area", "Candles"]`.

```javascript
favorites: {
    intervals: ["1D", "3D", "3W", "W", "M"],
    chartTypes: ["Area", "Line"]
},
```

### save_load_adapter

An object containing the save/load functions. It is used to implement a custom save/load algorithm. Please see details and an example on [Saving and Loading Charts page](Saving-and-Loading-Charts#api-handlers).

### settings_adapter

*Starting from version 1.11.*

An object that contains set/remove functions. Use it to save chart settings to your preferred storage (including server-side). If it is available then it should have the following methods:

1. `initialSettings: Object`

    An object with the initial settings

1. `setValue(key: string, value: string): void`

    A function that is called to store key/value pair.

1. `removeValue(key: string): void`

    A function that is called to remove a key.

```javascript
settings_adapter: {
    initialSettings: { ... },
    setValue: function(key, value) { ... },
    removeValue: function(key) { ... },
}
```

### compare_symbols

*Starting from version 17.*

An optional field containing an array of custom compare symbols for the Compare window.
Each symbol info should contain the following fields:

* `symbol` - a string that defines a symbol to compare
* `title` - a string, the name of instrument that will be displayed near the corresponding checkbox

```javascript
compare_symbols: [
    { symbol: 'DAL', title: 'Delta Air Lines' },
    { symbol: 'VZ', title: 'Verizon' },
    ...
];
```

### additional_symbol_info_fields

An optional field containing an array of custom symbol info fields to be shown in the Symbol Info dialog.
Each additional symbol info field should have the following properties:

* `title` - a string that is used as the name of the new symbol info
* `propertyName` - a string that is used to look up a property from the symbol info returned from the chart's datafeed

See [Symbology](Symbology#SymbolInfo-Structure) for more information about symbol info.

```javascript
additional_symbol_info_fields: [
    { title: 'Ticker', propertyName: 'ticker' }
]
```

### header_widget_buttons_mode

An additional optional field to change the look and feel of buttons on the top toolbar.
Mode can be of the following:

* `fullsize`: always full-size buttons on the top toolbar
* `adaptive`: adaptive/auto mode (fullsize if the window width allows and icons on small windows).
* `compact`: icons only buttons on the top toolbar (favorites won't be shown)

By default (if option is omitted) header will be in adaptive mode (fullsize if the window width allows and icons on smaller windows).

```javascript
header_widget_buttons_mode: 'fullsize',
```

### time_scale

An additional optional field to add more bars on screen.
At the moment the only sub-option available are:

* `min_bar_spacing`: number - should be greater than 0.

```javascript
time_scale: {
    min_bar_spacing: 10,
}
```

### custom_translate_function

Use this property to set your own translation function. `key` and `options` will be passed to the function.

You can use this function to provide custom translations for some strings.

The function should return either a string with a new translation or `null` to fallback to the default translation.

For example, if you want to rename "Trend Line" shape to "Line Shape", then you can do something like this:

```javascript
custom_translate_function: (key, options) => {
    if (key === 'Trend Line') {
        // patch the title of trend line
        return 'Line Shape';
    }

    return null;
}
```

### symbol_search_complete

Use this property to set a function to override the symbol input from symbol search dialogs.

For example for you may want to get additional input from the user before deciding which symbol should be resolved.

The function should take one parameter: a `string` of input from the symbol search and should return a `Promise` that resolves with the new symbol string.

**NOTE:** This override is not called when adding a symbol to the watchlist.

```javascript
symbol_search_complete: (symbol) => {
    return new Promise((resolve) => {
        let newSymbol = getNewSymbol(symbol);
        resolve(newSymbol);
    });
}
```

### context_menu

You could use this object to override context menu in some way.

#### items_processor

Provide this function if you want to change the set of actions being displayed in the context menu.

You can filter out, add yours and re-order items.

The library will call your function each time it wants to display a context menu and with provide a list of items to display.
This function should return an array of items to display.

A function has the following signature:

```ts
type ContextMenuItemsProcessor = (items: readonly IActionVariant[], actionsFactory: ActionsFactory) => Promise<readonly IActionVariant[]>;
```

Where:

* `items` - an array of items the library wants to display
* `actionsFactory` - a factory you could use to create a new items for the context menu.
  It consists of the following methods:
  * `createAction` - creates an action with provided options.
  * `createAsyncAction` - creates an action that will wait for a promise to get its options. In terms of GUI until a promise is resolved the loader/spinner will be displayed.
  * `createSeparator` - creates a separator item.

Your function must return a Promise for an array of context menu items to display.
Please look at [TypeScript declaration file](https://github.com/tradingview/charting_library/blob/unstable/charting_library/charting_library.d.ts) provided with the package for types and possible options/functions you might use.

#### renderer_factory

**EXPERIMENTAL.**

By providing this function you could override the default renderer for context menu.
The signature of the function is the following:

```ts
export type ContextMenuRendererFactory = (items: readonly IActionVariant[], params: CreateContextMenuParams, onDestroy: () => void) => Promise<IContextMenuRenderer>;
```

Where:

* `items` - an array of items the library wants to display
* `params` - an object representing where the user right-clicked on (only if there is an existing menu), consisting of:
  * `menuName` - name of the menu
  * `detail` - object providing more details for the menu:
    * `type` - could be either `series` | `study`, `shape` or `groupOfShapes`
    * `id` - string (series), string | null (study), number | string | null (shape) or string | null (groupOfShapes)
* `onDestroy` - a function that you should call once a created menu is hidden/destroyed

The returned value should be a Promise object that resolves with an object with the following methods:

* `show(pos)` - displays the menu at the position `pos`. Please refer to [TypeScript declaration file](https://github.com/tradingview/charting_library/blob/unstable/charting_library/charting_library.d.ts) for exact type of `position` object.
* `hide()` - hides the menu.
* `isShown()` - returns whether a menu is currently displayed.

### settings_overrides

The object that contains new values for values saved to the settings. These overrides will replace any matching values from the settings, regardless of where the settings are loaded from (i.e. local storage or a custom settings adapter). The object is similar to the [overrides](#overrides) object.

[overrides](#overrides) will not affect values that have been saved to settings so this option can be used instead.

```javascript
settings_overrides: {
    "linetooltrendline.linecolor": "blue"
}
```

## Trading Terminal only

### widgetbar

:chart: *applies to [Trading Terminal](Trading-Terminal) only*

The object that contains settings for the widget panel on the right side of the chart. Watchlist, news, details and data window widgets on the right side of the chart can be enabled using the `widgetbar` field in Widget constructor:

```javascript
widgetbar: {
    details: true,
    watchlist: true,
    news: true,
    datawindow: true,
    watchlist_settings: {
        default_symbols: ["NYSE:AA", "NYSE:AAL", "NASDAQ:AAPL"],
        readonly: false
    },
}
```

* `details` (*default:* `false`): Enables details widget in the widget panel on the right.
* `watchlist` (*default:* `false`): Enables watchlist widget in the widget panel on the right.
* `news` (*default:* `false`): Enables news widget in the widget panel on the right.
* `datawindow` (*default:* `false`): Enables data window widget in the widget panel on the right.
* `watchlist_settings.default_symbols` (*default:* `[]`): Sets the list of default symbols for watchlist.
* `watchlist_settings.readonly` (*default:* `false`): Enables read-only mode for the watchlist.

### rss_news_feed

:chart: *applies to [Trading Terminal](Trading-Terminal) only*

Use this property to change the RSS feed for news. You can set a different RSS for each symbol type or use a single RSS for all symbols. The object should have the `default` property, other properties are optional. The names of the properties match the symbol types. Each property is an object (or an array of objects) with the following properties:

1. `url` - is a URL to be requested. It can contain tags in curly brackets that will be replaced by the terminal: `{SYMBOL}`, `{TYPE}`, `{EXCHANGE}`.
1. `name` - is a name of the feed to be displayed underneath the news.

Here is an example:

```javascript
rss_news_feed: {
    default: [ {
        url: "https://articlefeeds.nasdaq.com/nasdaq/symbols?symbol={SYMBOL}",
        name: "NASDAQ"
      }, {
        url: "http://feeds.finance.yahoo.com/rss/2.0/headline?s={SYMBOL}&region=US&lang=en-US",
        name: "Yahoo Finance"
      } ]
},
```

Another example:

```javascript
rss_news_feed: {
    "default": {
        url: "https://articlefeeds.nasdaq.com/nasdaq/symbols?symbol={SYMBOL}",
        name: "NASDAQ"
    }
}
```

One more example:

```javascript
rss_news_feed: {
    "default": {
        url: "https://articlefeeds.nasdaq.com/nasdaq/symbols?symbol={SYMBOL}",
        name: "NASDAQ"
     },
    "stock": {
        url: "http://feeds.finance.yahoo.com/rss/2.0/headline?s={SYMBOL}&region=US&lang=en-US",
        name: "Yahoo Finance"
    }
}
```

### news_provider

:chart: *applies to [Trading Terminal](Trading-Terminal) only*

Use this property to set your own news getter function. Both the `symbol` and `callback` will be passed to the function.

The callback function should be called with an object. The object should have two properties: `title` which is a optional string, and `newsItems` which is an array of news objects that have the following structure:

* `title` (required) - the title of news item.
* `published` (required) - the time of news item in ms (UTC).
* `source` (optional) - source of the news item title.
* `shortDescription` (optional) - Short description of a news item that will be displayed under the title.
* `link` (optional) - URL to the news story.
* `fullDescription` (optional) - full description (body) of a news item.

**NOTE:** Only `title` and `published` are the main properties used to compare what has already been published and what's new.

**NOTE 2:** When a user clicks on a news item a new tab with the `link` URL will be opened. If `link` is not specified then a pop-up dialog with `fullDescription` will be shown.

**NOTE 3:** If both `news_provider` and `rss_news_feed` are available then the `rss_news_feed` will be ignored.

See [News API examples](News-Api-Examples) for usage examples.

### broker_factory

:chart: *applies to [Trading Terminal](Trading-Terminal) only*

Use this field to pass the function that returns a new object which implements [Broker API](Broker-API). This is a function that accepts [Trading Host](Trading-Host) and returns [Broker API](Broker-API).

```javascript
broker_factory: function(host) { ... }
```

### broker_config

:chart: *applies to [Trading Terminal](Trading-Terminal) only*

Use this field to set the configuration flags for the Trading Terminal. [Read more](Trading-Objects-and-Constants#configflags-object).

```javascript
broker_config: {
    supportReversePosition: true,
    supportPLUpdate: true,
    ...
},
```

## See Also

* [Widget Methods](Widget-Methods)
* [Featuresets](Featuresets)
* [Saving and Loading Charts](Saving-and-Loading-Charts)
* [Overriding Default Properties of the Studies](Studies-Overrides)
* [Overriding Default Properties of the Chart](Overrides)
