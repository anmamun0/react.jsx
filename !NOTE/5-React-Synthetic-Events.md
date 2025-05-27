React supports a rich set of synthetic events, similar to the DOM events in vanilla JavaScript. These are grouped into categories like:

## React Synthetic Event Categories & Lists


 
### 1.  Mouse Events
<h6> 
 
| Event Name       | Description                          |
|------------------|--------------------------------------|
| `onClick`        | Fires when an element is clicked     |
| `onDoubleClick`  | Fires on double click                |
| `onMouseDown`    | Mouse button is pressed              |
| `onMouseUp`      | Mouse button is released             |
| `onMouseEnter`   | Mouse enters the element             |
| `onMouseLeave`   | Mouse leaves the element             |
| `onMouseMove`    | Mouse is moved over the element      |
| `onMouseOver`    | Mouse enters element or children     |
| `onMouseOut`     | Mouse leaves element or children     |
| `onContextMenu`  | Fires on right-click (context menu)  |
</h6>

### 2. Keyboard Events
<h6> 
 
| Event Name        | Description                                           |
|-------------------|-------------------------------------------------------|
| `onKeyDown`       | Fires when a key is pressed                          |
| `onKeyUp`         | Fires when a key is released                         |
| `onKeyPress` ⚠️   | (Deprecated) Fires when a key is pressed and held — use `onKeyDown` instead |
</h6>

### 3. Form Events
<h6> 
 
| Event Name   | Description                                                        |
|--------------|--------------------------------------------------------------------|
| `onChange`   | Fires when input value changes                                     |
| `onInput`    | Fires on input event (similar to `onChange`, but lower-level)      |
| `onSubmit`   | Fires when a form is submitted                                     |
| `onReset`    | Fires when a form is reset                                         |
| `onInvalid`  | Fires when input fails HTML5 validation                            |
| `onFocus`    | Fires when an element gains focus                                  |
| `onBlur`     | Fires when an element loses focus                                  |
</h6>

### 4.  Focus Events
<h6> 
 
| Event Name | Description              |
|------------|--------------------------|
| `onFocus`  | Element gains focus      |
| `onBlur`   | Element loses focus      |
</h6>

### 5. Clipboard Events
<h6> 
 
| Event Name | Description          |
|------------|----------------------|
| `onCopy`   | Copy event triggered |
| `onCut`    | Cut event triggered  |
| `onPaste`  | Paste event triggered|
</h6>
 
###  6. Touch Events
<h6> 
 
| Event Name     | Description                     |
|----------------|---------------------------------|
| `onTouchStart` | Touch starts                   |
| `onTouchMove`  | Finger moves on screen         |
| `onTouchEnd`   | Touch ends                    |
| `onTouchCancel`| Touch interrupted (e.g., alert box) |
</h6>
 

### 7. Pointer Events (works with mouse, touch, pen, etc.)
<h6> 
 
| Event Name           | Description                         |
|----------------------|-----------------------------------|
| `onPointerDown`      | Pointer is pressed                 |
| `onPointerUp`        | Pointer is released                |
| `onPointerMove`      | Pointer is moved                  |
| `onPointerEnter`     | Pointer enters element             |
| `onPointerLeave`     | Pointer leaves element             |
| `onPointerOver`      | Pointer is over element or its children |
| `onPointerOut`       | Pointer leaves element or children |
| `onGotPointerCapture`| Pointer is captured                |
| `onLostPointerCapture`| Pointer capture lost             |
</h6>

### 🖼️ 8. UI Events
<h6> 
 
| Event Name | Description              |
|------------|--------------------------|
| `onScroll` | Element is scrolled      |
| `onResize` | Window is resized (only on window) |
</h6>

### 9. Media Events
<h6> 
 
| Event Name                                  | Description                          |
|---------------------------------------------|------------------------------------|
| `onPlay`, `onPause`, `onEnded`, `onVolumeChange`, `onTimeUpdate`, etc. | Media control events for `<video>` / `<audio>` |
 </h6>

### 10. Animation & Transition Events
<h6> 
 
| Event Name          | Description                |
|---------------------|----------------------------|
| `onAnimationStart`  | CSS animation starts       |
| `onAnimationEnd`    | CSS animation ends         |
| `onAnimationIteration` | CSS animation repeats    |
| `onTransitionEnd`   | CSS transition ends        |
 </h6>

