# Animated

The `Animated` library is designed to make animations fluid, powerful, and painless to build and maintain. `Animated` focuses on declarative relationships between inputs and outputs, configurable transforms in between, and `start`/`stop` methods to control time-based animation execution.

The core workflow for creating an animation is to create an `Animated.Value`, hook it up to one or more style attributes of an animated component, and then drive updates via animations using `Animated.timing()`.

- Function Component
- Class Component

> Don't modify the animated value directly. You can use the [`useRef` Hook](https://reactjs.org/docs/hooks-reference.html#useref) to return a mutable ref object. This ref object's `current` property is initialized as the given argument and persists throughout the component lifecycle.

## Example[](https://reactnative.dev/docs/animated#example)

The following example contains a `View` which will fade in and fade out based on the animated value `fadeAnim`

- Function Component
- Class Component

<iframe loading="lazy" src="https://snack.expo.dev/embedded?iframeId=t3yumwxupm&amp;preview=true&amp;platform=web&amp;supportedPlatforms=ios,android,web&amp;name=Animated&amp;description=Example%20usage&amp;theme=light&amp;waitForData=true" height="100%" width="100%" frameborder="0" data-snack-iframe="true" style="box-sizing: border-box; border: 0px; color-scheme: auto; display: block;"></iframe>

