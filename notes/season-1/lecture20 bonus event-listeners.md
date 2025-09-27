# Image Gallery

## The DOM Structure
![Image 1](/assets/Screenshot%20(13).png)

## Add Event Listener
![Image 2](/assets/Screenshot%20(14).png)

Now when we `console.log(e)`, a lot of information about the event like `type`, `target`, etc., is shown.

We can set multiple event listeners for the same element, and the **order of execution** will be the **same as in the source code**.

## Event Propagation and Bubbling
![Image 3](/assets/Screenshot%20(15).png)

**DEFAULT BEHAVIOUR:** bubbling — an event propagates to its parents.

- When we click on an element, its event runs first, then its parent's, then the parent's parent, and so on.

**Examples:**
- Click grandparent → Grandparent 1  
- Click parent → Parent 1 then Grandparent 1  
- Click child → Child 1 then Parent 1 then Grandparent 1  

## Events in Document
![Image 4](/assets/Screenshot%20(16).png)

If we add an event to `document`, clicking anywhere triggers it.

## Capture
![Image 5](/assets/Screenshot%20(17).png)

The **three phases** of event propagation:

Capture (only if `capture:true`) -> Target -> Bubbling

- Capture propagates **downwards**.  
- Example: if grandparent has `capture:true`, clicking child executes **grandparent capture first**, then normal bubbling (`child -> parent -> document`).

![Image 6](/assets/Screenshot%20(18).png)

Here, **all captures occur first**, then bubbling.

## Stopping Event Propagation
![Image 7](/assets/Screenshot%20(19).png)

- When propagation reaches an element with `e.stopPropagation()`, it **stops propagation** in either capture or bubbling.

![Image 8](/assets/Screenshot%20(20).png)

- The event for that element **occurs only once**.

![Image 9](/assets/Screenshot%20(21).png)

## Removing Element
![Image 10](/assets/Screenshot%20(22).png)

- If we do not use a **named function** (e.g., `printHi`), `.removeEventListener` won’t work because **anonymous functions are different references**.

![Image 11](/assets/Screenshot%20(23).png)

- Adding a new `div` dynamically won’t work as expected because the selector only contains **existing divs** at the time the listener was added.

![Image 12](/assets/Screenshot%20(24).png)

- We can fix it using **event delegation**: check `event.target.matches("div")`. This way, dynamically added divs are also handled.

![Image 13](/assets/Screenshot%20(25).png)

A **global event listener** example.

# SETINTERVAL
```js
// Example: Print a message every 2 seconds
let count = 0;
const intervalId = setInterval(() => {
    console.log("Hello! Count: " + count);
    count++;
    if (count === 5) {
        clearInterval(intervalId); // Stop the interval after 5 times
    }
}, 2000);

```

setInterval(callback, delay) repeatedly executes the callback function every delay milliseconds.
Returns an interval ID that can be used to stop the timer with clearInterval().
Common use cases:

Repeatedly update UI elements (e.g., clock, slideshow).

Polling server or API.

Animations in combination with DOM manipulation


