# Computed Properties

Continuing the example from conditionals.md we can now check the boxes as we complete the assignments and they are added and removed from each section. Now lets make this a lttle better by adding computed properties.

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