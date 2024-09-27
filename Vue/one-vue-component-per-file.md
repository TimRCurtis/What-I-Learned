# One Vue Component Per File

Usually when you are working with Vue you will have a single Vue component per file. the file structure will typically look something like this:

```
js/
    components/
        AppButton.js

```

This is where we put the template code and add the export statement.

```js
export default {
    template: `
        <button class="bg-gray-200 hover:bg-gray-400 border rounded p-5 py-2">
            <slot />
        </button>
    `,
}
```

Now going back to the entry point of our app, we can import the component and use it in our app. We have to define the path to the component file and the name of the component. Then reference the component in the `components` property associated with the components object.

> Note: For this example we need to set the script tag to type="module" so that we can import the component without any errors.

```html
<div id="app">
    <app-button>Submit</app-button>
</div>
<script type="module">
    import AppButton from './js/components/AppButton.js';

    let app = {
        components: {
            'app-button': AppButton
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```