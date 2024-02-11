# create-svelte

## Generate static site using svelte SSG

To assist you in creating a static webpage for GitHub Pages using Svelte, we have developed a template for you: [ShaokangJiang/svelte-template (github.com)](https://github.com/ShaokangJiang/svelte-template).

Please follow the link provided, and initiate the creation of a new repository.

![image-20240210175403813](./assets/image-20240210175403813.png)

After GitHub completes the cloning process, navigate to the settings page. On the left panel, under the "Pages" tab, locate the "Source" section and select "GitHub Actions" as the source. 

Clone this repository and proceed with your work. Upon completion, commit and push your changes. The corresponding GitHub Actions will then execute, building a static website hosted at `https://your-username.github.io/your-repo-name` for you.

![image-20240210175104365](./assets/image-20240210175104365.png)



Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/main/packages/create-svelte).

## Creating a project 

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm create svelte@latest

# create a new project in my-app
npm create svelte@latest my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
