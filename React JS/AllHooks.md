# React Hooks Cheat Sheet

React hooks are functions that allow you to use state and other React features without writing a class.

## 1. useState

### Usage:

`useState` is used to manage state in functional components.

### Example:

```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

## 2. useEffect

### Usage:

`useEffect` is used to perform side effects in functional components.

### Example:

```jsx
import React, { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetchData().then((result) => {
      setData(result);
    });
  }, []);

  return (
    <ul>
      {data.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}
```

## 3. useContext

### Usage:

`useContext` is used to access the context within a functional component.

### Example:

```jsx
import React, { useContext } from "react";

const ThemeContext = React.createContext("light");

function ThemeComponent() {
  const theme = useContext(ThemeContext);

  return <div>Current Theme: {theme}</div>;
}
```

## 4. useRef

### Usage:

`useRef` is used to hold a mutable reference to a DOM element or a value that doesn't trigger re-renders.

### Example:

```jsx
import React, { useRef, useEffect } from "react";

function AutoFocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} />;
}
```

## 5. useMemo

### Usage:

`useMemo` is used to memoize expensive computations in functional components.

### Example:

```jsx
import React, { useMemo } from "react";

function ExpensiveComponent({ list }) {
  const sum = useMemo(() => {
    console.log("Computing sum...");
    return list.reduce((acc, item) => acc + item, 0);
  }, [list]);

  return <div>Sum: {sum}</div>;
}
```

## 6. useCallback

### Usage:

`useCallback` is used to memoize functions to prevent unnecessary re-renders.

### Example:

```jsx
import React, { useCallback, useState } from "react";

function ParentComponent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent increment={increment} />
    </div>
  );
}
```

## 7. useReducer

### Usage:

`useReducer` is used to manage complex state logic that involves multiple actions.

### Example:

```jsx
import React, { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>Increment</button>
      <button onClick={() => dispatch({ type: "decrement" })}>Decrement</button>
    </div>
  );
}
```

## 8. useLayoutEffect

### Usage:

`useLayoutEffect` is similar to `useEffect`, but it runs synchronously after all DOM mutations.

### Example:

```jsx
import React, { useLayoutEffect, useState } from "react";

function MeasureElement() {
  const [width, setWidth] = useState(0);

  const measureWidth = () => {
    setWidth(ref.current.clientWidth);
  };

  const ref = useRef(null);

  useLayoutEffect(() => {
    measureWidth();
    window.addEventListener("resize", measureWidth);

    return () => {
      window.removeEventListener("resize", measureWidth);
    };
  }, []);

  return <div ref={ref}>Width: {width}px</div>;
}
```

## 9. useImperativeHandle

### Usage:

`useImperativeHandle` customizes the instance value that is exposed when using `ref` with `forwardRef`.

### Example:

```jsx
import React, { useRef, useImperativeHandle, forwardRef } from "react";

const CustomInput = forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
    // Other methods...
  }));

  return <input ref={inputRef} />;
});

function ParentComponent() {
  const customInputRef = useRef();

  const handleButtonClick = () => {
    customInputRef.current.focus();
  };

  return (
    <div>
      <CustomInput ref={customInputRef} />
      <button onClick={handleButtonClick}>Focus Input</button>
    </div>
  );
}
```

## 10. useDebugValue

### Usage:

`useDebugValue` is used to display custom labels for custom hooks in React DevTools.

### Example:

```jsx
import React, { useDebugValue, useState } from "react";

function useCustomCounter(initialCount) {
  const [count, setCount] = useState(initialCount);
  useDebugValue(`Count: ${count}`);

  return [count, setCount];
}
```

## 11. useMediaQuery

### Usage:

`useMediaQuery` is used to track changes in media queries.

### Example:

```jsx
import React from "react";
import { useMediaQuery } from "react-responsive";

function ResponsiveComponent() {
  const isMobile = useMediaQuery({ maxWidth: 767 });

  return <div>{isMobile ? "Mobile" : "Desktop"}</div>;
}
```

## 12. useSWR (from SWR library)

### Usage:

`useSWR` is a data-fetching hook for managing remote data fetching and caching.

### Example:

```jsx
import React from "react";
import useSWR from "swr";

function DataFetcher() {
  const { data, error } = useSWR("/api/data", fetch);

  if (error) return <div>Error loading data</div>;
  if (!data) return <div>Loading...</div>;

  return <div>Data: {data}</div>;
}
```

## 13. useLocation (with react-router)

### Usage:

`useLocation` is used to access the current URL location in a React Router application.

### Example:

```jsx
import React from "react";
import { useLocation } from "react-router-dom";

function CurrentLocation() {
  const location = useLocation();

  return <div>Current Location: {location.pathname}</div>;
}
```

---
