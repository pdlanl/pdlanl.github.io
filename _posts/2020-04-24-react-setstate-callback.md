---
title: Using setState with callback in react
categories:
excerpt: Using setState with callback in react with problem, solution and example
tags:
  - ReactJs
toc: true
toc_sticky: true
author_profile: true
comments: true
header:
  overlay_color: '#000'
  overlay_filter: '0.5'
  overlay_image: /assets/images/posts/2020-04-24-react-setstate-callback.png
  teaser: /assets/images/posts/2020-04-24-react-setstate-callback.png
---

## Introduction

`setState` is an api provided by React which is used to update state and re-render a component. But it is not synchronous i.e the view is not update immediately after the `setState` is called. This can be problematic sometimes.

## Problem

Suppose, we want to perform some action immediately after the `setState` is called and the action requires the updated value but the state is not updated immediately, so we end up with stale value from the state. Generally, this occurs when we are unclear with the way `setState` works.

**Example**

```javascript
onSomeAction = () => {
  const { count } = this.state;
  this.setState({ count: count + 1 });
  if (this.state.count > 5) {
    alert("You've pressed button 5 times");
  }
};
```

You can find complete example on [CodeSandbox](https://codesandbox.io/s/fervent-brook-1r4y8?file=/src/App.js 'CodeSandbox')

If you check the example you can find that the alert is shown to the user when s/he clicks the button 6 times instead of 5 which we wanted. But we had to display the alert when the button was presses 5 times. But the code does not seem to have any error, how did it happen? It is because the `setState` updates the state after a certain time and until it is updated the next line will have already been executed resulting in the issue. So, how can we fix it?

## Solution

If we look into the documentation of [setState](https://reactjs.org/docs/react-component.html#setstate 'setState'). We can see that it takes two arguments:

1. Updater: For updating the state
2. Callback (optional): For performing any action after the state has been updated

The callback is a function and is called when setState has completely executed. So, let's try to change the above implementation to work as expected with the callback.

**Example**

```javascript
onSomeAction = () => {
  const { count } = this.state;
  this.setState({ count: count + 1 }, () => {
    if (this.state.count > 5) {
      alert("You've pressed button 5 times");
    }
  });
};
```

Complete example on [CodeSandbox](https://codesandbox.io/s/fervent-brook-1r4y8?file=/src/App.js 'CodeSandbox')

So, we finally displayed alert to the user when s/he clicked the button 5 times.
