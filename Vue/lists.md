# Lists

When you have items that you want to display in a list, you can create a component that will display the items. This example shows a to do list with checkboxes for when you complete each item. Now the component will be called `assignments` and we need to use an array.

Each item the array will need the name and need a way to track if the assignment has been completed. This is setup just like any other array.

```html
<div id="app">
    <section>
        <h2>Assignments</h2>

        <ul>
            <li>Finish project <input type="checkbox"></li>
            <li>Read chapter 4 <input type="checkbox"></li>
            <li>Turn in homework <input type="checkbox"></li>
        </ul>
    </section>
</div>

<script>
    let app = {
        data() {
            return {
                assignments: [
                    { name: 'Finish project', complete: false},
                    { name: 'Read chapter 4', complete: false},
                    { name: 'Turn in homework', complete: false}
                ]
            }
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

Now we can use `v-for` on the `<li>` elements to render each item in the assignments component array. We will echo out each assignment name in the assignments component inside the `{{}}` known as mustash syntax. This is how you loop through an array and display the data dynamically.

```html
<div id="app">
    <section>
        <h2>Assignments</h2>

        <ul>
            <li v-for="assignment in assignments">{{ assignment.name }}</li>
        </ul>
    </section>
</div>
```

You can see that we removed the checkbox input, but now we will add it back by putting the `{{ assignment.name }}` and the input inside a label tag.

```html
<div id="app">
    <section>
        <h2>Assignments</h2>

        <ul>
            <li v-for="assignment in assignments">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox">
                </label>
            </li>
        </ul>
    </section>
</div>
```

## v-model
Right now we don't have two way binding so nothing happens when we check the box as if we completed that assignment. To get this to work we will need to use `v-model` inside the input tag. This will bind the check status input to the `complete: false` property in the assignments component. This will update that property in real time.

> When you are working with forms and inputs you will always use `v-model` to bind them to data you have else where.

```html
<div id="app">
    <section>
        <h2>Assignments</h2>

        <ul>
            <li v-for="assignment in assignments">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>
</div>

<script>
    let app = {
        data() {
            return {
                assignments: [
                    { name: 'Finish project', complete: false},
                    { name: 'Read chapter 4', complete: false},
                    { name: 'Turn in homework', complete: false}
                ]
            }
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```