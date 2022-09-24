The Charting Library uses your own data where you define the symbology yourself. You may name the symbols as you see fit.

But there are some fine points that you should be aware of:

1. Our own symbology assumes that symbol names use `EXCHANGE:SYMBOL` format.
   The Library supports this by default. You may continue using if it meets your requirements.
1. If you already have or considering a different symbology then you might want to use the `ticker` field.

   `ticker` is the unique identifier of the symbol that is used **only** inside the Library. Your users will never be able to see it.
   Simply enter the `ticker` values in all of your SymbolInfo objects and Symbol Search results and expect that the Charting Library will request the data based on those values.

# SymbolInfo Structure

**This section is extremely important. 72.2% of all issues experienced by Charting Library users are caused by wrong/malformed SymbolInfo data.**

SymbolInfo is an object containing symbol metadata. This object is the result of resolving the symbol. SymbolInfo has following fields:

## name

It's the name of the symbol. It is a string that your users will be able to see. Also, it will be used for data requests if you are not using **tickers**.

## ticker

It's an unique identifier for this particular symbol in your symbology.
If you specify this property then its value will be used for all data requests for this symbol. `ticker` will be treated the same as [name](#name) if not specified explicitly.

## description

Description of a symbol. Will be displayed in the chart legend for this symbol.

## type

Optional type of the instrument.

*Possible types are:*

- `stock`
- `index`
- `forex`
- `futures`
- `crypto`
- `expression`
- `spread`
- `cfd`
- or another string value.

## session

Trading hours for this symbol. See the [Trading Sessions](Trading-Sessions) article to learn more details.

## session_display

The session value to display in the UI. If not specified, then `session` is used.

## session_holidays

List of holidays for this symbol. These dates are not displayed on the chart.
It's a string in the following format:

`YYYYMMDD[,YYYYMMDD]`.

Example: `20181105,20181107,20181112`.

## corrections

List of corrections for this symbol. Corrections are days with specific trading sessions. They can be applied to holidays as well.
It's a string in the following format:

`SESSION:YYYYMMDD[,YYYYMMDD][;SESSION:YYYYMMDD[,YYYYMMDD]]`.

Where `SESSION` has the same format as [Trading Sessions](Trading-Sessions).

Example: `1900F4-2350F4,1000-1845:20181113;1000-1400:20181114`.

## exchange, listed_exchange

Both of these fields are expected to have a short name of the exchange where this symbol is traded.

The name will be displayed in the chart legend for this symbol.

## timezone

Timezone of the exchange for this symbol. We expect to get the name of the time zone in `olsondb` format.

*Supported timezones are:*

- `Etc/UTC`
- `Africa/Cairo`
- `Africa/Johannesburg`
- `Africa/Lagos`
- `America/Argentina/Buenos_Aires`
- `America/Bogota`
- `America/Caracas`
- `America/Chicago`
- `America/El_Salvador`
- `America/Juneau`
- `America/Lima`
- `America/Los_Angeles`
- `America/Mexico_City`
- `America/New_York`
- `America/Phoenix`
- `America/Santiago`
- `America/Sao_Paulo`
- `America/Toronto`
- `America/Vancouver`
- `Asia/Almaty`
- `Asia/Ashkhabad`
- `Asia/Bahrain`
- `Asia/Bangkok`
- `Asia/Chongqing`
- `Asia/Dubai`
- `Asia/Ho_Chi_Minh`
- `Asia/Hong_Kong`
- `Asia/Jakarta`
- `Asia/Jerusalem`
- `Asia/Karachi`
- `Asia/Kathmandu`
- `Asia/Kolkata`
- `Asia/Kuwait`
- `Asia/Manila`
- `Asia/Muscat`
- `Asia/Qatar`
- `Asia/Riyadh`
- `Asia/Seoul`
- `Asia/Shanghai`
- `Asia/Singapore`
- `Asia/Taipei`
- `Asia/Tehran`
- `Asia/Tokyo`
- `Atlantic/Reykjavik`
- `Australia/ACT`
- `Australia/Adelaide`
- `Australia/Brisbane`
- `Australia/Perth`
- `Australia/Sydney`
- `Europe/Athens`
- `Europe/Belgrade`
- `Europe/Berlin`
- `Europe/Bratislava`
- `Europe/Brussels`
- `Europe/Bucharest`
- `Europe/Budapest`
- `Europe/Copenhagen`
- `Europe/Helsinki`
- `Europe/Istanbul`
- `Europe/London`
- `Europe/Luxembourg`
- `Europe/Madrid`
- `Europe/Moscow`
- `Europe/Oslo`
- `Europe/Paris`
- `Europe/Riga`
- `Europe/Rome`
- `Europe/Stockholm`
- `Europe/Tallinn`
- `Europe/Vilnius`
- `Europe/Warsaw`
- `Europe/Zurich`
- `Pacific/Auckland`
- `Pacific/Chatham`
- `Pacific/Fakaofo`
- `Pacific/Honolulu`
- `Pacific/Norfolk`
- `US/Mountain`

## format

Format of displaying labels on the price scale:

- `price` - formats decimal or fractional numbers based on `minmov`, `pricescale`, `minmove2` and `fractional` values
- `volume` - formats decimal numbers in thousands, millions, billions or trillions

## minmov, pricescale, minmove2, fractional

These four keys have different meanings when used for common and fractional prices.

### Common prices

`MinimalPossiblePriceChange = minmov / pricescale`

- `minmov` is the amount of price precision steps for 1 tick. For example, since the tick size for U.S. equities is `0.01`, `minmov` is 1. But the price of the E-mini S&P futures contract moves upward or downward by `0.25` increments, so the `minmov` is `25`.
- `pricescale` defines the number of decimal places. It is `10^number-of-decimal-places`. If a price is displayed as `1.01`, `pricescale` is `100`; If it is displayed as `1.005`, `pricescale` is `1000`.
- `minmove2` for common prices is `0` or it can be skipped.
- `fractional` for common prices is `false` or it can be skipped.

Example:

Typical stock with `0.01` price increment: `minmov = 1, pricescale = 100, minmove2 = 0`.

### Fractional prices

Fractional prices are displayed 2 different forms: 1) `xx'yy` (for example, `133'21`) 2) `xx'yy'zz` (for example, `133'21'5`).

