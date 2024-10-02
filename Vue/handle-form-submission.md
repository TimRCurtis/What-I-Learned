# Handle a Form Submission

Here is a simple form that will add a new assignment to the list of assignments. We can use the `v-on` directive to listen for the form submit event and then add the new assignment to the assignments array. This will be in the form tag. We use `@submit="add"`

```html
<form>
    <div>
        <input placeholder="New Assignment" />
        <button type="submit">Add</button>
    </div>
</form>
```