Refer to the [Animations](https://reactnative.dev/docs/animations#animated-api) guide to see additional examples of `Animated` in action.

## Overview[](https://reactnative.dev/docs/animated#overview)

There are two value types you can use with `Animated`:

- [`Animated.Value()`](https://reactnative.dev/docs/animated#value) for single values
- [`Animated.ValueXY()`](https://reactnative.dev/docs/animated#valuexy) for vectors

`Animated.Value` can bind to style properties or other props, and can be interpolated as well. A single `Animated.Value` can drive any number of properties.

### Configuring animations[](https://reactnative.dev/docs/animated#configuring-animations)

`Animated` provides three types of animation types. Each animation type provides a particular animation curve that controls how your values animate from their initial value to the final value:

- [`Animated.decay()`](https://reactnative.dev/docs/animated#decay) starts with an initial velocity and gradually slows to a stop.
- [`Animated.spring()`](https://reactnative.dev/docs/animated#spring) provides a basic spring physics model.
- [`Animated.timing()`](https://reactnative.dev/docs/animated#timing) animates a value over time using [easing functions](https://reactnative.dev/docs/easing).

In most cases, you will be using `timing()`. By default, it uses a symmetric easeInOut curve that conveys the gradual acceleration of an object to full speed and concludes by gradually decelerating to a stop.

### Working with animations[](https://reactnative.dev/docs/animated#working-with-animations)

Animations are started by calling `start()` on your animation. `start()` takes a completion callback that will be called when the animation is done. If the animation finished running normally, the completion callback will be invoked with `{finished: true}`. If the animation is done because `stop()` was called on it before it could finish (e.g. because it was interrupted by a gesture or another animation), then it will receive `{finished: false}`.

```jsx
Animated.timing({}).start(({ finished }) => {
  /* completion callback */
});
```

Copy

### Using the native driver[](https://reactnative.dev/docs/animated#using-the-native-driver)

By using the native driver, we send everything about the animation to native before starting the animation, allowing native code to perform the animation on the UI thread without having to go through the bridge on every frame. Once the animation has started, the JS thread can be blocked without affecting the animation.

You can use the native driver by specifying `useNativeDriver: true` in your animation configuration. See the [Animations](https://reactnative.dev/docs/animations#using-the-native-driver) guide to learn more.

### Animatable components[](https://reactnative.dev/docs/animated#animatable-components)

Only animatable components can be animated. These unique components do the magic of binding the animated values to the properties, and do targeted native updates to avoid the cost of the React render and reconciliation process on every frame. They also handle cleanup on unmount so they are safe by default.

- [`createAnimatedComponent()`](https://reactnative.dev/docs/animated#createanimatedcomponent) can be used to make a component animatable.

`Animated` exports the following animatable components using the above wrapper:

- `Animated.Image`
- `Animated.ScrollView`
- `Animated.Text`
- `Animated.View`
- `Animated.FlatList`
- `Animated.SectionList`

### Composing animations[](https://reactnative.dev/docs/animated#composing-animations)

Animations can also be combined in complex ways using composition functions:

- [`Animated.delay()`](https://reactnative.dev/docs/animated#delay) starts an animation after a given delay.
- [`Animated.parallel()`](https://reactnative.dev/docs/animated#parallel) starts a number of animations at the same time.
- [`Animated.sequence()`](https://reactnative.dev/docs/animated#sequence) starts the animations in order, waiting for each to complete before starting the next.
- [`Animated.stagger()`](https://reactnative.dev/docs/animated#stagger) starts animations in order and in parallel, but with successive delays.

Animations can also be chained together by setting the `toValue` of one animation to be another `Animated.Value`. See [Tracking dynamic values](https://reactnative.dev/docs/animations#tracking-dynamic-values) in the Animations guide.

By default, if one animation is stopped or interrupted, then all other animations in the group are also stopped.

### Combining animated values[](https://reactnative.dev/docs/animated#combining-animated-values)

You can combine two animated values via addition, subtraction, multiplication, division, or modulo to make a new animated value:

- [`Animated.add()`](https://reactnative.dev/docs/animated#add)
- [`Animated.subtract()`](https://reactnative.dev/docs/animated#subtract)
- [`Animated.divide()`](https://reactnative.dev/docs/animated#divide)
- [`Animated.modulo()`](https://reactnative.dev/docs/animated#modulo)
- [`Animated.multiply()`](https://reactnative.dev/docs/animated#multiply)

### Interpolation[](https://reactnative.dev/docs/animated#interpolation)

The `interpolate()` function allows input ranges to map to different output ranges. By default, it will extrapolate the curve beyond the ranges given, but you can also have it clamp the output value. It uses linear interpolation by default but also supports easing functions.

- [`interpolate()`](https://reactnative.dev/docs/animated#interpolate)

Read more about interpolation in the [Animation](https://reactnative.dev/docs/animations#interpolation) guide.

### Handling gestures and other events[](https://reactnative.dev/docs/animated#handling-gestures-and-other-events)

Gestures, like panning or scrolling, and other events can map directly to animated values using `Animated.event()`. This is done with a structured map syntax so that values can be extracted from complex event objects. The first level is an array to allow mapping across multiple args, and that array contains nested objects.

- [`Animated.event()`](https://reactnative.dev/docs/animated#event)

For example, when working with horizontal scrolling gestures, you would do the following in order to map `event.nativeEvent.contentOffset.x` to `scrollX` (an `Animated.Value`):

```jsx
 onScroll={Animated.event(
   // scrollX = e.nativeEvent.contentOffset.x
   [{ nativeEvent: {
        contentOffset: {
          x: scrollX
        }
      }
    }]
 )}
```

Copy

------

# Reference

## Methods[](https://reactnative.dev/docs/animated#methods)

When the given value is a ValueXY instead of a Value, each config option may be a vector of the form `{x: ..., y: ...}` instead of a scalar.

### `decay()`[](https://reactnative.dev/docs/animated#decay)

```jsx
static decay(value, config)
```

Copy

Animates a value from an initial velocity to zero based on a decay coefficient.

Config is an object that may have the following options:

- `velocity`: Initial velocity. Required.
- `deceleration`: Rate of decay. Default 0.997.
- `isInteraction`: Whether or not this animation creates an "interaction handle" on the `InteractionManager`. Default true.
- `useNativeDriver`: Uses the native driver when true. Default false.

------

### `timing()`[](https://reactnative.dev/docs/animated#timing)

```jsx
static timing(value, config)
```

Copy

Animates a value along a timed easing curve. The [`Easing`](https://reactnative.dev/docs/easing) module has tons of predefined curves, or you can use your own function.

Config is an object that may have the following options:

- `duration`: Length of animation (milliseconds). Default 500.
- `easing`: Easing function to define curve. Default is `Easing.inOut(Easing.ease)`.
- `delay`: Start the animation after delay (milliseconds). Default 0.
- `isInteraction`: Whether or not this animation creates an "interaction handle" on the `InteractionManager`. Default true.
- `useNativeDriver`: Uses the native driver when true. Default false.

------

### `spring()`[](https://reactnative.dev/docs/animated#spring)

```jsx
static spring(value, config)
```

Copy

Animates a value according to an analytical spring model based on [damped harmonic oscillation](https://en.wikipedia.org/wiki/Harmonic_oscillator#Damped_harmonic_oscillator). Tracks velocity state to create fluid motions as the `toValue` updates, and can be chained together.

Config is an object that may have the following options.

Note that you can only define one of bounciness/speed, tension/friction, or stiffness/damping/mass, but not more than one:

The friction/tension or bounciness/speed options match the spring model in [`Facebook Pop`](https://github.com/facebook/pop), [Rebound](https://github.com/facebookarchive/rebound), and [Origami](http://origami.design/).

- `friction`: Controls "bounciness"/overshoot. Default 7.
- `tension`: Controls speed. Default 40.
- `speed`: Controls speed of the animation. Default 12.
- `bounciness`: Controls bounciness. Default 8.

Specifying stiffness/damping/mass as parameters makes `Animated.spring` use an analytical spring model based on the motion equations of a [damped harmonic oscillator](https://en.wikipedia.org/wiki/Harmonic_oscillator#Damped_harmonic_oscillator). This behavior is slightly more precise and faithful to the physics behind spring dynamics, and closely mimics the implementation in iOS's CASpringAnimation.

- `stiffness`: The spring stiffness coefficient. Default 100.
- `damping`: Defines how the spring’s motion should be damped due to the forces of friction. Default 10.
- `mass`: The mass of the object attached to the end of the spring. Default 1.

Other configuration options are as follows:

- `velocity`: The initial velocity of the object attached to the spring. Default 0 (object is at rest).
- `overshootClamping`: Boolean indicating whether the spring should be clamped and not bounce. Default false.
- `restDisplacementThreshold`: The threshold of displacement from rest below which the spring should be considered at rest. Default 0.001.
- `restSpeedThreshold`: The speed at which the spring should be considered at rest in pixels per second. Default 0.001.
- `delay`: Start the animation after delay (milliseconds). Default 0.
- `isInteraction`: Whether or not this animation creates an "interaction handle" on the `InteractionManager`. Default true.
- `useNativeDriver`: Uses the native driver when true. Default false.

------

### `add()`[](https://reactnative.dev/docs/animated#add)

```jsx
static add(a, b)
```

Copy

Creates a new Animated value composed from two Animated values added together.

------

### `subtract()`[](https://reactnative.dev/docs/animated#subtract)

```jsx
static subtract(a, b)
```

Copy

Creates a new Animated value composed by subtracting the second Animated value from the first Animated value.

------

### `divide()`[](https://reactnative.dev/docs/animated#divide)

```jsx
static divide(a, b)
```

Copy

Creates a new Animated value composed by dividing the first Animated value by the second Animated value.

------

### `multiply()`[](https://reactnative.dev/docs/animated#multiply)

```jsx
static multiply(a, b)
```

Copy

Creates a new Animated value composed from two Animated values multiplied together.

------

### `modulo()`[](https://reactnative.dev/docs/animated#modulo)

```jsx
static modulo(a, modulus)
```

Copy

Creates a new Animated value that is the (non-negative) modulo of the provided Animated value

------

### `diffClamp()`[](https://reactnative.dev/docs/animated#diffclamp)

```jsx
static diffClamp(a, min, max)
```

Copy

Create a new Animated value that is limited between 2 values. It uses the difference between the last value so even if the value is far from the bounds it will start changing when the value starts getting closer again. (`value = clamp(value + diff, min, max)`).

This is useful with scroll events, for example, to show the navbar when scrolling up and to hide it when scrolling down.

------

### `delay()`[](https://reactnative.dev/docs/animated#delay)

```jsx
static delay(time)
```

Copy

Starts an animation after the given delay.

------

### `sequence()`[](https://reactnative.dev/docs/animated#sequence)

```jsx
static sequence(animations)
```

Copy

Starts an array of animations in order, waiting for each to complete before starting the next. If the current running animation is stopped, no following animations will be started.

------

### `parallel()`[](https://reactnative.dev/docs/animated#parallel)

```jsx
static parallel(animations, config?)
```

Copy

Starts an array of animations all at the same time. By default, if one of the animations is stopped, they will all be stopped. You can override this with the `stopTogether` flag.

------

### `stagger()`[](https://reactnative.dev/docs/animated#stagger)

```jsx
static stagger(time, animations)
```

Copy

Array of animations may run in parallel (overlap), but are started in sequence with successive delays. Nice for doing trailing effects.

------

### `loop()`[](https://reactnative.dev/docs/animated#loop)

```jsx
static loop(animation, config?)
```

Copy

Loops a given animation continuously, so that each time it reaches the end, it resets and begins again from the start. Will loop without blocking the JS thread if the child animation is set to `useNativeDriver: true`. In addition, loops can prevent `VirtualizedList`-based components from rendering more rows while the animation is running. You can pass `isInteraction: false` in the child animation config to fix this.

Config is an object that may have the following options:

- `iterations`: Number of times the animation should loop. Default `-1` (infinite).

------

### `event()`[](https://reactnative.dev/docs/animated#event)

```jsx
static event(argMapping, config?)
```

Copy

Takes an array of mappings and extracts values from each arg accordingly, then calls `setValue` on the mapped outputs. e.g.

```jsx
 onScroll={Animated.event(
   [{nativeEvent: {contentOffset: {x: this._scrollX}}}],
   {listener: (event) => console.log(event)}, // Optional async listener
 )}
 ...
 onPanResponderMove: Animated.event([
   null,                // raw event arg ignored
   {dx: this._panX}],    // gestureState arg
{listener: (event, gestureState) => console.log(event, gestureState)}, // Optional async listener
 ),
```

Copy

Config is an object that may have the following options:

- `listener`: Optional async listener.
- `useNativeDriver`: Uses the native driver when true. Default false.

------

### `forkEvent()`[](https://reactnative.dev/docs/animated#forkevent)

```jsx
static forkEvent(event, listener)
```

Copy

Advanced imperative API for snooping on animated events that are passed in through props. It permits to add a new javascript listener to an existing `AnimatedEvent`. If `animatedEvent` is a javascript listener, it will merge the 2 listeners into a single one, and if `animatedEvent` is null/undefined, it will assign the javascript listener directly. Use values directly where possible.

------

### `unforkEvent()`[](https://reactnative.dev/docs/animated#unforkevent)

```jsx
static unforkEvent(event, listener)
```

Copy

------

### `start()`[](https://reactnative.dev/docs/animated#start)

```jsx
static start([callback]: ?(result?: {finished: boolean}) => void)
```

Copy

Animations are started by calling start() on your animation. start() takes a completion callback that will be called when the animation is done or when the animation is done because stop() was called on it before it could finish.

**Parameters:**

| NAME     | TYPE                            | REQUIRED | DESCRIPTION                                                  |
| :------- | :------------------------------ | :------- | :----------------------------------------------------------- |
| callback | ?(result?: {finished: boolean}) | No       | Function that will be called after the animation finished running normally or when the animation is done because stop() was called on it before it could finish |

Start example with callback:

```jsx
Animated.timing({}).start(({ finished }) => {
  /* completion callback */
});
```

Copy

------

### `stop()`[](https://reactnative.dev/docs/animated#stop)

```jsx
static stop()
```

Copy

Stops any running animation.

------

### `reset()`[](https://reactnative.dev/docs/animated#reset)

```jsx
static reset()
```

Copy

Stops any running animation and resets the value to its original.

## Properties[](https://reactnative.dev/docs/animated#properties)

### `Value`[](https://reactnative.dev/docs/animated#value)

Standard value class for driving animations. Typically initialized with `new Animated.Value(0);`

You can read more about `Animated.Value` API on the separate [page](https://reactnative.dev/docs/animatedvalue).

------

### `ValueXY`[](https://reactnative.dev/docs/animated#valuexy)

2D value class for driving 2D animations, such as pan gestures.

You can read more about `Animated.ValueXY` API on the separate [page](https://reactnative.dev/docs/animatedvaluexy).

------

### `Interpolation`[](https://reactnative.dev/docs/animated#interpolation-1)

Exported to use the Interpolation type in flow.

------

### `Node`[](https://reactnative.dev/docs/animated#node)

Exported for ease of type checking. All animated values derive from this class.

------

### `createAnimatedComponent`[](https://reactnative.dev/docs/animated#createanimatedcomponent)

Make any React component Animatable. Used to create `Animated.View`, etc.

------

### `attachNativeEvent`[](https://reactnative.dev/docs/animated#attachnativeevent)

Imperative API to attach an animated value to an event on a view. Prefer using `Animated.event` with `useNativeDrive: true` if possible