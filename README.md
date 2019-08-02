# jsx-simple-state
State management (hopefully) made simple.

## Motivation
You probably don't always need to use Redux or React Context API and wrapping your Consumer inside your Provider, or is it the other way around? 🤷‍♂️

For simpler applications you might just want a K.I.S.S. approach 🤔(did he just called me stupid?)

# How to do it?
You can create your state somewhere (well, maybe at the application level to look profesh)! 
Once that's out of the way, you can change it from anywhere in your app regardless of component hierarchy. 🎉🎉🎉
Once the state changes, any component subscribing to it will get a prop updated.

For example, lets say we want to create a property that stores a "theme", how does that look?

## Example

1) Create your initial state
```javascript
import { h, render } from 'preact';
import { State } from "jsx-simple-state";
import SomeButton from './button';
import SomePage from './page';

// define a prop for a "theme"
State.theme = 'dark';

function App() {
  return (
    <div>
      <h1>Howdy</h1>
      <SomeButton />
      <SomePage />
    </div>
  );
}

render(<App />, document.querySelector('body'), document.querySelector('#app'));
```

2) Lets fill that SomeButton class shall we?
```javascript
import { h } from 'preact';
import { State } from 'jsx-simple-state';

export function SomeButton() {
  return (
    <button onPointerDown={() => { State.theme = 'light'; }}>Light Theme</button>
  );
}
```

3) All we need is to complete that SomePage and decorate it with a Consumer specifying the prop we want to subscribe to changes
```javascript
import { h, Component } from 'preact';
import { withConsumer } from 'jsx-simple-state';

class SomePage extends Component {
  render() {
    return (
      <p>The selected theme is {this.props.theme}</p>
    );
  }
}

export default withConsumer(['theme'])(SomePage);
```

And thats it!
