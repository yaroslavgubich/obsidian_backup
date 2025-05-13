#key #react

Why do I need this ? 


Here’s what those two things are doing and why they matter:

### `key` on the outer div in the `.map()`

```jsx
{expCards.map(card => (
  <div key={card.title} className="exp-card-wrapper">   // ← key lives here
    …
  </div>
))}
```

- **Why React needs a `key`**
    
    - When you render a list, React compares the _previous_ virtual-DOM tree with the _next_ one to figure out which items changed, moved, or were removed.
        
    - A stable, unique `key` lets React match list items between renders quickly, instead of re-mounting them all or getting the order wrong.
        
    - Without keys (or with duplicated keys) you can get subtle UI bugs (wrong item receives focus, wrong component state preserved, animated lists jitter, etc.) and React will log a warning.
        
- **Why the `key` must be on the topmost element returned by the callback**  
    React ignores `key` on any nested child. Only the element that directly represents the list “item” should have it. If you prefer not to add an extra wrapper div, you can use **`<React.Fragment>`** (or the shorthand `<>`) and put the key there:
    
    ```jsx
    {expCards.map(card => (
      <React.Fragment key={card.title}>
        <div className="xl:w-2/6">
          <GlowCard card={card}>
            …
          </GlowCard>
        </div>
      </React.Fragment>
    ))}
    ```
    
- **Small bug in your snippet**  
    You wrote `key="card.title"` (a literal string). It should be **`key={card.title}`** so React receives the actual title value (e.g., `"AWS"`), not the text `"card.title"` for every item.
    
- **Choosing the key**
    
    - Prefer something **unique and stable** like an `id` from your data (`card.id`) rather than the title, in case two cards share the same name or the title can change.
        

---

#### Take-aways

- `xl:w-2/6` is a Tailwind width utility that only kicks in at the xl breakpoint—handy for responsive layouts.
    
- `key` is essential whenever you render arrays; place it on the element that represents each list item and make sure it’s a unique, consistent value.