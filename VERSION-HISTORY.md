
# Spritely version history

To download previous releases of Spritely, see [this repostory](https://github.com/artlogicmedialtd/spritely-archive).

## Version 0.6.8

* Fixed an incorrect intialization of $._spritely.instances that was causing the
  plugin to break.

## Version 0.6.7

* Removed the erroneous 'stop_after' key from the default options object.
* The synonymous 'play_frames' option has now been fixed, and can be used to play only a set number of frames of animation. Note that this option only applies to sprite animations. It is used like so:

```javascript
    $('#sprite').sprite({
        no_of_frames: 5,
        fps: 12,
        play_frames: 36 // Play through the animation three times and then stop.
    });
```

* Fixed the 'do_once' option, which plays through the animation one time and then stops on the last frame (and works for both sprite and panning animations):

```javascript
    $('#sprite').sprite({
        no_of_frames: 5,
        fps: 12,
        do_once: true
    });
```

## Version 0.6.6

* Fix an issue that causes the background image position to reset along the panned axis before animation begins.

## Version 0.6.5
* Better detection of 'background-position-x' CSS support
* Fix incorrect use of clearInterval in $.fn.destroy()

## Version 0.6.4
* Added metadata information for plugins.jquery.com, and incrimented the version number. (No actual changes to Spritely.)

## Version 0.6.3
* Fixed an issue that caused the background of panning sprites to disappear on some browsers. This affects at least Firefox on 64-bit Windows 7. Offset values are now reduced to the smallest (correct) value possible on each update.

## Version 0.6.2
* Removed reliance on jQuery.browser; perform an actual feature check.

## Version 0.6.1
* Added some refinements from [Gary Hussey](http://bossninja.com/). Thanks Gary.
* Spritely now correctly clears timeouts/intervals when destroying sprites.
* Added a goToFrame() method so you can set the current frame at any point.
* Fixed the .spStop method where the 'last FPS' value was not being set, and the user specified FPS being ignore when .spStart was called.

## Version 0.6
* Added events to the .sprite() method: on_first_frame, on_last_frame, on_frame:

```javascript
    $('#sprite').sprite({
        fps: 9,
        no_of_frames: 24,
        on_first_frame: function(obj) {
            obj.spState(1); // change to state 1 (first row) on frame 1
        },
        on_last_frame: function(obj) {
            obj.spStop(); // stop the animation on the last frame
        },
        on_frame: {
            8: function(obj) {
                obj.spState(2); // change to state 2 (row 2) on frame 8
            },
            16: function(obj) {
                obj.spState(3); // change to state 3 (row 3) on frame 16
            }
        }
    });
```
* Added start_at_frame:

```javascript
    $('#sprite').sprite({fps: 9, no_of_frames: 24, start_at_frame: 8});
```

## Version 0.5
* Added a destroy() method which will stop the element's sprite behaviour, without actually removing the element. Example:

```javascript
    $('#my_sprite').destroy()
```

## Version 0.4
* Add up/down for 'pan' method.
* Added 'dir' option for Sprites. This means a Sprite can be played in reverse.
* Removed alert message regarding jQuery.draggable (now uses console.log, if available)

## Version 0.3b
* Added lockTo method for locking sprites to background images.

```javascript
    $('#sprite').lockTo('#background, {
        'left': 380,
        'top': -60,
        'bg_img_width': 1110
    });
```

## Version 0.2.1
* Animate function will stop cycling after play_frames has completed

## Version 0.2 beta
* Added isDraggable method (requires jquery-ui)

```javascript
    $('#sprite').sprite().isDraggable({start: null, stop: function() {
        alert('Ouch! You dropped me!');
    });
```
* Sprites may be set to play a limited number of frames when instantiated, e.g.

```javascript
    $('#sprite').sprite({fps: 9, no_of_frames: 3, play_frames: 30})
```
* Sprite speed may be controlled at any point by setting the frames-per-second

```javascript
    $('#sprite').fps(20);
```
* Sprites with multiple rows of frames may have there 'state' changed, e.g. to make the second row of frames
  active, use: $('#sprite').spState(2); - to return to the first row, use

```javascript
    $('#sprite').spState(1);
```
* Background element speed may be controlled at any point with .spSpeed(), e.g.

```javascript
    $('#bg1').spSpeed(10)
```
* Background elements may be set to a depth where 100 is the viewer (up close) and 0 is the horizon, e.g.:

```javascript
    $('#bg1').pan({fps: 30, speed: 2, dir: 'left', depth: 30});
    $('#bg2').pan({fps: 30, speed: 3, dir: 'left', depth: 70});
```
* Relative speed of backgrounds may now be set in a single action with

```javascript
    // Make elements closer to the horizon (lower depths) move slower than closer elements (higher depths)
    $('#bg1, #bg2').spRelSpeed(20);
```
