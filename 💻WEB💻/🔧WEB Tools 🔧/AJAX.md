#whatis #ajax 
AJAX, which stands for Asynchronous JavaScript and XML, is a set of web development techniques that enable web applications to send and receive data asynchronously from a server without requiring a full page reload. This approach helps in creating smoother, faster, and more interactive web experiences.

AJAX uses a combination of:

- A browser built-in XMLHttpRequest object (or more recently, the Fetch API) to request data from a web server,
- JavaScript and HTML DOM to display or use the data.

### How AJAX Works:

1. **User Event**: A user event triggers the AJAX call, such as clicking a button or submitting a form.
2. **Create XMLHttpRequest**: The JavaScript XMLHttpRequest object is created.
3. **Send Request to Server**: The XMLHttpRequest object sends a request to a server (this can be a GET or POST request).
4. **Server Processes Request**: The server processes the request, interacts with a database if necessary, and sends a response back to the webpage.
5. **Response Loaded**: Once the response data is loaded, the callback function is executed to update the webpage content dynamically without reloading the page.

### AJAX in React:

React does not include AJAX by default, but it is designed to work seamlessly with AJAX techniques for data fetching and other server interactions. React components can use AJAX calls to fetch data in their lifecycle methods, such as `componentDidMount`, or in hooks like `useEffect` for functional components. Here are the typical ways to integrate AJAX in React:

- **XMLHttpRequest**: Although not commonly used in modern React applications, it's possible to use the traditional XMLHttpRequest to perform AJAX calls.
- **Fetch API**: A more modern and widely used alternative to XMLHttpRequest, providing a more powerful and flexible feature set.
- **Axios**: A popular third-party library that simplifies HTTP requests. It supports promises, making it easy to use in React applications.

### Example of Fetch API in React:

```javascript
import React, { useState, useEffect } from 'react';

function App() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.error('Error fetching data:', error));
  }, []); // Empty dependency array means this effect runs once after the initial render

  return (
    <div>
      {data ? <div>{data.title}</div> : <p>Loading...</p>}
    </div>
  );
}

export default App;
```

### Conclusion:

AJAX itself is not part of React; however, React provides the flexibility to use AJAX for fetching data asynchronously. Using AJAX in React can significantly enhance user experience by updating the UI dynamically based on server responses without reloading pages. The Fetch API or libraries like Axios are common choices among React developers for making HTTP requests.

what #htttp #reqest contains: 

### HTTP request

Composed of 4 elements:  
  
  

