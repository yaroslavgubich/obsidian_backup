To #deploy your Next.js project to #Vercel using the #CLI, follow these steps:

---

### **1. Install Vercel CLI (If Not Installed)**

Run the following command in your terminal:

```sh
npm install -g vercel
```

---

### **2. Login to Vercel**

If you haven't logged in yet, authenticate with:

```sh
vercel login
```

This will open a browser for authentication. Follow the prompts to log in.

---

### **3. Initialize Vercel in Your Project (Only If Not Yet Linked)**

Inside your project folder (`barcoblanco-store`), run:

```sh
vercel
```

It will ask:

- **Set up and deploy?** → Yes
- **Which scope do you want to deploy to?** → Select your Vercel account
- **Link to an existing project?** → Select your project if already created, otherwise choose "Create a new project"
- **What’s your project’s framework?** → Select `Next.js`
- **What directory is your code located in?** → `.` (default)
- **Configure builds and development settings?** → Just press **Enter** for default settings

This links your project to Vercel.

---

### **4. Deploy Your Project**

Run:

```sh
vercel --prod
```

This will build and deploy your project to production.

---

### **5. Deploy to Preview (Optional)**

If you want a **preview deployment** (not production), run:

```sh
vercel
```

This will deploy to a temporary preview URL.

---

### **6. Check Deployment**

Once the deployment finishes, Vercel will provide a link like:

```
https://barcoblanco-store.vercel.app
```

Open the link to check your live project.

---

### **7. Updating & Redeploying**

After making changes, simply run:

```sh
vercel --prod
```

It will deploy the latest version of your project.

---

**🚀 Done! Your Next.js project is now live on Vercel!**