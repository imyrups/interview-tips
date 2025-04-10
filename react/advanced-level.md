### Advanced level questions

## How does React's reconciliation algorithm work?
React’s reconciliation algorithm, also known as "diffing," is responsible for efficiently updating the DOM when the state or props of a component change. The algorithm works by comparing the new Virtual DOM with the previous one (a process called "diffing"). Here’s how it works:

1. Two Types of Updates:
   
  - `Reconciliation`: When a component’s state or props change, React creates a new Virtual DOM and compares it with the old one to figure out what changed.
    
  - `Keyed Updates`: React uses the key attribute in lists to optimize updates by identifying which items in a list were added, removed, or reordered.

2. Batched Updates: React batches updates to minimize the number of renders. Instead of updating the DOM every time state or props change, React groups the changes together and processes them in a single render cycle.

3. Efficient Diffing: React only compares elements with the same type. If two components have different types, React completely replaces the component. If the types are the same, React performs a shallow comparison of props and state to decide what needs to be updated.

##  How does the Context API differ from Redux? When would you choose one over the other?
Both the Context API and Redux are used for state management in React, but they have different use cases:

    - Context API:
  
       - The Context API is a built-in React feature for passing data through the component tree without having to manually pass props at every level.
       
       - Ideal for low-to-moderate complexity state management, such as themes, authentication, language preferences, etc.
       
       - Can lead to performance issues if used for frequently changing state since it triggers re-renders for all components that consume the context.
       
    - Redux:
    
       - Redux is a more complex and flexible library for managing application state, often used for more global state management in large applications.
       
       - Uses a centralized store and provides middleware for handling asynchronous actions (e.g., Redux Thunk, Redux Saga).
       
       - Redux is more suited for complex state logic, especially in large-scale applications where actions need to be dispatched from various components, and side effects need to be handled.

When to use Context API:
    For small to medium-sized apps with shared data like themes, authentication, and settings.

When to use Redux:
    For larger applications with complex state logic, actions, reducers, and middleware (such as for handling async operations like data fetching).


## What is Server-Side Rendering (SSR) in React? How does it differ from Client-Side Rendering (CSR)?

Server-Side Rendering (SSR):
  - SSR involves rendering the React application on the server and sending a fully rendered HTML page to the client.
  - The initial load of the page is fast, as the HTML is already generated on the server.
  - After the page is loaded, React takes over to handle client-side interactions (this is known as hydration).
  
  Benefits:
    - SEO-friendly: Since the content is pre-rendered, search engines can easily crawl and index the page.
    - Faster initial load: The browser receives fully rendered HTML, reducing the time to first meaningful paint.
  
  Example of SSR setup:
    - Next.js is a popular framework for SSR in React.

Client-Side Rendering (CSR):
  - CSR involves rendering the React application entirely on the client side using JavaScript. Initially, the server sends a minimal HTML file and loads the necessary JavaScript to render the UI.
  - The content is rendered in the browser, and React manages the UI updates.
  
  Benefits:
    - Rich Interactivity: Since the rendering happens on the client-side, the UI can be highly interactive without the need for full page reloads.
    - Faster subsequent navigation: Since the app has already been loaded, navigating between pages is fast.
  
  Example of CSR:
    - Create React App is an example of a CSR setup.

SSR vs CSR:
    - SSR is better for SEO and initial load performance but can be more complex to set up.
    - CSR is better for dynamic web apps where interactivity is prioritized, and SEO is not a concern.

## What are some common performance optimization techniques in React?
- Memoization:
    - Use React.memo to prevent unnecessary re-renders of functional components when their props don’t change.
    - Use useMemo to memoize expensive computations.
    - Use useCallback to memoize functions that are passed as props to child components, preventing unnecessary re-renders.
- Lazy Loading:
    - Split your code into smaller bundles using React.lazy() and Suspense, so only the components needed for the current view are loaded.
- Virtualization:
    - Use libraries like react-window or react-virtualized to render only the visible elements in large lists, improving performance for long lists or tables.
- Avoid Inline Functions:
    - Inline functions or objects passed as props to child components can cause unnecessary re-renders. Use useCallback or move the function outside the render method.
- ShouldComponentUpdate / PureComponent:
    - Use shouldComponentUpdate in class components or PureComponent to avoid re-renders for props that haven't changed.
Use of Web Workers:
    - For expensive tasks like image processing or computations, offload the work to web workers to keep the UI thread free.
Avoiding Large React Trees:
    - Keep your component tree shallow and avoid deeply nested components where possible to reduce the overhead of reconciliation.

## What is React Concurrent Mode, and how does it improve performance?

- React Concurrent Mode is an experimental feature that allows React to work on multiple tasks at the same time. It makes rendering more efficient by breaking the rendering work into smaller chunks and spreading it out over time.
    - Prioritizing UI Updates: With Concurrent Mode, React can prioritize urgent tasks like animations and interactions, ensuring that users always experience smooth and responsive UIs.
    - Interruptible Rendering: If there is a higher priority update (e.g., a user interaction), React can interrupt the current render to handle that update and then resume the previous one.
    - Suspense for Data Fetching: In Concurrent Mode, Suspense is used not just for lazy loading components but also for data fetching. It can pause rendering until the necessary data is ready, showing loading states while waiting for the data.