- **VERB**: GET / POST / PATCH / DELETE ([REST pattern](https://en.wikipedia.org/wiki/Representational_state_transfer))
- **URL**: the address of the resource requested
- **HEADERS**: provide additional informations about the request
- **BODY (optional)**: used to send data to the server

### Modern way

[`fetch` API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

Easier to understand, faster and with more features.

### Very simple structure

(As seen during the HTTP & API lecture)

```js
// GET request example
fetch(url).then((response) => {
  // Do something once HTTP response is received
})
```


### Fetch in a nutshell

Takes only 2 arguments: the URL and an optional JavaScript `Object`

```js
fetch(url, { // Second argument allows to precise verb, headers and body
  method: "POST",
  headers: {},
  body: {}}
)
```

  

Allows to interact with the server `response` thanks to `.then()`

```js
.then((response) => {
  // Do something once HTTP response is received
})
```

### Why do we need `.then()`?

By default `fetch` returns a JavaScript object called a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

```js
const url = "https://api.github.com/users/dhh"
console.log(fetch(url));
```

`.then()` allows us to wait for the end of the operation before interacting with the `response`

```js
fetch(url) // We make the HTTP request
  .then((response) => {
    // As soon as the response is received, we can interact with the response
  })
```
### What is a [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response)?

It’s an interface of the `fetch` API that represents the response to a HTTP request
![[Pasted image 20240427141238.png]]![[Pasted image 20240427141255.png]]

It has 3 states: `pending`, `fulfilled` and `rejected`
You can access to the content of the `Response` by calling `.json()`  
(which also returns a `Promise`)

```
fetch(url).then(response => console.log(response.json()));
```

### Most common structure of a `fetch` request

```js
const url = "https://api.github.com/users/dhh"

fetch(url) // Make the HTTP request
  .then(response => response.json()) // Wait for the response and parse it as JSON
  .then((data) => {
    console.log(data); // Wait for parsing, allowing us to manipulate the data
  })
```

---

## Advanced requests with `fetch`

Let’s use the testing API [reqres.in](https://reqres.in/)

`/api/register` endpoint to live-code a `POST` request with `fetch`

### Add a form to your HTML

```js
<!-- index.html -->
<!-- [...] -->
<form action="" id="form">
  <input type="email" id="email">
  <input type="password" id="password">
  <input type="submit">
</form>
```

### `signUp()` function

It will collect the `email` and the `password` on `submit`

```js
const signUp = (event) => {
  event.preventDefault()
  const emailValue = document.getElementById("email").value
  const passwordValue = document.getElementById("password").value
  // Todo: send the request with fetch
}

const form = document.querySelector("#form")
form.addEventListener("submit", signUp)
```

### `fetch` second argument

You can define the `verb`, the `headers` and the `body`

of the request in a JavaScript `Object`

```js
const requestDetails = {
  method: "POST",
  headers: {"Content-Type": "application/json"},
  body: JSON.stringify({"email": emailValue, "password": passwordValue})
}
```

### Send the request

```js
const signUp = (event) => {
  event.preventDefault()
  const emailValue = document.getElementById("email").value
  const passwordValue = document.getElementById("password").value
  const requestDetails = {
    method: "POST",
    headers: {"Content-Type": "application/json"},
    body: JSON.stringify({"email": emailValue, "password": passwordValue})
  }
  fetch("https://reqres.in/api/register", requestDetails)
    .then(response => response.json())
    .then(data => console.log(data));
}

const form = document.querySelector("#form")
form.addEventListener("submit", signUp)
```

---

## Adding JS Packages

Let’s add alerts with [`sweetalert2` package](https://sweetalert2.github.io/)

```js
<!-- index.html -->

<!-- Add css in the head -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/sweetalert2@11.7.1/dist/sweetalert2.min.css">

<!-- Add javascript script at the end of the body -->
<the-script src="https://cdn.jsdelivr.net/npm/sweetalert2@11.7.1/dist/sweetalert2.all.min.js"></the-script>
<!-- rename the-script into script after copy-paste -->
```

```js
// javascript/application.js
fetch("https://reqres.in/api/register", requestDetails)
  .then((response) => {
    if (response.status === 200) {
      Swal.fire({title: 'Success', text: 'You are connected', icon: 'success'})
    } else {
      Swal.fire({title: 'Error!', text: 'Oups! Something went wrong', icon: 'error'})
    }
  })
```

### Problem

Adding a lot of script tags at the end of the body can become messy 🤯

![](https://kitt.lewagon.com/camps/1576/lectures/content/assets/javascript/external_libraries.png)

### Solution: [`import-maps`](https://github.com/WICG/import-maps)

A library to organise JavaScript imports

### How does it work?

One script to import them all 😎

```js
<!-- index.html -->

<the-script type="importmap">
{
  "imports": {
    "bootstrap": "https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js",
    "sweetalert2": "https://cdn.jsdelivr.net/npm/sweetalert2@11.7.1/+esm"
  }
}
</the-script>
<!-- rename the-script into script after copy-paste -->
```

⚠️ `import-maps` should be added in the `head` tag  
  
  

⚠️ Imported libraries should be packaged as [ES modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

### Import your script as a module

`importmap` allows you import libraries in your JS files.  
  
  

But it only works only if our file has the `type="module"` attributes

```js
<!-- index.html -->

<the-script src="javascript/application.js" type="module"></the-script>
<!-- rename the-script into script after copy-paste -->
```

### Import libraries when needed

```js
// javascript/application.js
import Swal from 'sweetalert2';
```

### Compatibilities ⚠️

`importmap` isn’t fully supported by browsers [at the moment](https://caniuse.com/import-maps)

![](https://kitt.lewagon.com/camps/1576/lectures/content/assets/javascript/import_maps_compatibilities.png)

### [`es-module-shims`](https://github.com/guybedford/es-module-shims)

You need to import `es-module-shims` before the `importmap`

to make it work with older browsers

```js
<the-script async src="https://ga.jspm.io/npm:es-module-shims@1.6.3/dist/es-module-shims.js"></the-script>
```


#how to get all data from #forms

https://www.freecodecamp.org/news/formdata-explained/

In JavaScript, "form data" can also refer to the `FormData` object, which is used to construct a set of key/value pairs representing form fields and their values. This can be used to send data via AJAX without needing to manually process each form element.

### Key Features of the `FormData` Object:

- **Simplicity**: Easily construct and send form data asynchronously.
- **Flexibility**: Works with both `XMLHttpRequest` and the modern `Fetch` API.
- **Support for Files**: Unlike simple key/value pairs, `FormData` can handle file uploads seamlessly.

Here's a brief example of how you might use the `FormData` object with the Fetch API to send data to a server:

```javascript
// Assuming you have a form with id="myForm"
const form = document.getElementById('myForm');
const formData = new FormData(form);

// Optionally, add additional data to formData
formData.append('key', 'value');

// Use Fetch API to send formData to a server
fetch('your-server-endpoint', {
  method: 'POST',
  body: formData,
})
.then(response => response.json())
.then(result => console.log('Success:', result))
.catch(error => console.error('Error:', error));
```

The `FormData` object is particularly useful for sending files and large pieces of data that are complex to handle manually. It manages content-type headers automatically, making it easier to implement robust file uploading features.

#how to #reset a #form 

To reset a form in JavaScript, you can use the `reset()` method on the form element. This method clears all the input fields back to their initial values. Here’s a quick example of how to do it:

```javascript
// Assume there's a form with the ID 'myForm'
const form = document.getElementById('myForm');

// To reset the form
form.reset();
```

This will immediately clear all form inputs and reset them to their default values as specified in the HTML form definitions. This is particularly useful for clearing a form after submission or when providing an option to clear a form manually with a reset button.