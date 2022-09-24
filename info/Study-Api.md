## Study API

### isUserEditEnabled()

Returns `true` if a user is able to remove/change/hide the study.

### setUserEditEnabled(enabled)

1. `enabled` - `true` or `false`

Enables or disables removing/changing/hiding a study by the user.

### getInputsInfo()

Returns the information about all the inputs - an array of [StudyInputInfo](#studyinputinfo) objects.

### getInputValues()

Returns values of study inputs - an array of [StudyInputValueItem](#studyinputvalueitem) objects.

### setInputValues(inputs)

1. `inputs` should be an array of [StudyInputValueItem](#studyinputvalueitem) objects.

Sets input values for a study. It may contain only some of the inputs that you wish to change.

### getStyleInfo()

Returns the information about all the properties contained in Style tab - an array of [StudyStyleInfo](#studystyleinfo) objects.

### getStyleValues()

Returns values of style properties - an array of [StudyStyleValues](#studystylevalues) objects.

### mergeUp()

Merges the study up (if possible).

### mergeDown()

Merges the study down (if possible).

### unmergeUp()

Unmerges the study up (if possible).

### unmergeDown()

Unmerges the study down (if possible).

### changePriceScale(priceScale)

1. `priceScale` should be a string with one of the following values:
    * `"new-left"` - attach the study to the new left price scale
    * `"new-right"` - attach the study to the new right price scale
    * `"no-scale"` - do not attach the study to any price scale if there are another price scales on the pane. The study will be added in 'No Scale' mode
    * `"as-series"` - attach the study to the price scale where the main series is attached (it is only applicable if the study and the main series are located on the same pane)
    * `entityId` - attach the study to the same price axis as a study with a corresponding `entityId`

Changes the price scale of the study. See [here](Panes-And-Scales-Behavior) more information about panes and scales behavior in relation to studies.

### isVisible()

Returns `true` if the study is visible.

### setVisible(value)

1. `value` - `true` or `false`

Shows/hides the study.

### bringToFront()

Places the study on top of all other chart objects.

### sendToBack()

Places the study behind all other chart objects.

### applyOverrides(overrides)

1. `overrides` - new [overrides](Studies-Overrides) for the study

Applies `overrides` to the study.

Note: `overrides` object keys don’t need to start with the study name. The key is applied to a particular study.
For example, you should use `style` instead of `Overlay.style` to override the current style of the Overlay study.

### onDataLoaded

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when the study data is loaded. You can also use the same object to unsubscribe from the event.

Example:

```javascript
studyApi.onDataLoaded().subscribe(
    null,
    () => console.log('Study data is loaded'),
    true
);
```

### onStudyError

You can subscribe using [Subscription](Subscription) object returned by this function to be notified when the study received an error. You can also use the same object to unsubscribe from the event.

Example:

```javascript
studyApi.onStudyError().subscribe(
    null,
    () => console.log('Study error'),
    true
);
```

### :chart: applyToEntireLayout()

Copies the study to all charts of the layout.

## Primitive types

### StudyInputInfo

An object with the following keys:

* `id` - input ID of the study
* `name` - name of the input
* `type` - type of the input
* `localizedName` - name of the input translated to the current language

### StudyInputValueItem

An object with the following keys:

* `id` - input ID of the study
* `value` - value of the input

### StudyStyleInfo

An object with the following keys (short decription). More details can be found [here](Custom-Studies-Metainfo):

* `defaults` - optional property - an object containing settings that are applied when user clicks `Apply Defaults`
* `plots` - optional property - an array with study plots info
* `styles` - optional property - an object with `plot id` as keys and style info as values
* `bands` - optional property - an array with study band info objects
* `filledAreas` - optional property - an array of filled areas info. Filled area is a special object, which allows coloring an area between two plots
* `palettes` - optional property - an object with the definitions of palletes that are used in `plots` and `defaults`

### StudyStyleValues

Same object as [StudyStyleInfo](#studystyleinfo) without the `default` property.
