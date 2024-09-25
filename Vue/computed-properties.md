# Computed Properties

Continuing the example from list.md we currently can check the boxes as we complete the assignments, but nothing happens except that we are tracking if the assignments complete proprty is true or fasle.

This is where computed properties comes into play. For this example, we want the items that we complete to move to a new list of completed assignments.

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

All we do is just copy the Assignments section and add it underneath but change the name to Completed and the original assignments to In Progress. Then we can use the `filter` method to filter the completed assignments. This will check to see if the assignment data complete property is set to true and will show it in the completed section.

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