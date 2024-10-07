# Handle a Form Submission

Here is a simple form that will add a new assignment to the list of assignments. We can use the `v-on` directive to listen for the form submit event and then add the new assignment to the assignments array. This will be in the form tag. We use `@submit="add"` where we are calling the add method in the methods object.

```html
<form @submit="add">
    <div>
        <input placeholder="New Assignment" />
        <button type="submit">Add</button>
    </div>
</form>
```

We don't just want the form to submit like normal since the page will reload. We need to have the add method prevent the default action of the form submit event. This is done by adding `event.preventDefault()` to the add method and using `add(e)`.

``` javascript
methods: {
    add(e) {
        e.preventDefault();
    }
}
```

This way of preventing the default action of the form submit event is a good way to handle form submissions, but since it is very common to do this there is another way to do it. Vue added a `.prevent` modifier to the `v-on` directive. This will prevent the default action of the event.

```html
<form @submit.prevent="add">
    <div>
        <input placeholder="New Assignment" />
        <button type="submit">Add</button>
    </div>
</form>
```

Now we need to grab what the user entered in the input and add it to the assignments array. Let's do this by leverage the `v-model` directive. Then we need to bind it to the correct input tag.

``` javascript
data() {
    return {
        newAssignment: ''
    }
}
```
```html
<form @submit.prevent="add">
    <div>
        <input v-model="newAssignment" placeholder="New Assignment" />
        <button type="submit">Add</button>
    </div>
</form>
```

Now that we have the new assignment in the data, we can add it to the assignments array. We can do this by using the `push` method on the assignments array.

```javascript
methods: {
    add() {
        this.assignments.push({
            name: this.newAssignment,
            complete: false,
            id: this.assignments.length + 1
        });
    }
}
```

What happens now is that when the user submits the form, the `add` method is called and the new assignment is added to the assignments array. Vue will see the new assignment and update the DOM to show the new assignment in the list as well as the app.

Right now the last thing to do is reset the new assignment input. Right now when the user adds a new assignment, the input will still have the new assignment in it. To have it reset after the user submits the form, we can update the `add` method to reset the input by having the newAssignment property set to an empty string.

```javascript
methods: {
    add() {
        this.assignments.push({
            name: this.newAssignment,
            complete: false,
            id: this.assignments.length + 1
        });

        this.newAssignment = '';
    }
}
```