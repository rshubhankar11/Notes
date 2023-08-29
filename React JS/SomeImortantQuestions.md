# Some Interview asked Questions:

## 1. What is HOC (Higher Order Component)?

**Ans:**
A Higher-Order Component (HOC) is a design pattern in React that involves creating a function that takes a component and returns a new component with additional functionality. HOCs are used to reuse component logic, add props, modify behavior, or wrap components with other components. They help separate concerns, promote code reusability, and enable composability.

Here's a simple example of how to create and use a Higher-Order Component in React:

```jsx
import React from "react";

// Higher-Order Component that adds a new prop to the wrapped component
function withColor(WrappedComponent, color) {
  // Return a new component that wraps the original component
  return function (props) {
    return <WrappedComponent {...props} color={color} />;
  };
}

// Component that will be wrapped with the Higher-Order Component
function TextComponent(props) {
  return <p style={{ color: props.color }}>{props.text}</p>;
}

// Wrapping the TextComponent using the withColor HOC
const ColoredText = withColor(TextComponent, "blue");

function App() {
  return (
    <div>
      <TextComponent text="Hello, world!" color="red" />
      <ColoredText text="Hello, HOC!" />
    </div>
  );
}

export default App;
```

In this example:

1. We define a Higher-Order Component `withColor` that takes a `WrappedComponent` and a `color` as parameters.
2. Inside `withColor`, we return a new function that renders the `WrappedComponent` with an additional `color` prop.
3. We create a `TextComponent` that simply displays a colored text based on the provided color prop.
4. We use the `withColor` HOC to create a new component `ColoredText` by wrapping the `TextComponent`.
5. In the `App` component, we use both the original `TextComponent` and the enhanced `ColoredText` component, demonstrating the flexibility of HOCs.

HOCs are powerful tools for enhancing and reusing component logic, but keep in mind that in modern React, Hooks and render props have become more popular alternatives for achieving similar goals while promoting better component composition.

## 2. Create a react application to increase the count on click of button and clear the count on click of button . Also add a button, to which if we click it will keep increasing the count until click Stop button ?

**ANS:**

```jsx
import React, { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);
  const [autoIncrement, setAutoIncrement] = useState(false);

  useEffect(() => {
    let interval;

    if (autoIncrement) {
      interval = setInterval(() => {
        setCount((prevCount) => prevCount + 1);
      }, 1000);
    }

    return () => clearInterval(interval);
  }, [autoIncrement]);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  const handleClear = () => {
    setCount(0);
  };

  const handleAutoIncrement = () => {
    setAutoIncrement(true);
  };

  const handleStopAutoIncrement = () => {
    setAutoIncrement(false);
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={handleIncrement}>Increment</button>
      <button onClick={handleClear}>Clear</button>
      {!autoIncrement ? (
        <button onClick={handleAutoIncrement}>Start Auto Increment</button>
      ) : (
        <button onClick={handleStopAutoIncrement}>Stop Auto Increment</button>
      )}
    </div>
  );
}

export default App;
```

In this example:

- The `count` state holds the current count value.
- The `autoIncrement` state is used to determine whether the count should automatically increase.
- The `useEffect` hook is used to set up an interval for auto-incrementing the count when `autoIncrement` is `true`.
- The `handleIncrement` function increases the count by 1.
- The `handleClear` function sets the count back to 0.
- The `handleAutoIncrement` function starts the auto-increment process.
- The `handleStopAutoIncrement` function stops the auto-increment process.
- Depending on the state of `autoIncrement`, either the "Start Auto Increment" button or the "Stop Auto Increment" button is displayed.

Copy and paste this code into your React application's entry file (usually `src/index.js` or `src/App.js`), and you should see the described functionality when you run the application.

## 3. What is Strict mode in React Js ?

**Ans:**
In React, Strict Mode is a tool that helps developers identify and address potential problems in their applications by enabling a stricter set of checks and warnings. It is not a component you render in your UI but rather a wrapper that you use to enable certain development-only features.

When you wrap your application or a part of it in a Strict Mode component, React performs additional checks and warnings to help catch common mistakes that could lead to poor performance or unexpected behavior. These checks are only enabled in development mode and are meant to provide developers with more visibility into potential issues.

Some benefits of using Strict Mode include:

1. **Identifying Unsafe Lifecycle Methods:** Strict Mode helps you identify and avoid using legacy and potentially unsafe lifecycle methods.

2. **Detecting Deprecated APIs:** It highlights the use of deprecated React APIs, encouraging you to use the latest recommended alternatives.

3. **Preventing Side Effects During Rendering:** It helps catch side effects that are invoked during rendering, which can lead to performance problems.

4. **Warning About Legacy String Refs:** Strict Mode warns against using string refs, which are considered legacy and less reliable.

To use Strict Mode, you can wrap your entire application or just specific components with it. Here's how you can enable Strict Mode in your application:

```jsx
import React from "react";
import ReactDOM from "react-dom";

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);
```

In this example, the `<React.StrictMode>` wrapper is applied around the root component (`<App />`). This will activate the development checks and warnings for the entire application.

Remember that Strict Mode checks are only performed in development mode and are meant to help you catch potential problems early on. Once your application is ready for production, you can remove the Strict Mode wrapper for the final build.
