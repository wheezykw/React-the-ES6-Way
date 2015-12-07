# Component constructors and state

In React, props are immutable. Meaning you can't change the value of the props
once the component is created. So how do we got about creating dynamic UI's
that change? We use state. State is what represents what your application
UI looks like at any given moment. We define the initial state of our component
inside the constructor. What's a constructor?!?!?! It's the "initialize"
function for the class. Any time a new instance of the class is created, the
constructor is called and passed in any properties that are given during
initialization.
```es6
export default class Component extends React.Component {
  constructor(props) {
    super(props)

    this.state = props
  }
}
```

What's going on here? Every React component is initialized with props. So when
you create a component using JSX like this:
```jsx
<Component
  foo='bar'
  bar='baz'
/>
```

The constructor of that `Component` class receives a JavaScript object literal
that looks like this:
```json
{
  foo: 'bar',
  bar: 'baz'
}
```

The other thing you may find strange is the `super` function call. What this
does is it tells the class to call the inherited classes (in this case, the
React.Component) constructor function with the arguments you give it. When
using inherited classes it is require that the super method (if being called)
be called before anything else in the constructor. So here we're just passing
off the props to React and letting React do what it normally does with them.
In this case React will assign them to `this.props`. In this contrived example
we're also assigning the state of the application to the props.

Now let's open up our `ReadingTime` component and add the following
constructor:
```es6
constructor(props) {
  super(props)

  this.state = {
    readTime: 0
  }
}
```

For reference, your `ReadingTime` component should now look like this:
```es6
import React from 'react'

export default class ReadingTime extends React.Component {
  static propTypes = {
    wordsPerMinute: React.PropTypes.number
  }

  static defaultProps = {
    wordsPerMinute: 270
  }

  constructor(props) {
    super(props)

    this.state = { readTime: 0 }
  }

  render() {
    return (
      <div>Hello ReadingTime!</div>
    )
  }
}
```

Excellent! We've created another component! Let's open up our main application
component and add this component to our app. Open up `example/react-reading-time.jsx`
and import our component:
```es6
import ReadingTime from '../src/reading-time'
```

Ok now let's add this component to our view. We'll also add some classes,
a textarea for writing an article and some default text to put into the textarea.
Let's just rewrite the entire render function like this:
```es6
render() {
  let defaultText = 'Foo is baz and bar'

  return (
    <div className='container' style={{ marginTop: '50px' }}>
      <div data-article className='col-lg-8 col-lg-offset-2 form-group'>
        <textarea
          defaultValue={defaultText}
          className='form-control'
          style={{ height: '500px', resize: 'none' }}>
        </textarea>
      </div>
      <ReadingTime className='col-lg-2 well' />
    </div>
  )
}
```

Woohoo! We've got our component set to render inside of our main application
page along with a text area. You'll notice a few things I did there that
may seem strange. The first one is adding a data attribute to the div that
holds the textarea. I did this so that later on down the road our `ReadingTime`
component will have a way to know which container to get the word count from.

I also added a style attribute to the element, but it doesn't look like a normal
style tag that you would add to an HTML. Remember when we talked about JSX,
and how it's really just JavaScript? Because of that, we have to give the
style tag a regular old JavaScript object to work with, which it can then
turn into the proper style tag when rendering the DOM.

Another attribute that was added to the `textarea` that is JSX specific is
the `defaultValue` attribute. React has the notion of `Controlled` and
`Uncontrolled` components. When the `value` attribute is set on any type of
input, it becomes a controlled component, and the value of that input will
**always** be that value. User interaction will have no effect on it. The only
way to change the value is through an event handler. In our case, we just
wanted to set the initial value of the input, which is why we used the
`defaultValue` attribute instead of the `value` attribute. When there is no
`value` set on an input, it is an uncontrolled component.

Let's fire up the server again with `npm start` and visit `localhost:8881/example`
and see what we've created so far! It's getting more and more exciting by the
minute!

## Next lesson...

Next we're going to dive into the Virtual DOM and find out how it is that
React is so good at updating the UI based on the state of the component.
