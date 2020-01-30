# 01 JavaScript Drum Kit

## Key Points and Steps

- Play sound when a certain key is pressed
  1. Add an event listener `keydown` to the entire window object
  2. Inside of the callback function...
     - Obtain `keyCode` element using `querySelector`
       ```
       audio = document.querySelector(`audio[data-key='${e.keyCode}']`);
       const key = document.querySelector(`.key[data-key='${e.keyCode}']`);
       ```
     - Play audio whenever a key is pressed
       ```
       audio.currentTime = 0;
       audio.play();
       ```
- Add effect and remove effect
  1. Add CSS class when a key is pressed
  ```
  key.classList.add('playing');
  ```
  2. remove CSS class when the transition is over
     - Obtain all keys
       ```
       const keys = document.querySelectorAll('.key');
       ```
     - Loop through all elements and attach event listener
       ```
       keys.forEach(keys => keys.addEventListener('transitionend', removeTransition),
       );
       ```
     - Create removeTransition function
       ```
       function removeTransition(e) {
         if (e.propertyName !== 'transform') return;
         this.classList.remove('playing');
       }
       ```