- `xx` is an integer part.
- `minmov/pricescale` is a Fraction.
- `minmove2` is used in form 2.
- `fractional` is `true`

Example:

If `minmov = 1`, `pricescale = 128` and `minmove2 = 4`:

- `119'16'0` represents `119 + 16/32`
- `119'16'2` represents `119 + 16.25/32`
- `119'16'5` represents `119 + 16.5/32`
- `119'16'7` represents `119 + 16.75/32`

More examples:

- `ZBM2014 (T-Bond)` with `1/32`: `minmov = 1`, `pricescale = 32`, `minmove2 = 0`
- `ZCM2014 (Corn)` with `2/8`: `minmov = 2`, `pricescale = 8`, `minmove2 = 0`
- `ZFM2014 (5 year t-note)` with `1/4 of 1/32`: `minmov = 1`, `pricescale = 128`, `minmove2 = 4`

## has_intraday

*Default:* `false`

Boolean value showing whether the symbol includes intraday (minutes) historical data.

If it's `false` then all buttons for intraday resolutions will be disabled for this particular symbol.

If it is set to `true`, all intradays resolutions that are supplied directly by the datafeed must be provided in `intraday_multipliers` array.

**WARNING** Any daily, weekly or monthly resolutions cannot be inferred from intraday resolutions!

## supported_resolutions

An array of resolutions which should be enabled for this symbol.

Each item of an array is expected to be a string. Format is described in another [article](Resolution).

If one changes the symbol and new symbol does not support the selected resolution then resolution will be switched to the first available one in the list.

Resolution availability logic (pseudocode):

```javascript
resolutionAvailable  =
    resolution.isIntraday
        ? symbol.has_intraday && symbol.supported_resolutions(resolution)
        : symbol.supported_resolutions(resolution);
```

In case of absence of `supported_resolutions` in a symbol info all DWM resolutions will be available. Intraday resolutions will be available if `has_intraday` is `true`.

Supported resolutions affect available timeframes too. The timeframe will not be available if it requires the resolution that is not supported.

## intraday_multipliers

*Default:* `[]`

