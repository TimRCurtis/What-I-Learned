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

Now we want the items that we complete to move to a new list of completed assignments. All we do is just copy the Assignments section and add it underneath but change the name to Completed and the original assignments to In Progress. Then we can use the `filter` method to filter the completed assignments. This will check to see if the assignment data complete property is set to true and will show it in the completed section.

```html
<div id="app">
    <section>
        <h2>In Progress</h2>

        <ul>
            <li v-for="assignment in assignments">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>

    <section>
        <h2>Completed</h2>

        <ul>
            <li v-for="assignment in assignments.filter(a => a.complete)">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>
</div>
```

Right now when we check an assignment in the In Progress section, it stays in the In Progress section. We need to update the data to reflect the change. To so this we can just copy the filter method and negate it. This will only show the assignments that are not completed.

```html
<div id="app">
    <section>
        <h2>In Progress</h2>

        <ul>
            <li v-for="assignment in assignments.filter(a => ! a.complete)">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>

</div>
```

Next we need to add a `:key=""` property to both In Progress and Completed sections so that Vue knows how to update the data. Usually the data is most likely stored in a database and the key could be the id of the assignment. In this example we can add an id to each assignment and use that as the key.

```html
<div id="app">
    <section>
        <h2>In Progress</h2>

        <ul>
            <li v-for="assignment in assignments.filter(a => ! a.complete)" :key="assignment.id">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>

    <section>
        <h2>Completed</h2>

        <ul>
            <li v-for="assignment in assignments.filter(a => a.complete)" :key="assignment.id">
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
                    { name: 'Finish project', complete: false, id: 1},
                    { name: 'Read chapter 4', complete: false, id: 2},
                    { name: 'Turn in homework', complete: false, id: 3}
                ]
            }
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

Now the app is updating the data as we check and uncheck the boxes. This is a good start but we can do better. We can use conditionals to only render each section if there are any assignments in that section. That is in the Conditionals.md file.