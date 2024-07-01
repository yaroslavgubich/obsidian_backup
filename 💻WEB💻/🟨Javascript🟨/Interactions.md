Example of utilizing #eventlistener #removeeventlistener #button #queryselector #classlist 


Here's how you can modify your `clicked` function to include this behavior:

```javascript
const btn = document.querySelector("#my-button");
const link = document.querySelector("#hide-link");

const clicked = () => {
  // Change button text to "clicked"
  btn.innerHTML = "clicked";
  link.classList.remove("d-none");

  // Set a timeout to reset the button text after each click
  setTimeout(() => {
    btn.innerHTML = "hide";
  }, 5000); // Reset the text after 5 seconds
};

// Add the event listener to the button
btn.addEventListener("click", clicked);
```

In this modified code:

- When the button is clicked, the text changes to "clicked".
- A `setTimeout` is then set up to change the text back to "hide" after 5 seconds.
- This `setTimeout` will be set up each time the button is clicked, ensuring that the text resets 5 seconds after each click.

This approach ensures that no matter how many times you click the button, the text will always revert to "hide" 5 seconds after each click.

one #button effect the other 