Array of resolutions (in minutes) supported directly by the data feed.
Each such resolution may be passed to, and should be implemented by, [getBars](JS-Api#getbarssymbolinfo-resolution-periodparams-onhistorycallback-onerrorcallback).
The default of `[]` means that the data feed supports aggregating by any number of minutes.

If the data feed only supports certain minute resolutions but not the requested resolution, [getBars](JS-Api#getbarssymbolinfo-resolution-periodparams-onhistorycallback-onerrorcallback) will be called (repeatedly if needed) with a higher resolution as a parameter, in order to build the requested resolution.

For example, if the data feed only supports minute resolution, set `intraday_multipliers` to `['1']`.

When the user wants to see 5-minute data, [getBars](JS-Api#getbarssymbolinfo-resolution-periodparams-onhistorycallback-onerrorcallback) will be called with the resolution set to 1 until the library builds all the 5-minute resolution by itself.

## has_seconds

*Default:* `false`

Boolean value showing whether the symbol includes seconds in the historical data.

If it's `false` then all buttons for resolutions that include seconds will be disabled for this particular symbol.

If it is set to `true`, all resolutions that are supplied directly by the data feed must be provided in `seconds_multipliers` array.

## seconds_multipliers

*Default:* `[]`

It is an array containing resolutions that include seconds (excluding postfix) that the data feed provides.

E.g., if the data feed supports resolutions such as `["1S", "5S", "15S"]`, but has 1-second bars for some symbols then you should set `seconds_multipliers` of this symbol to `[1]`. This will make Charting Library build 5S and 15S resolutions by itself.

## has_ticks

*Default:* `false`

Boolean value showing whether the symbol includes ticks in the historical data.

If it's `false` then all buttons for resolutions that include ticks will be disabled for this particular symbol.

## has_daily

*Default:* `true`

The boolean value showing whether data feed has its own daily resolution bars or not.

If `has_daily` = `false` then Charting Library will build the respective resolutions using 1-minute bars by itself. If not, then it will request those bars from the data feed only if specified resolution belongs to `daily_multipliers`, otherwise an error will be thrown.

## daily_multipliers

*Default:* `['1']`

Array (of strings) containing the [resolutions](Resolution#Days) (in days - without the suffix) supported by the data feed.

For example it could be something like

```javascript
daily_multipliers = ['1', '3', '4', '6', '7'];
```

## has_weekly_and_monthly

*Default:* `false`

The boolean value showing whether data feed has its own weekly and monthly resolution bars or not.

If `has_weekly_and_monthly` = `false` then Charting Library will build the respective resolutions using daily bars by itself. If not, then it will request those bars from the data feed using either the `weekly_multipliers` or `monthly_multipliers` if specified. If resolution is not within either list an error will be raised.

## weekly_multipliers

*Default:* `['1']`

Array (of strings) containing the [resolutions](Resolution#Weeks) (in weeks - without the suffix) supported by the data feed.

For example it could be something like

```javascript
weekly_multipliers = ['1', '5', '10'];
```

## monthly_multipliers

*Default:* `['1']`

Array (of strings) containing the [resolutions](Resolution#Months) (in months - without the suffix) supported by the data feed.

For example it could be something like

```javascript
monthly_multipliers = ['1', '3', '4', '5', '10'];
```

## has_empty_bars

*Default:* `false`

The boolean value showing whether the library should generate empty bars in the session when there is no data from the data feed for this particular time.

I.e., if your session is `0900-1600` and your data has gaps between `11:00` and `12:00` and your `has_empty_bars` is `true`, then the Library will fill the gaps with bars for this time.

Flag `has_emtpy_bars` = `true` cannot be used if featureset `disable_resolution_rebuild` is enabled.

## has_no_volume

NOTE: `has_no_volume` is deprecated and will be removed in future releases, you should use `visible_plots_set` instead.

*Default:* `false`

Boolean showing whether the symbol includes volume data or not.

## visible_plots_set

*Default:* `ohlcv`

Represents what values are supported by the symbol. Possible values:

- `ohlcv` - the symbol supports open, high, low, close and has volume
- `ohlc` - the symbol supports open, high, low, close, but doesn't have volume
- `c` - the symbol supports only close, it's displayed on the chart using line-based styles only

## volume_precision

*Default:* `0`

Integer showing typical volume value decimal places for a particular symbol. 0 means volume is always an integer. 1 means that there might be 1 numeric character after the comma.

## data_status

The status code of a series with this symbol. The status is shown in the upper right corner of a chart.

*Supported statuses are:*

- `streaming`
- `endofday`
- `pulsed`
- `delayed_streaming`

## expired

*Default:* `false`

Boolean value showing whether this symbol is an expired futures contract or not.

## expiration_date

Unix timestamp of the expiration date. One must set this value when `expired` = `true`.

Charting Library will request data for this symbol starting from that time point.

## sector

Sector for stocks to be displayed in the Symbol Info.

## industry

Industry for stocks to be displayed in the Symbol Info.

## original_currency_code

The currency in which the instrument is traded.

## currency_code

The currency in which the instrument is traded or some other currency if currency conversion is enabled. It is displayed in the Symbol Info dialog and on the price axes.

## original_unit_id

A unique identifier of a unit in which the instrument is traded.

## unit_id

A unique identifier of a unit in which the instrument is traded or some other identifier if unit conversion is enabled. It is displayed on the price axes.

## unit_conversion_types

Allowed unit conversion group names. See also [units](JS-Api#units).