- Benefits of Concurrent Mode:
    - Improved User Experience: By rendering UI updates in smaller chunks, Concurrent Mode allows for smoother transitions and avoids blocking the main thread, leading to a more responsive app.
      
    - Better Handling of Delays: UI updates that would normally be blocked due to expensive operations (like network requests) are handled more gracefully, reducing janky interactions.

## Explain the concept of "Render Props" in React. How is it different from higher-order components (HOCs)?

Render Props is a pattern where a component takes a function as a prop and calls that function with its own state or other data. 

The function returns a JSX element, allowing the parent to define how the component's state is rendered.

Differences from Higher-Order Components (HOCs):
    - Render Props passes a function that returns JSX, allowing more flexible and dynamic control over how data is rendered.
    
    - HOCs are functions that take a component and return a new component with additional props. HOCs are typically used for adding common functionality to multiple components (e.g., adding authentication or data fetching logic).
    
    - Render Props are generally more flexible and can work with components that need to be controlled by the parent.


##  What is "Reconciliation" in React, and how does it optimize rendering performance?

Reconciliation is the process by which React determines how to update the DOM based on changes to the component's state or props. It compares the old Virtual DOM with the new one and applies the minimal set of changes to the actual DOM, optimizing performance.

Key Points in Reconciliation:
    - Keyed Updates: React uses keys to identify elements in a list and efficiently update only the changed elements.
    
    - Shallow Comparison: React compares components at a shallow level. If the type of a component has changed, React will discard the previous tree and render the new one from scratch.
    
    - Batched Updates: React batches multiple updates together to reduce the number of re-renders, improving performance.


## Explain the concept of “Error Boundaries” in React. How do they work, and how do they differ from try/catch blocks?

Error Boundaries are React components that catch JavaScript errors in their child component tree, log those errors, and display a fallback UI instead of crashing the entire app. Error boundaries prevent the whole React component tree from crashing when a JavaScript error occurs.

    - How They Work: Error boundaries implement componentDidCatch(error, info) or the static getDerivedStateFromError() lifecycle methods to handle errors.

    - Fallback UI: You can render a custom fallback UI when an error occurs in the child component.

Difference from try/catch:
    
    - try/catch is used to handle errors in functions or code blocks, while Error Boundaries are specific to handling errors in React component rendering and lifecycle methods. They cannot catch errors in event handlers or asynchronous code.


## Performance ptimization in react?
It can be optimised at mutiple levels:
   - Bundler Level: minify js, css
   - Assets level:
   - CDN / Server level:
   - Rendering comp faster:

## How do we do assest optimization in react?  


## How do we effective do Code splitting, Chuking in react?


## How do you handle Role Based Access Control? or Procted Routes?


## How do you handle Sites where Loading icons is strictly restricted? (Shimmer UI)


## How do you make sure styles from one component does not affect other component? or vice versa have some shared styles?


## How do you make sure the react application accessibility compliant?


## How do you make sure the security in react app?


## What are some of the design patterns used in react o share logic and organize components more effectively?

1. Render Props Pattern:
      - A render prop is a technique for sharing code between React components using a function that returns a React element.

2. Container / Presentational Pattern (Smart/Dumb Components):
      - This is about separating logic from UI. The idea is to isolate the data-fetching/state-management logic (container) from the UI layout (presentational).

3. Higher-Order Components (HOC):
      - A function that takes a component and returns a new component with added behavior.
  
4. Hooks Pattern (Modern React):
      - With React hooks, especially useState and useEffect, you can share logic through custom hooks instead of HOCs or render props. 


## What are error boundaries and how is that implemented?

## What is an Error Boundary?

An **Error Boundary** is a React component that catches JavaScript errors in the **component tree below it** and displays a **fallback UI** instead of crashing the entire app.

# ✅ It catches:
- Rendering errors
- Lifecycle errors
- Constructor errors of child components

# ❌ It doesn't catch:
- Errors in event handlers
- Asynchronous code (e.g., `setTimeout`)
- Server-side rendering errors
- Errors inside the error boundary itself

---

# 🛠️ How to Implement an Error Boundary

Error boundaries must be class components (as of React 18).

# Basic Example:

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so next render shows fallback UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Log the error (to console or error reporting services)
    console.error("Error caught by ErrorBoundary:", error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong.</h2>;
    }

    return this.props.children;
  }
}
```
# Usage

```jsx
   <ErrorBoundary fallback={<div>Oops! Custom Error UI</div>}>
     <ComponentThatMightCrash />
   </ErrorBoundary>
```
```jsx
   render() {
     if (this.state.hasError) {
       return this.props.fallback || <h2>Something went wrong.</h2>;
     }
     return this.props.children;
   }
```









