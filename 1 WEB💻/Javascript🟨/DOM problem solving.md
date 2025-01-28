const card = document.querySelectorAll(".scratchcard");

console.log(card);

card.style.background = "rgba(255, 255, 255, 1)";

#queryselectorAll not selecting all elements 

#solution 
The issue you're encountering is due to the fact that `document.querySelectorAll(".scratchcard")` returns a NodeList, not a single element. Therefore, you can't directly apply styles to the entire NodeList using `card.style`. Instead, you need to iterate over each element in the NodeList and apply the style individually.

Here's how you can achieve that:

```javascript
const cards = document.querySelectorAll(".scratchcard");

cards.forEach(card => {
    card.style.background = "rgba(255, 255, 255, 1)";
});
```

This code iterates over each element with the class "scratchcard" and sets its background color to white with full opacity.

By using `forEach`, you apply the style to each element in the NodeList separately.

In conclusion, to apply styles to multiple elements selected using `querySelectorAll`, you need to iterate over the resulting NodeList and apply the styles to each individual element.

#problem #queryselector not working 
``` js
// todo1: Select all the scratchcards off the page (using either querySelector or querySelectorAll)✅

const card = document.querySelectorAll(".scratchcard");

card.forEach((elem) => {

  elem.style.background = "rgba(255, 255, 200, 1)";

  card.addEventListener("click",fucntion(){

    const balance = document.getElementById("balance").innerHTML;

    const balance = balance - 10

    document.getElementById("balance").innerHTML = balance;

  })

});

// todo2: Listen for when the user clicks on one of these scratchcards.

  

// todo3:

/* When they do, subtract 10 from the amount

 of money they have. Don’t worry about calculating

  how much they’ve won yet (that’s the next section). */

  

// todo4: Display their balance on the page.
```

#fix #solution #arrowFunction needs to be like this 
``` js // todo1: Select all the scratchcards off the page (using either querySelector or querySelectorAll)✅

const card = document.querySelectorAll(".scratchcard");

card.forEach((elem) => {

  elem.style.background = "rgba(255, 255, 200, 1)";

  card.addEventListener("click",fucntion(){

    const balance = document.getElementById("balance").innerHTML;

    const balance = balance - 10

    document.getElementById("balance").innerHTML = balance;

  })

});

// todo2: Listen for when the user clicks on one of these scratchcards.

  

// todo3:

/* When they do, subtract 10 from the amount

 of money they have. Don’t worry about calculating

  how much they’ve won yet (that’s the next section). */

  

// todo4: Display their balance on the page.
```
