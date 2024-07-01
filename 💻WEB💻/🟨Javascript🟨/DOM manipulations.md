``` javascript
```/* eslint-disable no-multiple-empty-lines */

/* eslint-disable prefer-const */

/* eslint-disable import/extensions */

  

import runChallenges from "../spec/list_generator_examiner.js";

  

const listItem = (content) => {

  // Return the proper <li> HTML tag with its content (as a string)

  return `<li class="list-group-item">${content}</li>`;

};

  

const unorderedList = (items) => {

  // Convert each item into a list item and join them into a single string

  const listItems = items.map(item => listItem(item)).join("");

  return `<ul class="list-group">${listItems}</ul>`;

};

  

// Do not remove these lines:

if (typeof window === "object") {

  document.addEventListener("DOMContentLoaded", () => {

    const array = ["eggs", "bread"];

    const listHTML = unorderedList(array);

    document.body.innerHTML += listHTML;

  });

}

  

runChallenges(listItem, unorderedList); // Do not remove.

export { listItem, unorderedList }; ```

#solution #list #eventlistener #js
how to #disable #eventlistener 
``` js
const cards = document.querySelectorAll(".scratchcard");

cards.forEach((card) => {

  card.addEventListener("click", function handleClick() {

    // Change background as intended

    card.style.background = "rgba(155, 235, 215, 1)";

  

    // Disable further events by removing the event listener

    card.removeEventListener("click", handleClick);

  

    // Adjust balance by deducting 10, ensuring balance is non-negative before deducting

    let balance = Number(document.getElementById("balance").innerHTML);

    if (balance > 0) {

      balance -= 10;

      document.getElementById("balance").innerHTML = balance;

    }

  });

});```
___
#cheatsheet on #eventlisteners and #dom

https://kitt.lewagon.com/camps/1576/lectures/04-Front-End%2F04-JS-and-DOM

#video with instructions 

https://www.youtube.com/watch?v=y17RuWkWdn8


#select #classes #eventlistener 


``` JS
//* simple version with .btn

  

const displayAlertOnButtonClick = () => {

  // TODO: Select the big green button

  const button = document.querySelector(".btn");

  // TODO: Bind the `click` event to the button

  button.addEventListener("click", () => {

    // TODO: On click, display `Thank you!` in a JavaScript alert!

    alert("Thank you!");

  });

};

  

// displayAlertOnButtonClick(); // Do not remove!

  

//* version with concatenated class names

  

const displayAlertOnButtonClick = () => {

  // TODO: Select the big green button

  const button = document.querySelector(".btn.btn-lg.btn-success");

  // TODO: Bind the `click` event to the button

  button.addEventListener("click", () => {

    // TODO: On click, display `Thank you!` in a JavaScript alert!

    alert("Thank you!");

  });

};

  

// displayAlertOnButtonClick(); // Do not remove!

  

//* short version without saving button as const or let for later use

document.querySelector('.btn.btn-lg.btn-success').addEventListener('click', () => {

  alert('Button clicked!');

});   
```

#select #multiple elements with #queryselectorAll 
``` js
// ~ TODO: sport btn: sport,toggle the active css class on the element

// ~ TODO:      select all buttons and store in a variable

const sportIcons = document.querySelectorAll(".clickable");

sportIcons.forEach((elem) => {

// ~ TODO:      add class active

// ~ TODO:  We should be able to select several sports

  elem.addEventListener("click", event => elem.classList.toggle("active"));

});

// ~ TODO: refactor >>>

const sportIcons = document.querySelectorAll(".clickable");

  

const toggleActive = (event) => {

  event.currentTarget.classList.toggle("active");

};

  

const bindButtonToClick = (button) => {

  button.addEventListener('click', toggleActive);

};

  

sportIcons.forEach(bindButtonToClick);

// more concise version 

document.querySelectorAll(".clickable").forEach(button => {
  button.addEventListener('click', event => event.currentTarget.classList.toggle("active"));
});

```