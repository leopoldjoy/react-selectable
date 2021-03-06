# Selectable items for React

Allows individual or group selection of items using the mouse or touch.

## Demo
[Try it out](http://unclecheese.github.io/react-selectable/example)

## Upgrading from 0.1
There have been significant changes in the 0.2 release. Please [read about them here](UPGRADING.md).
## Getting started
```
npm install react-selectable
```

```js
import React from 'react';
import { render } from 'react-dom';
import { SelectableGroup, createSelectable } from 'react-selectable';
import SomeComponent from './some-component';

const SelectableComponent = createSelectable(SomeComponent);

class App extends React.Component {
  
  constructor (props) {
  	super(props);
  	this.state = {
  		selectedKeys: []
  	};
  }

  render () {
    return (
      <SelectableGroup onSelection={this.handleSelection}>
        {this.props.items.map((item, i) => {
          	let selected = this.state.selectedKeys.indexOf(item.id) > -1;
          	return (
          		<SelectableComponent key={i} selected={selected} selectableKey={item.id}>
          			{item.title}
          		</SelectableComponent>
          	);
        })}
      </SelectableGroup>
    );
  },
  
  handleSelection (selectedKeys) {
  	this.setState({ selectedKeys });
  }
	
}
```
## Configuration

The `<SelectableGroup />` component accepts a few optional props:
* `onSelection` (Function) Callback fired after user completes selection
* `tolerance` (Number) The amount of buffer to add around your `<SelectableGroup />` container, in pixels.
* `component` (String) The component to render. Defaults to `div`.
* `fixedPosition` (Boolean) Whether the `<SelectableGroup />` container is a fixed/absolute position element or the grandchild of one. Note: if you get an error that `Value must be omitted for boolean attributes` when you try `<SelectableGroup fixedPosition={true} />`, simply use Javascript's boolean object function: `<SelectableGroup fixedPosition={Boolean(true)} />`.

## Extended Features

If you need extended features such as item click selection (without dragging), not clearing the previous selection at the start of a drag, or a function callback during selection, check out [react-selectable-extended](https://github.com/leopoldjoy/react-selectable-extended).