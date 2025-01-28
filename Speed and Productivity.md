#aliases #npmrundev #npmrunbuild
To retain the existing functionality in your `package.json` while adding the ability to use `d` or `b` as shortcuts, follow these steps:

### Update Your Shell Configuration for `d` and `b`

You will create **global shell aliases** for `d` and `b` to map them directly to `npm run dev` and `npm run build`. This approach avoids modifying your `package.json` and works seamlessly.

#### Steps:

1. **Edit Your Shell Configuration File**
    
    - For **bash** users: Open `~/.bashrc`
    - For **zsh** users: Open `~/.zshrc`
    - For **fish** users: Open `~/.config/fish/config.fish`
2. **Add the Aliases** Append the following lines to the file:
    
    ```bash
    alias d="npm run dev"
    alias b="npm run build"
    ```
    
3. **Reload the Configuration File** Run the appropriate command based on your shell to apply the changes:
    
    - For bash:
        
        ```bash
        source ~/.bashrc
        ```
        
    - For zsh:
        
        ```bash
        source ~/.zshrc
        ```
        
    - For fish:
        
        ```bash
        source ~/.config/fish/config.fish
        ```
        
4. **Use the New Shortcuts**
    
    - Type `d` to run `npm run dev`:
        
        ```bash
        d
        ```
        
    - Type `b` to run `npm run build`:
        
        ```bash
        b
        ```
        

---

### Keeping `package.json` Unchanged

Your `package.json` remains as:

```json
"scripts": {
    "dev": "next dev --turbopack",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
}
```

This setup ensures both `npm run dev` and `npm run build` are fully functional while providing a global shorthand for those commands.

---

### Optional (for Consistency Across Systems)

If you’re working in a team and want everyone to have these shortcuts, you can document the alias setup in your project’s `README.md` so others can replicate it on their local environments.