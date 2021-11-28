# Svelte Learning

Svelte is a front-end compiler for creating reactive web apps & interfaces. It can be used for small parts of a site or entirely (SPA).

## What is the difference between Svelte and front-end framework like React?

Svelte is not a framework, but a compiler. It compiles your code for production at build time into a single vanilla JS bundle. Moreover, no extra scripts or libraries are shipped to production, it causes results in a faster running website.

- No Virtual DOM
- Write less code

## Installation

1. Install degit package

```
npm install -g degit
```

2. Create Svelte project

```
degit sveltejs/template <project_name>

cd <project_name>
```

3. Install packages

```
npm install
```

4. Run project

```
npm run dev
```

## Enable TypeScript in Svelte

You can enable TS in Svelte project by running setupTypeScript.js file with Node. Then, re-run your dependency manager with npm install again.

```
node scripts/setupTypeScript.js

npm install
```

When you change your code, Svelte automatically re-build JS bundle again. No need to install package like nodemon.

## Folder Structure

- App.svelte - svelte component
- scripts/setupTypeScript.js - enable TypeScript, it will be disappeared after running this file.
- rollup.config.js - svelte config like a webpack.
