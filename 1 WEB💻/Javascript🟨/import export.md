#js #import #export 

Here’s a **comprehensive cheat sheet** for JavaScript **import/export** syntax covering both CommonJS and ES6 modules.

---

## **ES6 Modules**

### **Export Syntax**

#### Named Exports
Exports multiple named variables, functions, or classes.
```javascript
// Exporting named variables/functions
export const name = 'Yaroslav';
export function greet() {
  console.log('Hello!');
}
export class Person {
  constructor(name) {
    this.name = name;
  }
}
```

#### Default Export
Exports a single default value (can be variable, function, or class).
```javascript
// Default export
export default function greet() {
  console.log('Hello, world!');
}

// or

const name = 'Yaroslav';
export default name;
```

#### Combining Named and Default Exports
```javascript
export const name = 'Yaroslav';
export default function greet() {
  console.log('Hello, world!');
}
```

#### Export All (`*`)
Re-exports everything from another module.
```javascript
export * from './module.js';
```

#### Export with Renaming
Rename exports for more control.
```javascript
const myName = 'Yaroslav';
export { myName as name };
```

---

### **Import Syntax**

#### Importing Named Exports
```javascript
import { name, greet } from './module.js';
```

#### Importing All as a Namespace
```javascript
import * as Module from './module.js';
console.log(Module.name);
Module.greet();
```

#### Importing Default Exports
```javascript
import greet from './module.js';
greet();
```

#### Mixing Default and Named Imports
```javascript
import greet, { name } from './module.js';
```

#### Import with Aliases
```javascript
import { greet as sayHello } from './module.js';
sayHello();
```

---

## **CommonJS Modules**

### **Export Syntax**

#### Exporting with `module.exports`
```javascript
// Single export
module.exports = function greet() {
  console.log('Hello!');
};

// or

module.exports = {
  name: 'Yaroslav',
  greet: function () {
    console.log('Hello!');
  }
};
```

#### Exporting with `exports`
```javascript
exports.name = 'Yaroslav';
exports.greet = function () {
  console.log('Hello!');
};
```

---

### **Import Syntax**

#### Importing a Module
```javascript
const module = require('./module.js');
module.greet();
console.log(module.name);
```

#### Destructuring Named Exports
```javascript
const { name, greet } = require('./module.js');
console.log(name);
greet();
```

---

## **Dynamic Imports (ES6)**

#### Importing a Module Dynamically
```javascript
import('./module.js').then((module) => {
  module.greet();
});
```

#### Dynamic Import with `async/await`
```javascript
(async () => {
  const module = await import('./module.js');
  module.greet();
})();
```

---

## **Special Cases**

### Importing JSON Files
```javascript
import data from './data.json' assert { type: 'json' }; // ES6 Modules
const data = require('./data.json'); // CommonJS
```

### Importing CSS/Assets (for frameworks like React)
```javascript
import './styles.css';
import logo from './logo.png';
```

### Side Effects Only (No Variables Imported)
```javascript
import './polyfills.js';
```

---

### **Quick Comparison**

| Feature                  | ES6 Modules       | CommonJS          |
|--------------------------|-------------------|-------------------|
| Syntax                  | `import/export`   | `require/module.exports` |
| Default Export          | `export default`  | `module.exports`  |
| Static vs Dynamic        | Static            | Dynamic           |
| Top-Level `await`        | Supported         | Not supported     |
| Tree Shaking            | Supported         | Not supported     |

---

This cheat sheet gives you a full reference for working with JavaScript modules in both CommonJS and ES6 formats. Let me know if you need practical examples or further clarification!