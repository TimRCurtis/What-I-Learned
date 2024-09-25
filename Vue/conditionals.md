# Conditionals

Continuing the example from computed-properties.md we can now check the boxes as we complete the assignments and they are added and removed from each section. Now lets add conditionals to each section so that they only appear if there are any assignments in that section.

We can do this by adding `v-if` or `v-show` to the In Progress and Completed sections.

> Note: `v-if` is a conditional that will only show the element if the expression is true. `v-show` is a conditional that will basically toggle visibility of the element.

We are going to use `v-show` in this example and copy the filter method from the computed properties example, but add `.length` to the end of the expression. The `.length` will return if there is more than 0 items in the array.

```html
<div id="app">
    <section v-show="assignments.filter(a => ! a.complete).length">
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

    <section v-show="assignments.filter(a => a.complete).length">
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

