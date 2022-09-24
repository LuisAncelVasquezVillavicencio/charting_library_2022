WatchedValue object is returned by some methods of the [Trading Terminal](Trading-Terminal). Using this object you can get/set some value and be notified when the value is changed.

### value()

Returns current value.

### setValue(value)

Sets new value. Readonly WatchedValue object doesn't have this method.

### subscribe(callback, options)

1. `callback` is a function to be called when the value is changed
1. `options` is an object with the following properties:
    1. `once` - if it is set to true then the callback will be executed only once
    1. `callWithLast` - if it is set to true then the callback will be executed with the previous value (if available)

### unsubscribe(callback)

Use the same function that you used in the `subscribe` function to unsubscribe from the updates.

### when(callback)

A simplified version of subscription, with promise-like interface, generally for using with boolean-valued watched values

1. `callback` is a function to be called when the value became `true`. `once` and `callWithLast` are implicitly set to true.
