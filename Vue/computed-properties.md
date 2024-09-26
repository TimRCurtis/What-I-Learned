# Computed Properties

Continuing the example from conditionals.md we can now check the boxes as we complete the assignments and they are added and removed from each section. Now lets make this a lttle better by adding computed properties.

We can take the line `assignments.filter(a => a.complete)` in the completed section and and replace it with `completedAssignments`. Also change it in the ul tag where the `v-for` is.

```html
<div id="app">
    <section v-show="completedAssignments.length">
        <h2>Completed</h2>

        <ul>
            <li v-for="assignment in completedAssignments" :key="assignment.id">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>
</div>
```

Now down in our app, we can add computed property after the data property. Then use the filter method we did have that we replaced with completedAssignments. This will be our first computed property.

> Note: we can still access the assignments data in the computed property since Vue is proxying it behind the scenes.

```html
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
        },

        computed: {
            completedAssignments() {
                return this.assignments.filter(assignment => assignment.complete);
            }
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```

We can do the same thing for the In Progress section. We will just copy the completedAssignments computed property and change the name to inProgressAssignments. Also, make sure that the filter method is the opposite of the completedAssignments filter method by adding a `!` in front of the `assignment.complete` and replaceing the filter in the ul tag under the In Progress section with `inProgressAssignments`.

```html
<div id="app">
    <section v-show="inProgressAssignments.length">
        <h2>In Progress</h2>

        <ul>
            <li v-for="assignment in inProgressAssignments" :key="assignment.id">
                <label>
                    {{ assignment.name }}

                    <input type="checkbox" v-model="assignment.complete">
                </label>
            </li>
        </ul>
    </section>
    <section v-show="completedAssignments.length">
        <h2>Completed</h2>

        <ul>
            <li v-for="assignment in completedAssignments" :key="assignment.id">
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
        },

        computed: {
            inProgressAssignments() {
                return this.assignments.filter(assignment => ! assignment.complete);
            },
            completedAssignments() {
                return this.assignments.filter(assignment => assignment.complete);
            }
        }
    };

    Vue.createApp(app).mount('#app');
</script>
```