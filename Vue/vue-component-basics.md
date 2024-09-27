# Vue Component Basics

We weant to create a custom component which we can either register globally or locally to parent components.

Some examples of Vue components are:

- A component that displays a list of items
- A component that displays a form
- A component that displays a button

For this example we will take the code from computed-properties.md and create some custom components.

> Note: The compoent object takes the same kind of data as the app object like data, methods, computed, etc.

```html
<script>
    let app = {
        components: {
            'app-button': {},
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

Lets take this component and say when it is mounted, an alert will pop up saying "Hello".

```html
<script>
    let app = {
        components: {
            'app-button': {
                mounted() {
                    alert('Hello');
                }
            },
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

Once we have registered the component, we can use it in our app by using the component name, ie `<app-button></app-button>`. These custom components are how we can tuck away markup, behavior, and logic into reusable components. This is how we can have certain compents to have the same CSS across the app.

```html
<div id="app">
    <app-button></app-button>
</div>

<script>
    let app = {
        components: {
            'app-button': {
                mounted() {
                    alert('Hello');
                }
            },
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

## Templates

To style the component we can use the `template` property. This is where we can put the HTML and CSS for the component. 

> Note: I'm using Tailwind to style the button.

```html
<script>
    let app = {
        components: {
            'app-button': {
                template: `
                    <button class="bg-gray-200 hover:bg-gray-400 border rounded p-5 py-2">Click Me</button>
                `,
            },
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

We can now reference the button component in our app as many times as we want. Each one is like it's own instance. We also don't want to hard code the text for this button so we need to use slots.

## Slots

Slots are a way to pass data to a component. This lets us create reusable components that can be used in different places in our app and not have to hard code any content or data.

To use slots we need to add a `<slot />` tag to the component where we want data to be passed to.

```html
<div id="app">
    <app-button>Submit</app-button>
</div>
<script>
    let app = {
        components: {
            'app-button': {
                template: `
                    <button class="bg-gray-200 hover:bg-gray-400 border rounded p-5 py-2">
                        <slot />
                    </button>
                `,
            },
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```