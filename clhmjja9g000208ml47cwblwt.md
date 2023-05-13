---
title: "Beginners Guide: Optimizing Performance with Event Delegation in Vanilla JS"
datePublished: Sat May 13 2023 22:10:14 GMT+0000 (Coordinated Universal Time)
cuid: clhmjja9g000208ml47cwblwt
slug: beginners-guide-optimizing-performance-with-event-delegation-in-vanilla-js
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/f3s0i96CRGQ/upload/48f4e6467781fb862933def4f3eacd52.jpeg
tags: javascript, beginners, frontend-development, vanilla-js-1

---

Event listeners in JavaScript are essential for enabling elements in the Document Object Model or DOM to respond to user actions on a webpage. However, it's vital to be mindful of the impact of having too many event listeners. Each event listener, when created, consumes memory resources. Consequently, an excessive number of event listeners in the DOM can lead to increased memory usage, ultimately affecting the performance of your web application.

By utilizing JavaScript Event Delegation, it is possible to reduce the overall number of event listeners in the DOM. In this article, we will explore the concept of event delegation and learn how to enhance the performance of web applications through it.

## Prerequisites

* Basic knowledge of HTML and CSS.
    
* Understanding of JavaScript Events, Event Handlers, and Event Propagation.
    

## An Overview of Event Delegation

JavaScript event delegation is a technique that allows you to optimize event handling in web applications. Instead of attaching event listeners to individual elements, event delegation involves attaching a single event listener to a parent element. This listener captures events from its child elements through event `bubbling` or `capturing`.

With event delegation, you can reduce the number of event listeners in the DOM, which leads to improved performance and memory efficiency. When an event occurs to a child element, it bubbles up to the parent element, where the event listener is attached. By leveraging the event `target` property, you can determine which child element triggered the event and take appropriate action. Hence, `currentTarget` points to the element where the event listener is attached (in this case, the parent element), while `target` points to the element that triggered the event (in this case, the child element).

Imagine having elements that are added or changed dynamically on your web page. With event delegation, you don't have to worry about attaching individual event listeners to these elements. The parent element acts as a centralized listener, capturing events from existing and dynamically generated child elements. It's like having an event radar that automatically adapts to changes in your DOM structure.

## Event Listener Hell

"Wait! What? Event Listener Hell?"

If you are familiar with the concept of callback hell in JavaScript, the outcome of having several chained callbacks, then you probably have the mixed emotions indicated above. Yes, you are within your rights to question my choice of title, but here's the catch: event listener hell in this context is having too many event listeners present in your JavaScript codebase.

There may be situations where an event listener is created within an event listener, and so on. Still, we shall focus on event listener hell cases resulting from having too many children event listeners created within a parent.

Below is a codepen showing an event listener hell situation. Click on the "JS" tab to see.

%[https://codepen.io/utin-francis-peter/pen/mdzKbZK?editors=1111] 

In the codepen, ten (10) button elements were created in the DOM. Using `document.querySelectorAll`, we selected all button elements with the same class name - `child`. By doing this, we had a `nodeList` stored in the `btns` variable. To have each `button` element react to a `click` event, we looped through it and attached individual event listeners to each element. Is this a good practice? Let's find out.

Excessive event listeners can overwhelm the DOM by consuming memory and processing power. When you have too many event listeners, it can slow down your web page and make it less responsive. Additionally, inefficient event handling code and accumulation of event listeners over time can cause performance issues. To prevent this, limit the number of event listeners through event delegation, optimize your code, and remove unnecessary listeners when they're no longer needed.

While removing unnecessary listeners from the DOM is an option, this article focuses on limiting the number of event listeners through delegation. Let's find out how!

## Event Delegation Haven

Welcome to Event Delegation Haven, a city of hope for the DOM. In this city, the number of event listeners in the DOM is limited and managed. When you find too many listeners attached to elements with a common parent, remember there's a city called Event Delegation Haven. Let's explore our newly found city, do join me.

> Which children element is your target? Now, instead of having an event listener attached to the child element directly, you have it attached to the parent element, knowing that when a click or specified event happens on the target child element, it bubbles up to the parent. The parent element has an event listener and a handler function ready to execute but only executes when the target child element passes the set condition(s) for block execution.

### Capturing Target Child Events

Considering how things work in this city, we must determine when a `target` child element has fired an event to execute the handler function efficiently. Let's look at an improved version of our previous codepen to see how. In the JavaScript snippet, we would only toggle the class of a button element if it passes the set condition.

```xml
<div class="parent">
      <button class="child">Btn 1</button>
      <button class="child">Btn 2</button>
      <button class="child">Btn 3</button>
      <button class="child">Btn 4</button>
      <button class="child">Btn 5</button>
      <button class="child">Btn 6</button>
      <button class="child can-toggle">Btn 7</button>
      <button class="child">Btn 8</button>
      <button class="child">Btn 9</button>
      <button class="child can-toggle">Btn 10</button>
    </div>
```

```css
button{
  background: #000;
  color: #fff;
}
.toggle-styles{
  background: #fff;
  color: #000
}
```

```javascript
const parent = document.querySelector(".parent");

parent.addEventListener("click", (e) => { 
const {target} = e;
// react to child event when set condition is passed
  if(target.classList.contains("can-toggle")){
    target.classList.toggle("toggle-styles")
  }
})
```

In the above snippets, the JavaScript snippet, to be specific, we successfully attached just one event listener to the parent element. We used event bubbling to capture the `target` child event. The process is as follows:

1. The event listener gets attached to the parent element.
    
2. On clicking on a child element, the event bubbles up from the target (child element) to the parent. Since the parent element has an event listener attached, a similar event is fired on the parent.
    
3. Next, the handler function attached to the parent gets executed. In our JavaScript snippet, we specified the condition for reacting to the child event, and within the code block, we specified what happens to the child element as a response to the client's action on the element.
    

## Conclusion

In this article, you've learned not to overwhelm the DOM with too many event listeners but rather to use a more DOM-friendly approach that involves attaching an event listener to a common parent. This approach helped us reduce the number of event listeners in our example from ten (10) to one (1); amazing, right?

This practice is among the few that comes with little or no sacrifices because by having fewer event listeners in the DOM, we minimize the amount of memory resource used, which optimizes the performance of our web applications.

That's all, folks! I hope this was helpful. Please do well to leave some feedback, share the article with friends, and connect with me on [**LinkedIn**](https://linkedin.com/in/francis-peter-utin).