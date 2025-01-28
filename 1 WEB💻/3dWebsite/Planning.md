____
**
1. Create a folder in a #hosting platform (#hostinger) in this example
2. In #yarn [Yarn](https://www.youtube.com/watch?v=0DGClZD5LEM) #vit [Vite](https://www.youtube.com/watch?v=KCrXgy8qtjM)
3. 
4. Initialize #git  and make a commit 
5. Add app.jsx
6. yarn run dev
7. 1
8. 

Below is a detailed, ordered list of steps you'd typically follow to start a project using **Yarn** and **Vite**, a build tool and development server that aims to provide a faster and leaner development experience for modern web projects.
___
### 1. Install Node.js and Yarn [Vit_2hrs_vid](https://www.youtube.com/watch?v=VAeRhmpcWEQ)
Before you start, you need to have Node.js and Yarn installed. You can download Node.js from [here](https://nodejs.org/) and Yarn from [here](https://yarnpkg.com/).
___
### 2. Create a New Project Directory
Create a new directory where you want your project to reside.

```bash
mkdir my-new-project
cd my-new-project
```
___
### 3. Initialize a Yarn Project
Initialize a new Yarn project in the directory you just created.

```bash
yarn init -y
```

This will generate a `package.json` file with default settings.
___
### 4. Add Vite to Your Project
Install Vite as a development dependency.

```bash
yarn add vite --dev
```
___
### 5. Add Scripts to package.json
Open the `package.json` file and add the following scripts to make it easier to run Vite:

```json
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "serve": "vite preview"
}
```
___
### 6. Initialize a Vite Project
Initialize a new Vite project template. You could choose a template based on the framework you're using (Vanilla, React, Vue, Svelte, etc.)

```bash
yarn create vite
```

Follow the prompts to configure your project.
___
### 7. Install Project Dependencies
If you've cloned or initialized a project that already has a `package.json` file, run the following to install all required dependencies.

```bash
yarn install
```
___
### 8. Start Development Server
To start the Vite development server, run:

```bash
yarn dev
```

This should launch the Vite development server, and your app should be available at `http://localhost:3000/` or another port if you've specified one.
___
### 9. Develop Your Project
With the development server running, you can now start building your application. Vite will automatically refresh the browser as you make changes.

### 10. Run a Production Build
When you're ready to create a production-ready build, you can use:

```bash
yarn build
```

This will generate optimized files in a `dist` directory.
___
### 11. Test Production Build Locally
You can test the production-ready version locally using:

```bash
yarn serve
```
___
### 12. Deploy
Once you're happy with your application, you can deploy it to your chosen hosting provider.

By following these steps, you should have a solid foundation for developing web projects with Yarn and Vite.
___