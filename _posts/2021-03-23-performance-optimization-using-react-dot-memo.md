---
title: Performance optimization using React.memo()
categories:
excerpt: Using React.memo() for optimizing your react app with example.
tags:
  - reactJS
  - optimization
  - performance
toc: true
toc_sticky: true
author_profile: true
comments: true
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/posts/2021-03-23-react-memo.png
  teaser: /assets/images/posts/2021-03-23-react-memo.png
---

NOTE: This article was first posted on [The Dev Post](https://thedevpost.com/blog/performance-optimization-using-react-memo/){:target="_blank"}.

# Introduction

`React.memo` is a higher order component provided by react that will return a memoized version of the component that only changes if one of the props has changed. It is same as `PureComponent` but instead of classes `React.memo` is used for functional components.

# Why use React.memo?

`React.memo` memoizes the rendered output then skips unnecessary rendering. This helps to prevent unnecessary re-rendering of components and computations needed for component rendering.

# React.memo in action

![Talk is cheap. Show me the code](https://img.devrant.com/devrant/rant/r_42298_vkdre.jpg)

As an example implementation lets create a component which will:

- Greet user
- Show number of times user has greeted
- Let user greet using button

Let's create and add a function/method on `GreetUser` component that does the work of simulating some heavy computations while rendering the component.

```javascript
// userGreeting.js

const UserGreeting = () => {
  const getUserName = () => {
    let i = 0;
    while (i < 3000000000) i++;

    return 'John Doe';
  };

  return <div>Hello {getUserName()},</div>;
};
```

`GreetingCount` and `Button` components will show the count and increment greet count on click respectively and do not have any heavy computations.

```javascript
// greetingCount.js

const GreetingCount = ({ count }) => (
  return <div>You greeted me {count} times.</div>;
);
```

```javascript
// button.js

const Button = ({ title, onClick }) => (
  <button onClick={onClick}>{title}</button>
);
```

And the parent component will import all these components and have method to update the greetings count.

```javascript
//App.js

const App = () => {
  const [greetCount, setGreetCount] = useState(0);
  const onGreet = () => {
    setGreetCount(greetCount + 1);
  };

  return (
    <div className='App'>
      <UserGreeting />
      <GreetingCount count={greetCount} />
      <Button title='Hi' onClick={onGreet} />
    </div>
  );
};
```

## Problem
![Before using React.memo](https://media.giphy.com/media/UsHTY3wmNpmk8G3b8W/giphy.gif)

As you can see that there is delay for certain interval before the UI updates after the button is clicked. This is because when we click on the button the state changes so every components are rerendered and  the `GreetUser` component is rerendered as well. The `getUserName` method is executed again due to re-render of `GreetUser` component thus causing delay on UI update.

## Solution

So the solution for the above problem is to use `React.memo()`. `The React.memo()` method will memoize the component and does a shallow comparison of the component and since none of the props in `GreetUser` component has been changed, it will skip re-rendering of this component. This will prevent the recomputation during the render and the UI updates quickly. For this we will wrap the component with `React.memo()` and export it.

```javascript
const UserGreeting = () => {
  // code here
};

export default React.memo(UserGreeting);
```
## Result:
![After using React.memo gif](https://media.giphy.com/media/f4DzHcAhrn8OD5AQlj/giphy.gif)

As you can see now that the component does not re-render `GreetUser` component and the UI is updated without any delay.

You can find complete example on [CodeSandbox](https://codesandbox.io/s/sleepy-dawn-6o4ln?file=/src/App.js 'CodeSandbox')
