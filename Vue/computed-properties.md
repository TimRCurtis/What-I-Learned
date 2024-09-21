# Computed Properties

Continuing the example from list.md we currently can check the boxes as we complete the assignments, but nothing happens except that we are tracking if the assignments complete proprty is true or fasle.

This is where computed properties comes into play. FOr this example, we want the items that we complete to move to a new list of completed assignments.

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

lorem ipsum dolor sit amet, consectet adip ex
lorem ipsum *dolor* sit amet, consectet adip

Let's start by creating an `index.html` file.