Removing or hiding the scrollbar can vary depending on the browser you're targeting, as different browsers have different proprietary pseudo-elements for styling. Here are some common ways to remove the scrollbar while still keeping the scroll functionality:

### For Webkit Browsers (e.g., Chrome, Safari)
```css
/* Hide scrollbar for Chrome, Safari and Opera */
.element::-webkit-scrollbar {
  display: none;
}
```

### For Firefox
```css
/* Hide scrollbar for Firefox */
.element {
  scrollbar-width: none;
}
```

### For Internet Explorer
```css
/* Hide scrollbar for IE */
.element {
  -ms-overflow-style: none;
}
```

### Global Hide (All elements in the entire page)
If you want to hide scrollbars globally for the entire page, you can apply these styles to the `body` or `html` tag.

### Complete Example
```css
/* Hide scrollbar for Chrome, Safari and Opera */
.element::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for Firefox */
.element {
  scrollbar-width: none;
}

/* Hide scrollbar for IE */
.element {
  -ms-overflow-style: none;
}
```

#### Note:
1. Hiding the scrollbar will make it less obvious that content is scrollable, potentially impacting user experience.
2. Some of the above methods are not standard and may not work in future versions of the browsers.

So, depending on your project's needs and target audience, choose the method that best suits you.

___
If you need to use the `&::` pseudo-element along with `-webkit-` vendor prefixes, you're likely using a CSS pre-processor like SCSS or styled-components. Here's how you can do it:

#### Styled-components (JSX):

```jsx
import styled from "styled-components";

const Container = styled.div`
  &::-webkit-scrollbar {
    width: 0;
    display: none; /* Hide scrollbar for Chrome, Safari and Opera */
  }
  scrollbar-width: none; /* Hide scrollbar for Firefox */
  -ms-overflow-style: none;  /* Hide scrollbar for IE and Edge */
`;

function App() {
  return <Container>Your content here</Container>;
}
```

#### SCSS:

```scss
/* styles.scss */

.hide-scrollbar {
  &::-webkit-scrollbar {
    width: 0;
    display: none; // Hide scrollbar for Chrome, Safari and Opera
  }
  scrollbar-width: none; // Hide scrollbar for Firefox
  -ms-overflow-style: none; // Hide scrollbar for IE and Edge
}
```

Then, you can import this SCSS file into your JSX component.

```jsx
import './styles.scss';

function App() {
  return <div className="hide-scrollbar">Your content here</div>;
}
```

These examples will hide the scrollbar across multiple browsers.
___
WebKit is a browser engine developed by Apple, primarily for its Safari browser. A browser engine is a core software component that takes HTML documents, CSS stylesheets, and JavaScript code and renders them into web pages for display to the user. WebKit is also the basis for many other browsers like Google Chrome (although Google eventually forked their engine into Blink), Opera, and various others, especially on mobile devices like iPhones and Androids.

The term "WebKit" in CSS and JavaScript is often seen as a prefix in various properties and APIs to enable browser-specific features that are not yet standardized across all browsers. These are often experimental features or optimizations. For example, the `-webkit-scrollbar` property allows you to customize the scrollbar in WebKit-based browsers.

Here's how you might see it in CSS:

```css
/* This will only work in WebKit-based browsers like Safari */
::-webkit-scrollbar {
  width: 12px;  /* Width of the scrollbar */
}
```

While WebKit-specific properties provide functionality that may not be available in other engines, it's generally a good idea to avoid relying on them too heavily in order to maintain cross-browser compatibility. Always check if there is a standard CSS property that achieves the same result, and consider providing fallbacks for other browsers.