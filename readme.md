# The Virtual DOM

So up until now you may have been wondering how React can possibly manage
to update the state of your components? You may have also heard of this
magical sounding thing called the Virtual DOM. Well the Virtual DOM is how
React works it's magic.

Imagine looking at all of the HTML markup on your page, and being able to
just take a snapshot of it in your memory, and just know when any little piece
of it has changed. That's essentially what the Virtual DOM is.

When your application is initially rendered into the DOM, with it's initial
state, React takes a "snapshot" of this and holds it in memory. This is the
Virtual DOM.

Any time a DOM update is triggered, React updates the Virtual DOM to reflect
the new state of the app. It then does what's called a DOM diff, and selects
only the pieces the DOM that have changed. It compares the Virtual DOM, with
the actual DOM, and only updates the parts of the DOM that have changed.

This makes updating the application state extremely fast and efficient, as
we do not have to update the entire page to reflect the new state of the app.
Also, we, as developers, do not have to programatically get the reference to
the DOM node that needs to be updated, and then perform the update ourselves.
We simply change a variable in the state tree and let React do all the work
for us.

## Putting it into practice

Ok awesome. This is great. But let's see it in action. Do you remember when
we created the constructor for our component in the last lesson? We set
the initial state of the app:
```es6
this.state = {
  readTime: 0
}
```

Let's use that state to display something in our widget. Update the render
method of your `ReadingTime` component to look like this:
```es6
render() {
  return (
    <div>
      <p>
        Estimated Read Time:<br /><br />
        <span>{this.state.readTime}</span>
      </p>
    </div>
  )
}
```

For the purposes of demonstration, let's go ahead and add a simple input to
our `ReadingTime` component:
```es6
render() {
  return (
    <div>
      <p>
        Estimated Read Time:<br /><br />
        <span>{this.state.readTime}</span>
        <input type='number' onChange={this.updateReadTime) />
      </p>
    </div>
  )
}
```

We've added a number input here so that we can update the `readTime` state
variable, and we've added an `onChange` handler to the input. Let's implement
that function. Add this just above the `render` function:
```es6
updateReadTime = (ev) => {
  this.setState({ readTime: ev.target.value })
}
```

This is just a simple function that updates the `state` of our component to
reflect the new value of the input. We'll explore event handlers and changing
state in more depth in Lesson 4, but for now you can quickly see how React
handles changes in component state and updates the DOM automagically.

You can go ahead and remove the number input and the `updateReadTime` function
from the `ReadingTime` component, we only used those for demonstration purposes.

## Next lesson...
We've learned about the Virtual DOM and how React uses it to manage state
changes in the app quickly and efficiently. Let's move on now and finish up our
reading time component.
