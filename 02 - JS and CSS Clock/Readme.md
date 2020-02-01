# 02 JS and CSS Clock

## Key Points

1. Set rotation onto clock hands
2. Get current time
3. Set interval for realtime udpates

#### property used

- **transform-origin**  
  sets the origin for an element's transformations
- **transform: rotate()**  
  allows you to specify rotation transforms individually and independently
- **transition**  
  a shorthand property for transition-property, transition-duration, transition-timing-function, and transition-delay
- **transition-timing-function: cubic-bezier(x, x, x, x)**  
  sets how intermediate values are calculated
- **setInterval(callback, time)**  
  repeatedly calls a function or executes a code snippet, with a fixed time delay between each call
- **new Date()**  
  creates a new Date object

## Steps

### CSS

1. Set clock hands to be vertical
2. Use `transform-origin` to set the rotation point to the furthest point on the x-axis (to the right)
3. Apply `transition` to smoothen the effect
4. Set the `transition-timing-function` to create a ticking effect

```
.hand {
  /* above omitted */
  transform-origin: 100%;
  transform: rotate(90deg);
  transition: all 0.05s;
  transition-timing-function: cubic-bezier(0.1, 2.3, 0.58, 1);
}
```

### JavaScript

1. Use `querySelector()` to define variables for each clock hand
2. Create a function which will be responsible for calculating the number of degrees for rotation
3. Convert the numerical value of current time to the degree of rotation  
   `((time / max) * 360)`
4. Adjust the starting point of rotation which was offset  
   `((time / max) * 360) + 90`
5. Make the degree of rotation sync with current time  
   `` secondHand.style.transform = `rotate(${secondsDegrees}deg)` ``
6. Use `setInterval()` to repeatedly call the function (created in step 2)

### Fine-tune

- **Issue:** Whenever clock hands reach 90°, clock hands will go from 444° to 90° counterclockwise
- **Soluiton:** add IF statement to remove transition at that point

  ```
  if (secondsDegrees === 90) secondHand.style.transition = `all 0s`;
  else secondHand.style.transition = `all 0.05s`;

  if (minsDegrees === 90) minHand.style.transition = `all 0s`;
  else minHand.style.transition = `all 0.05s`;
  ```

* **Issue:** Rotation of the hour hand feels unnatural
* **Soluiton:** Set the hour hand rotates guadually
  ```
  const hoursDegrees =
    (hours / 12) * 360 +
    (mins / 60 / 12) * 360 +
    (seconds / 60 / 60 / 12) * 360 +
    90;
  hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
  ```
