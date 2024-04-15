`React.createRef` crea un [ref](https://es.reactjs.org/docs/refs-and-the-dom.html) que puede ser adjunto a los elementos React por medio del atributo ref.

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.inputRef = React.createRef();  }

  render() {
    return <input type="text" ref={this.inputRef} />;  }

  componentDidMount() {
    this.inputRef.current.focus();  }
}
```