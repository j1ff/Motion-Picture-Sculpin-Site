---
layout: default
title: Parameters

---
# Parameters

------
## [#](#animationProgress)<a name="animationProgress"></a>Animation Progress Control

These parameters determine how and when the animation progresses from beginning to end.

#### [#](#steps)<a name="steps"></a>steps `*required`
* The number of steps in the animation.
~~~javascript
// No default value.
// Enter the number of frames your sprite has.
~~~

#### [#](#focalPoint)<a name="focalPoint"></a>focalPoint
* A numeric value that returns the numerator in the animation progress equation.
* This value is returned every time that an `animationEvents` event is triggered.

~~~javascript
// Default value - The bottom of the window.
focalPoint: function() {
  return $(window).scrollTop() + $(window).height();
},
~~~

#### [#](#startLogic)<a name="startLogic"></a>startLogic
* The numeric value that should be considered the starting point of the animation.
* This value is returned every time a `calibrationEvents` event is triggered.

~~~javascript
// Default value - The height of the window.
startLogic: function() {
  return $(window).height()
},
~~~

#### [#](#endLogic)<a name="endLogic"></a>endLogic
* The numeric value that should be considered the end point of the animation.
* This value is returned every time a `calibrationEvents` event is triggered.

~~~javascript
// Default value - The height of the page. Subtract 1px because it's helpful for letting an animation
// fully complete.
endLogic: function() {
  return $('html').height() - 1;
},
~~~

-----

## [#](#animation)<a name="animation"></a>Animation Behavior
Basic behavior parameters

#### [#](#loop)<a name="loop"></a>loop
* If set to true, then the animation will loop around instead of end once the `focalPoint` passes the `endLogic`

~~~javascript
// Default value
loop: false,
~~~

#### [#](#hideOnComplete)<a name="hideOnComplete"></a>hideOnComplete
* If set to true, then use `hide()` on the element once the animation has completed.

~~~javascript
// Default value
hideOnComplete: true,
~~~

-----

## [#](#sprites)<a name="sprites"></a>Sprite Offset Handling
Set the underlying method for how the background offsets get handled when animating.

#### [#](#pictureMethod)<a name="pictureMethod"></a>pictureMethod
* Set whether the plugin should add/remove classes to the element, or set `background-position` directly using the `css()` method.
* Possible values:
  * class
  * offset

~~~javascript
// Default value
pictureMethod: class,
~~~

#### [#](#baseClass)<a name="baseClass"></a>baseClass
* **Only relevant if `pictureMethod` is set to 'class'**
* If set, the value will be added as a class to the element, with the current step appended to the value
* ex: a `baseClass` of `motionpicture` will turn into `motionpicture1`, and the numeric value at the end will change with each step.
* If set, then you probably want to make sure that individual `background-position` parameters are set for each class that could be used.

~~~javascript
// Default value
baseClass: 'motionpicture',
~~~


#### [#](#stepOffsets)<a name="stepOffsets"></a>stepOffsets ####
* **Only relevant if `pictureMethod` is set to 'offset'**
* An object containing objects which store parameters for individual offsets. Keyed by step number.
* Allows you to set offsets for individual steps.
* Only use `left` and `top` offsets.

~~~javascript
// Default value - no special offsets.
stepOffsets: {},
~~~

~~~javascript
// example - special offset for second step.
stepOffsets: {2: {left: 100, top: 400}},
~~~



#### [#](#dynamicPlacement)<a name="dynamicPlacement"></a>dynamicPlacement
* If enabled, any time an `animationEvents` event is triggered `startLogic` and `endLogic` will be re-run.
* This is really only neede if your `startLogic` and `endLogic` reference points are changing a lot (for example if this is happening inside of a parallaxy page element).

~~~javascript
// Default value
dynamicPlacement: false,
~~~

---------

## [#](#events)<a name="events"></a>Events
* Determines what causes the animation to progress, and reference values to be set.

#### [#](#animationEvents)<a name="animationEvents"></a>animationEvents
* An array containing at least one object defining what event should trigger the animation, and what the target for the event must be.
~~~javascript
// Default value - Trigger animation on scroll
animationEvents: [{'event': 'scroll', 'target': $(window)}],
~~~

#### [#](#calibrationEvents)<a name="calibrationEvents"></a>calibrationEvents
* An array containing at least one object defining what event(s) should allow `startLogic` and `endLogic`

~~~javascript
// Default value - Update parameters when the window is resized.
calibrationEvents: [{'event': 'resize', 'target': $(window)}],
~~~
