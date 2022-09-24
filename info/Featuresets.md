`Feature` or `featureset` is a string literal that can be used to change the functionality of the chart. There are simple (atomic) and complex (composite) features. Composite feature consists of simple features. Disabling composite feature disables all of its simple parts as well. Supported features are listed below.

Please note that the leading `-` characters are not part of the featureset name in the table below.

### Visibility of controls and other visual elements

[**Interactive Map of Featuresets**](https://charting-library.tradingview-widget.com/featuresets.html)

| ID                                      | Default State | Library Version | Description                                                |
|-----------------------------------------|---------------|-----------------|------------------------------------------------------------|
| **header_widget**                       | on            |                 |                                                            |
| - header_widget_dom_node                | on            |                 | Disabling this feature hides the header widget DOM element |
| - header_symbol_search                  | on            |                 |                                                            |
| - symbol_search_hot_key                 | on            |       1.9       | Symbol search by pressing any key                          |
| - header_resolutions                    | on            |                 |                                                            |
| - - header_interval_dialog_button       | on            |                 |                                                            |
| - - - show_interval_dialog_on_key_press | on            |                 |                                                            |
| - header_chart_type                     | on            |                 |                                                            |
| - header_settings                       | on            |                 | Relates to Chart Properties button                         |
| - header_indicators                     | on            |                 |                                                            |
| - header_compare                        | on            |                 |                                                            |
| - header_undo_redo                      | on            |                 |                                                            |
| - header_screenshot                     | on            |                 |                                                            |
| - header_fullscreen_button              | on            |                 |                                                            |
| border_around_the_chart                 | on            |                 |                                                            |
| header_saveload                         | on            |                 | Hides save/load buttons (the feature is not part of `header_widget` featureset)                    |
| left_toolbar                            | on            |                 |                                                            |
| control_bar                             | on            |                 | Relates to the navigation buttons at the bottom of the chart            |
| timeframes_toolbar                      | on            |                 |                                                            |
| legend_widget                           | on            |      1.15       | Disabling this feature hides the legend widget             |
| display_legend_on_all_charts            | off           |       18        | Display legend on all diagrams regardless of crosshair synchronization |
| object_tree_legend_mode                 | on            |       18        | Display object tree button in the legend at a small width  |
| **edit_buttons_in_legend**              | on            |                 |                                                            |
| - show_hide_button_in_legend            | on            |       1.7       |                                                            |
| - format_button_in_legend               | on            |       1.7       |                                                            |
| - delete_button_in_legend               | on            |       1.7       |                                                            |
| **context_menus**                       | on            |                 |                                                            |
| - pane_context_menu                     | on            |                 |                                                            |
| - scales_context_menu                   | on            |                 |                                                            |
| - legend_context_menu                   | on            |                 |                                                            |
| main_series_scale_menu                  | on            |       1.7       | Displays the settings button in the bottom right corner of the chart |
| chart_crosshair_menu                    | on (terminal) | 1.7             | Enables the "plus" button on the price scale for quick trading |
| display_market_status                   | on            |                 |                                                            |
| remove_library_container_border         | on            |                 |                                           |
| property_pages                          | on            | 1.11            | Disables all property pages                |
| show_chart_property_page                | on            | 1.6             | Turning this feature off disables Properties        |
| chart_property_page_scales              | on            |                 |                                           |
| chart_property_page_trading             | on            |                 | This feature is for the Trading Terminal only           |
| chart_property_page_right_margin_editor | on            | 1.15            | Shows the right margin editor in the setting dialog |
| countdown                               | on            | 1.4             | Displays a countdown label on a price scale         |
| dont_show_boolean_study_arguments       | off           | 1.4             | Hides true/false study arguments |
| hide_last_na_study_output               | off           | 1.4             | Hides last n/a study output data        |
| symbol_info                             | on            | 1.5             | Enables the symbol info dialog                 |
| timezone_menu                           | on            | 1.5             | Disables timezone context menu    |
| snapshot_trading_drawings               | off           | 1.6             | Includes orders/positions/executions in the screenshot |
| source_selection_markers                | on            | 1.11            | Disables selection markers for series and indicators |
| go_to_date                              | on            | 1.11            | Allows you to jump to a particular bar using 'Go to' dialog |
| adaptive_logo                           | on            | 1.11            | Allows you to hide 'charts by TradingView' text on small-screen devices |
| show_dom_first_time                     | off           | 1.12            | Shows DOM panel when a user opens the Chart for the first time |
| hide_left_toolbar_by_default            | off           | 1.12            | Hides left toolbar when a user opens the Chart for the first time |
| chart_style_hilo                        | off           | 1.15            | Adds Hi-Lo option to chart style controls |
| pricescale_currency                     | off           | 16              | Displays the currency in which the instrument is traded on the price axes |
| pricescale_unit                         | off           | 19              | Displays the unit in which the instrument is traded on the price axes |
| scales_date_format                      | on            | 17              | Displays Date Format selector in Chart Settings |
| popup_hints                             | on            | 17              | Displays popup hints about possible mouse/shortcuts/UI actions |
| save_shortcut                           | on            |       18        | Enables the save shortcut |
| show_right_widgets_panel_by_default     | on            |       18        | Opens right widget toolbar on first launch |
| show_object_tree                        | on            |       18        | Shows the object tree button in the left or right panel depending on the product and configuration |
| show_spread_operators                   | off           |       20        | Shows the spread operators in the Symbol Search dialog |
| hide_exponentiation_spread_operator     | off           |       20        | Hide exponentiation spread operator (^) in the Symbol Search dialog |
| hide_reciprocal_spread_operator         | off           |       20        | Hide reciprocal spread operator (1/x) in the Symbol Search dialog |
| compare_symbol_search_spread_operators  | off           |       20        | Shows the spread operators in the Compare Search dialog - needs to be used in conjuction to show_spread_operators|
| studies_symbol_search_spread_operators  | off           |       20        | Shows the spread operators for Studies - needs to be used in conjuction to show_spread_operators|
| hide_resolution_in_legend               | off           |       20        | Hide the interval (D, 2D, W, M, etc.) in the chart legend and the data window|
| hide_unresolved_symbols_in_legend       | off           |       21        | Hide unresolved symbols in the chart legend and the data window|
| show_zoom_and_move_buttons_on_touch     | off           |       21        | On touch device show the zoom and move buttons at the bottom of the chart|
| hide_main_series_symbol_from_indicator_legend | on           |       22        | Hide the optional symbol input value from the indicator's legend if 'Main chart symbol' option is selected |
| hide_price_scale_global_last_bar_value  | off           |       23        | Hide the global last price label on price scale if last bar is outside of visible range |
| show_average_close_price_line_and_label | off           |       23        | Hide the visibility settings of the label and the average close price line |
| hide_image_invalid_symbol               | off           |       23        | Hide image shown to illustrate symbol is invalid |
| hide_object_tree_and_price_scale_exchange_label | off | 23 | Show/Hide the exchange label from the displayed label |
| use_na_string_for_not_available_values                   | off           |       24        | Show a literal "n/a" for not available values instead of "∅". |

### Elements placement

| ID                           | Default State | Library Version | Description                                                        |
|------------------------------|---------------|-----------------|--------------------------------------------------------------------|
| move_logo_to_main_pane       | off           |                 | Places the logo on the main series pane instead of the bottom pane |

### Behavior

| ID  | Default State | Library Version | Description
|-------|---------------|-----------------|------------
| **use_localstorage_for_settings** | on |                 | Allows storing all properties (including favorites) to the localstorage
| - items_favoriting | on |                 | Disabling this feature hides "Favorite this item" icon for Drawings and Intervals
| - save_chart_properties_to_local_storage | on |                 |  Can be disabled to forbid storing chart properties to the localstorage while allowing to save other properties. The other properties are favorites in the Charting Library and Watchlist symbols and some panels states in the Trading Terminal.
| create_volume_indicator_by_default | on |                 |
| create_volume_indicator_by_default_once | on |                  |
| volume_force_overlay | on |                 | Places Volume indicator on the same pane with the main series
| right_bar_stays_on_scroll | on |                 | Determines the behavior of Zoom feature: bar under the mouse cursor stays in the same place if this feature is disabled
| constraint_dialogs_movement | on |                 | Keeps the dialogs within the chart
| charting_library_debug_mode | off |                 | Enables logs
| side_toolbar_in_fullscreen_mode | off |                 | This enables Drawings Toolbar in the fullscreen mode
| header_in_fullscreen_mode | off |    16         | Enables header widget DOM element in the fullscreen mode
| disable_resolution_rebuild    | off   |                 | Shows bar time exactly as provided by the data feed with no adjustments.
| chart_scroll                  | on    |   1.10          | Allows chart scrolling
| chart_zoom                    | on    |   1.10          | Allows chart zooming
| horz_touch_drag_scroll        | on    |   16          | If enabled, the chart handles horizontal pointer movements on touch screens. In this case the webpage is not scrolled. If disabled, the webpage is scrolled instead. Keep in mind that if the user starts scrolling the chart vertically or horizontally, scrolling is continued in any direction until the user releases the finger.
| vert_touch_drag_scroll        | on    |   16          | If enabled, the chart handles vertical pointer movements on touch screens. In this case the webpage is not scrolled. If disabled, the webpage is scrolled instead. Keep in mind that if the user starts scrolling the chart vertically or horizontally, scrolling is continued in any direction until the user releases the finger.
| mouse_wheel_scroll            | on    |   16          | If enabled, chart scrolling with horizontal mouse wheel is enabled.
| pressed_mouse_move_scroll     | on    |   16          | If enabled, chart scrolling with left mouse button pressed is allowed.
| mouse_wheel_scale             | on    |   16          | If enabled, series scaling with a mouse wheel is enabled.
| pinch_scale                   | on    |   16          | If enabled, series scaling with pinch/zoom gestures (this option is supported on touch devices) is enabled.
| axis_pressed_mouse_move_scale | on    |   16          | If enabled, axis scaling with left mouse button pressed is allowed.
| low_density_bars              | off   |   1.15          | Allows zooming in to show up to one bar in the viewport
| uppercase_instrument_names    | on    | 1.12            | Disabling this feature allows a user to enter case-sensitive symbols
| no_min_chart_width            | off   | 1.14            | Disables minimum chart width limitation
| fix_left_edge                 | off   | 1.14            | Prevents scrolling to the left of the first historical bar
| lock_visible_time_range_on_resize | off   | 1.14        | Prevents changing visible time area on chart resizing
| shift_visible_range_on_new_bar  | on   | 1.15        | If disabled, adding a new bar zooms out the chart preserving the first visible point. Otherwise the chart is scrolled one point to the left when a new bar comes.
| custom_resolutions            | off   | 1.15            | If enabled, there is a possibility to add custom resolutions
| end_of_period_timescale_marks | off | 16 | Toggles the timeline marks to display the bar's end time
| cropped_tick_marks | on | 16 | If disabled, partially visible price labels on price axis will be hidden
| study_overlay_compare_legend_option | off | 20 | Applies symbol display mode (ticker/description) to overlay/compare studies in the status line
| study_symbol_ticker_description | off | 20 | Applies symbol display mode (ticker/description) to indicator inputs in the status line
| auto_enable_symbol_labels  | on | 20 | Displays Symbol Name Label when comparing Symbols
| insert_indicator_dialog_shortcut  | on | 21 | Enables insert indicator dialog shortcut (/)
| two_character_bar_marks_labels | off | 22 | Display at most two characters in bar marks. The default behaviour is to only display one character.
| confirm_overwrite_if_chart_layout_with_name_exists | off | 23 | By default many chart layouts can be saved with the same name. If this feature is enabled then the library will prompt to confirm overwriting chart layouts with the same name when saving, renaming, or cloning ("Save as").

### Important features

| ID | Default State | Library Version | Description
|-------|---------------|-----------------|------------
| study_templates | off | |
| datasource_copypaste | on | | Enables copying of drawings and studies
| seconds_resolution| off | 1.4 | Enables the support of resolutions that start from 1 second
| tick_resolution | off | 18 | Enables the support of tick resolution
| secondary_series_extend_time_scale | off | 20 | Enables a feature to allow an additional series to extend the time scale

## :chart: Trading Terminal

| ID | Default State | Terminal Version | Description
|-------|---------------|------------------|------------
| support_multicharts | on | | Enables context menu actions (Clone, Sync) related to Multiple Chart Layout
| header_layouttoggle | on | | Shows the Select Layout button in the header
| add_to_watchlist | on | 1.9 | Enables "Add symbol to Watchlist" item in the menu
| open_account_manager | on | 1.11 | Keeps the Account Manager opened by default
| trading_notifications | on | 1.11 | Shows trading notifications on the chart
| multiple_watchlists | on | 1.12 | Enables creating of multiple watchlists
| show_trading_notifications_history | on | 1.13 | Enables the Notifications Log tab in the bottom panel
| always_pass_called_order_to_modify | off | 1.15 | If a bracket order is modified, the terminal passes its parent order to `modifyOrder`. The featureset disables this behavior.
| drawing_templates                      | on  | 17  | Enables Drawing Templates on Drawing toolbar
| trading_account_manager | on | 17 | Shows the Account Manager Widget
| right_toolbar | on | 17 | Shows the right buttons toolbar
| order_panel | on | 17 | Shows the Order Panel
| order_info | on | 17 | Shows the Order info section in the Order dialog
| **buy_sell_buttons** | on | 18 | Shows the Buy/Sell Buttons in Legend
| - broker_button | on | 19 | Shows the Broker Button in Legend
| show_order_panel_on_start | off | 17 | Order Panel is visible when the chart opens
| order_panel_close_button | on | 17 | Shows close Order Panel button
| order_panel_undock | on | 17 | Shows the Undock button in the Order Panel Settings
| chart_hide_close_position_button | off | 22 | Hide the close button for position
| chart_hide_close_order_button | off | 22 | Hide the close button for order
| watchlist_import_export | on | | Enables watchlist export and import
| dom_widget | off | 22 | Enables DOM widget visibility
| keep_object_tree_widget_in_right_toolbar | off | 23 | Keeps Object Tree widget in the right toolbar
| show_last_price_and_change_only_in_series_legend | off | 23 | Show only the last price and change values in the main series legend.
