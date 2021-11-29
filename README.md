# Svelte Learning

Svelte is a front-end compiler for creating reactive web apps & interfaces. It can be used for small parts of a site or entirely (SPA).

## What is the difference between Svelte and front-end framework like React?

Svelte is not a framework, but a compiler. It compiles your code for production at build time into a JavaScript. Moreover, no extra scripts or libraries are shipped to production, it causes results in a faster running website.

- No Virtual DOM
- Write less code
- Produce highly optimized JS
- About 30% faster than other frameworks

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

## Svelte Component

```svelte
<script lang="ts">
  export let name: string;
  let age = 21;

  const changeAge = () => {
    age = 22;
  };
</script>

<main>
  <h1>Hello {name}!</h1>
  <p>{age}</p>
  <button on:click="{changeAge}">Change Age</button>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
```

## User Input & Data Binding

Two-way binding value with very easy way

```svelte
<script lang="ts">
  export let name: string;
  let job = 'Frontend developer';

  const changeJob = () => {
    job = 'Backend Developer';
  };

  const handleInput = (event) => {
    job = event.target.value;
  };
</script>

<main>
  <h1>Hello {name}!</h1>
  <p style="color:#0066ff">Your job is {job}</p>
  <!-- <input type="text" on:input="{handleInput}" value="{job}" /> -->
  <input type="text" bind:value={job} />
  <button on:click="{changeJob}">Change Job</button>
</main>
```

## Reactive Value

Reactive value update automatically when the data it depends on, change.

```svelte
<script lang="ts">
	let firstName = "Chitsanupong"
	let lastName = "Tangvasinkul"

	$: fullName = `${firstName} ${lastName}`
	$: {
		console.log(firstName)
		console.log(lastName)
	};
</script>

<main>
	<h1>Hello {fullName}</h1>
	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
</main>
```

## Loop

```svelte
<script lang="ts">
	let users = [
		{name: 'john', age: 24, id: 1},
		{name: 'mint', age: 22, id: 2},
		{name: 'carlos', age: 21, id: 3}
	]
</script>

<main>
	{#each users as user (user.id)}
	<div>
		<h4>{user.name}</h4>
		<p>{user.age} years old.</p>
	</div>
	{:else}
		<p>There are no users.</p>
	{/each}
</main>
```

## Inline Event Handlers

```svelte
<script lang="ts">
	let users = [
		{name: 'john', age: 24, id: 1},
		{name: 'mint', age: 22, id: 2},
		{name: 'carlos', age: 21, id: 3}
	]

	const deleteUser = (id) => {
		users = users.filter((user) => user.id != id)
	}
</script>

<main>
	{#each users as user (user.id)}
	<div>
		<h4>{user.name}</h4>
		<p>{user.age} years old.</p>
		<button on:click={() => deleteUser(user.id)}>Delete</button>
	</div>
	{:else}
		<p>There are no users.</p>
	{/each}
</main>
```

## Condition

```svelte
<script lang="ts">
	let users = [
		{name: 'john', age: 24, id: 1},
		{name: 'mint', age: 22, id: 2},
		{name: 'carlos', age: 21, id: 3}
	]

	const deleteUser = (id) => {
		users = users.filter((user) => user.id != id)
	}
	let score = 85
</script>

{#if score >= 80}
	<p>Grade: A</p>
{:else if score > 60}
	<p>Grade: B</p>
{:else}
	<p>Grade: F</p>
{/if}

```

## Import & Export Component

Svelte component is automatically exported. So, you can just import Svelte component without export that component.

```svelte
<!-- Modal.Svelte -->
<script>
    let showModal = true;
</script>

{#if showModal}
<div class="backdrop">
    <div class="modal">
        <p>Special offer now!</p>
    </div>
</div>
{/if}

<style>

</style>
```

```svelte
<!-- App.svelte -->
<script lang="ts">
	import Modal from './Modal.svelte'
</script>

<Modal />

<main>
	<h1>This is my Application</h1>
</main>
```

## Styling

Use global.css to style element globally. Then, use style tag in the component to locally style each component.

You can do conditional styling with `class:` attribute. If the result is true, class name will be applied in the element.

```svelte
<script>
    let showModal = true;
    let isSpecial = true;
</script>

{#if showModal}
<div class="backdrop" class:special={isSpecial}>
    <div class="modal">
        <p>Special offer now!</p>
    </div>
</div>
{/if}

<style>
    .backdrop {
        width: 100%;
        height: 100%;
        position: fixed;
        background: rgba(0,0,0,0.8);
    }
    .modal {
        padding: 10px;
        border-radius: 10px;
        max-width: 400px;
        margin: 10% auto;
        text-align: center;
        background: white;
    }

    .special {
        background: rgba(0,0,0,0.1);
    }
</style>
```

## Props

Svelte send props to component like React.

```svelte
<!-- App.svelte -->
<Modal message="Thank you for visiting our website!"/>
```

```svelte
<!-- Modal.svelte -->
<script>
    export let message = 'default message';
</script>

<div class="backdrop">
    <div class="modal">
        <p>{message}</p>
    </div>
</div>

```

## Event Handler

### Event forwarding

Pass functions as props to the component to pass the event.

### Event Modifier

- once - make sure the event can only fire once
- preventDefault - prevent the default action
- self - only fires the event if the clicked element is the target

```svelte
<!-- App.svelte -->
<Modal message="Thank you for visiting our website!" {showModal} on:click={toggleModal}/>
```

Tip: `{showModal}` is a shorthand for `showModal={showModal}`

```svelte
<!-- Modal.svelte -->
<script>
    export let message = 'default message';
    export let showModal = true;
</script>

{#if showModal}
<div class="backdrop" on:click|self>
    <div class="modal">
        <p>{message}</p>
    </div>
</div>
{/if}

```
