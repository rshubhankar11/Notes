# React.js Props

## Props Overview

Props (short for properties) are a way to pass data from a parent component to a child component in React.js. They allow you to make components dynamic and reusable by providing values that can be customized each time the component is used.

### Passing Props

Props are passed as attributes to a component in JSX. Inside the component, you can access props using the `props` object.

Example:

```jsx
// ParentComponent.js
import React from "react";
import ChildComponent from "./ChildComponent";

function ParentComponent() {
  const greeting = "Hello";
  const name = "Alice";

  return <ChildComponent greeting={greeting} name={name} />;
}

export default ParentComponent;
```

```jsx
// ChildComponent.js
import React from "react";

function ChildComponent(props) {
  return (
    <div>
      {props.greeting}, {props.name}!
    </div>
  );
}

export default ChildComponent;
```

## Using Props

In the above example, the `greeting` and `name` values are passed as props to the `ChildComponent`.

When `ParentComponent` renders `ChildComponent`, the values are dynamically inserted into the component.

## Default Props

You can also define default values for props using the `defaultProps` static property.

Example:

```jsx
import React from "react";

function Welcome(props) {
  return <h1>{props.message}</h1>;
}

Welcome.defaultProps = {
  message: "Welcome to React!",
};

export default Welcome;
```

## Props Validation

React provides a way to validate the type and presence of props using the `prop-types` library.

Example:

```jsx
import React from "react";
import PropTypes from "prop-types";

function Person(props) {
  return (
    <p>
      {props.name} is {props.age} years old.
    </p>
  );
}

Person.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
};

export default Person;
```

## Conclusion

Props are a fundamental concept in React.js that allow you to customize and pass data between components. They are essential for creating reusable and dynamic components, enhancing the flexibility and modularity of your application.

For more information on props and their usage, refer to the official [React documentation on props](https://reactjs.org/docs/components-and-props.html).

## Interview Questions on React Props and Prop Drilling

Here are some important interview questions related to React props and prop drilling, presented in Markdown (md) format:

## 1. What are props in React?

Props (short for properties) are a mechanism in React that allow data to be passed from a parent component to a child component. They are used to make components dynamic and reusable by customizing their behavior and appearance.

## 2. How are props passed to components in React?

Props are passed as attributes when rendering a component in JSX. The parent component passes data to the child component, and the child component receives the data through the `props` object.

## 3. How can you access props inside a functional component?

Inside a functional component, you can access props using the `props` parameter. For example: `function MyComponent(props) { ... }`.

## 4. Can you modify the value of props within a child component?

No, props are read-only. They cannot be modified directly within a child component. If a child component needs to modify the data, it should communicate with the parent component using callbacks.

## 5. What is prop drilling?

Prop drilling refers to the process of passing props from a higher-level component to a lower-level component through intermediary components that do not actually use the props themselves. This can lead to an unnecessary clutter of props being passed through components that don't need them, which can be less efficient and maintainable.

## 6. What is the purpose of the `defaultProps` property in a React component?

The `defaultProps` property allows you to define default values for props in case they are not provided when the component is used. This helps ensure that the component behaves predictably even if certain props are omitted.

## 7. How do you validate props in React components?

You can validate props using the `prop-types` library. By specifying prop types and their requirements, you can catch potential errors and improve the stability of your application.

## 8. What happens if a required prop is not passed to a component?

If a required prop is not passed to a component, React will show a warning in the browser's console. This helps developers identify and fix missing prop issues.

## 9. How can you set default props for a functional component?

In a functional component, you can set default props using the `defaultProps` object. For instance:

```jsx
function MyComponent(props) { ... }
MyComponent.defaultProps = { propName: 'defaultValue' };
```

## 10. Explain the difference between state and props in React.

Props are used to pass data from parent to child components and are immutable. State, on the other hand, is used to manage internal component data that can change over time. State is mutable and controlled by the component itself.

## 11. Can you change the value of props in the parent component from the child component?

No, props are read-only and should not be modified from child components. Changes to the data should be managed in the parent component, and if needed, communicated back to the child component using callbacks.

## Conclusion

Understanding how to work with props and recognizing the concept of prop drilling is crucial in React development. These interview questions cover key aspects of props and prop drilling, allowing you to showcase your knowledge and expertise during React interviews.

Remember to practice and experiment with props and prop drilling in real scenarios to gain a deeper understanding of their role in building React applications.