### 11. Wheel Events
<h6> 
 
| Event Name | Description         |
|------------|---------------------|
| `onWheel`  | Mouse wheel scroll  |
 </h6>

###  12. Misc
<h6> 
 
| Event Name | Description                     |
|------------|---------------------------------|
| `onError`  | Error occurred (image, script, etc.) |
| `onLoad`   | Resource loaded (image, iframe, etc.) |
</h6>

Would you like a cheat sheet PDF for all of these events with code snippets?









Here's a full set of React examples showcasing usage of all event types. You can copy these into your React project to experiment and learn.

## Mouse Events
```jsx
<div
  onClick={() => alert('Clicked!')}
  onDoubleClick={() => alert('Double Clicked!')}
  onMouseEnter={() => console.log('Mouse Enter')}
  onMouseLeave={() => console.log('Mouse Leave')}
  onMouseDown={() => console.log('Mouse Down')}
  onMouseUp={() => console.log('Mouse Up')}
  onMouseMove={() => console.log('Mouse Move')}
  onContextMenu={(e) => {
    e.preventDefault();
    alert('Right Clicked!');
  }}
>
  Hover or Click Me
</div>
```

## Keyboard Events
```jsx 
<input
  type="text"
  onKeyDown={(e) => console.log('Key Down:', e.key)}
  onKeyUp={(e) => console.log('Key Up:', e.key)}
/>
```

## Form Events

```jsx 
<form onSubmit={(e) => { e.preventDefault(); alert('Form Submitted'); }}>
  <input type="text" onChange={(e) => console.log('Change:', e.target.value)} />
  <button type="submit">Submit</button>
</form>
```

## Focus Events
```jsx 
<input
  type="text"
  onFocus={() => console.log('Focused')}
  onBlur={() => console.log('Blurred')}
/>
```
## Clipboard Events

```jsx 
<input
  type="text"
  onCopy={() => alert('Copied!')}
  onCut={() => alert('Cut!')}
  onPaste={() => alert('Pasted!')}
/>
```

## Touch Events (for mobile)

```jsx 
<div
  onTouchStart={() => console.log('Touch Start')}
  onTouchMove={() => console.log('Touch Move')}
  onTouchEnd={() => console.log('Touch End')}
>
  Touch Here
</div>
```

##  Pointer Events
```jsx 
<div
  onPointerDown={() => console.log('Pointer Down')}
  onPointerUp={() => console.log('Pointer Up')}
  onPointerMove={() => console.log('Pointer Move')}
  onPointerEnter={() => console.log('Pointer Enter')}
  onPointerLeave={() => console.log('Pointer Leave')}
>
  Pointer Event Box
</div>
```

## UI Events

```jsx 
<div onScroll={() => console.log('Scrolled')} style={{ overflowY: 'scroll', height: '100px' }}>
  <div style={{ height: '200px' }}>Scroll inside me</div>
</div>
```

## Media Events

```jsx 
<video
  width="320"
  height="240"
  controls
  onPlay={() => console.log('Playing')}
  onPause={() => console.log('Paused')}
  onEnded={() => console.log('Ended')}
>
  <source src="your-video.mp4" type="video/mp4" />
  Your browser does not support the video tag.
</video>
```

## Animation & Transition Events

```jsx
<div
  style={{ animation: 'slide 2s infinite' }}
  onAnimationStart={() => console.log('Animation Start')}
  onAnimationEnd={() => console.log('Animation End')}
  onAnimationIteration={() => console.log('Animation Iteration')}
>
  Animate Me
</div>

<style>
@keyframes slide {
  0% { transform: translateX(0); }
  50% { transform: translateX(100px); }
  100% { transform: translateX(0); }
}
</style>
```

##  Wheel Event

```jsx 
<div
  onWheel={(e) => console.log('Wheel delta:', e.deltaY)}
  style={{ height: '100px', overflowY: 'scroll' }}
>
  <div style={{ height: '300px' }}>Scroll me</div>
</div>
```

## Misc Events

```jsx
<img
  src="https://example.com/image.jpg"
  alt="Example"
  onLoad={() => console.log('Image loaded')}
  onError={() => console.log('Image failed to load')}
/>
```

Would you like these in a downloadable React events cheat sheet with visuals and output logs? 







