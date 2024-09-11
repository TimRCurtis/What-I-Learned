# Basic Binding & Event Handling

## Binding
We use *v-bind:* when we want to bind something to an expression. In this example, we bind the expression `buttonClasses` to the button tag which will change the text color of the button.

```html
<div id="app">
    <button v-bind:class="buttonClasses">Click Me</button>
</div>

<script>
     Vue.createApp({
         data() {
            return {
                buttonClasses: 'text-teal-400'
            };
        }
     }).mount('#app');
</script>
```

#### v-bind: Shorthand
There is a shorthand use for `v-bind:` since it tends to get used a lot. This short hand is just using the colon part.

```html
<div id="app">
    <button :class="buttonClasses">Click Me</button>
</div>
```

In this case we are binding the `class="buttonClasses"` to style the button tag, whcih lets us keep the styling the same across all button in this case. Now sometimes we don't need to do that so we just style the tag as normal.

---
## Event Handling

### Methods

We use methods for when we want something to happen when some kind of action or something else happens. The example below shows that when the button is clicked, an alert message is shown with the text "This has been toggled". We use the `v-on:click="toggle"` method and specifically the click event. Inside the click event we are telling it which expression or method we want to execute when the button is clicked.

```html
<div id="app">
    <button :class="buttonClasses" v-on:click="toggle">Click Me</button>
</div>

<script>
     Vue.createApp({
         data() {
            return {
                buttonClasses: 'text-teal-400'
            };
        },
        methods: {
            toggle() {
                alert('This has been toggled');
            }
        }
     }).mount('#app');
</script>
```
The above example is a way of writing components that was the original way all the way back in Vue 1 and it is referred to as the **Options API**.

Let's say we want to change the text color of the button when it is clicked. Using the same code from above, we will remove the alert function and replace it with `this.buttonClasses = 'text-red-600';`. This will change the text color of the button to the red color when the button is clicked, because the `v-on:click="toggle"` now changes the class styling from the original one to the new one. Currently it will not switch it back.

```html
<div id="app">
    <button :class="buttonClasses" v-on:click="toggle">Click Me</button>
</div>

<script>
     Vue.createApp({
         data() {
            return {
                buttonClasses: 'text-teal-400'
            };
        },
        methods: {
            toggle() {
                this.buttonClasses = 'text-red-600';
            }
        }
     }).mount('#app');
</script>
```

#### v-on: Shorthand
Just like `v-bind:`, there is a shorthand use for `v-on:`. It also tends to get used a lot, so the shorthand is the `@` symbol.

To have the button switch the colors everytime it is clicked we need to track if the button is active or not. By adding `active: false` in the data attribute we can then change the toggle method to switch it from *false* to *true*.

```html
<script>
     Vue.createApp({
         data() {
            return {
                buttonClasses: 'text-teal-400',
                active: false
            };
        },
        methods: {
            toggle() {
                this.active = ! this.active;
            }
        }
     }).mount('#app');
</script>
```

We then can remove the buttonClasses from the data attribute and then use the *v-bind:* with an expression that will check whether active is true or not. This will change the text color when the button is clicked.

```html
<div id="app">
    <button :class="active ? 'text-red-600' : 'text-teal-400'" @click="toggle">Click Me</button>
</div>

<script>
     Vue.createApp({
         data() {
            return {
                active: false
            };
        },
        methods: {
            toggle() {
                this.active = ! this.active;
            }
        }
     }).mount('#app');
</script>
```