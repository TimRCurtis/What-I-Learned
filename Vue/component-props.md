# Component Props

> Note: This is some quick housekeeping by turning the `let app {}` into its own component file. The new file is called `App.js`.

```html
<div id="app">
    <app-button>Submit</app-button>
</div>
<script type="module">
    import App from './js/components/App.js';

    Vue.createApp(App).mount('#app');
</script>
```

Back to Component Props. For this example we will add a prop to the button component. Normally you will have different styles for different types of buttons. For example, a primary button will be blue and a secondary button will be green. To do this we need to go to the AppButton.js file and add a `props` object to the component. Then  we can add the `type` prop and set it to a string.

```js
export default {
    template: `
        <button class="bg-gray-200 hover:bg-gray-400 border rounded p-5 py-2">
            <slot />
        </button>
    `,

    props: {
        type: String
    },
}
```

Next in our index.html file we can add a `type` attribute to the button component. This is where we can set the type to be any string like "primary" or "secondary".

```html
<div id="app">
    <app-button type="primary">Submit</app-button>
</div>
<script type="module">
    import App from './js/components/App.js';

    Vue.createApp(App).mount('#app');
</script>
```

We can even set a default value for the type prop. This will be used if the prop is not passed to the component.

```js
export default {
    template: `
        <button class="bg-gray-200 hover:bg-gray-400 border rounded p-5 py-2">
            <slot />
        </button>
    `,

    props: {
        type: {
            type: String,
            default: 'primary'
        }
    },
}
```

When setting class bindings, you can use a string, an array, or an object. We are going to use the object syntax. So we first bind the class property and put all the classes inside of `{}` with a key.

```js
export default {
    template: `
        <button 
            :class="{
                'bg-gray-200 hover:bg-gray-400 border rounded p-5 py-2': true
            }">
            <slot />
        </button>
    `,

    props: {
        type: {
            type: String,
            default: 'primary'
        }
    },
}
```

Now for this button we can set the padding, border radius, and border as default while setting the the different colors for the primary and secondary types.

```js
export default {
    template: `
        <button 
            :class="{
                'border rounded p-5 py-2': true,
                'bg-gray-200 hover:bg-gray-400': type === 'primary',
                'bg-blue-200 hover:bg-blue-400': type === 'secondary'
            }">
            <slot />
        </button>
    `,

    props: {
        type: {
            type: String,
            default: 'primary'
        }
    },
}
```

We can now configure the style of the button based on an incoming prop value. If we need to access a prop, we refernce the name. If we need to access a data property, we refernce the name.