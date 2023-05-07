---
title: "Enhancing UX through Image Loading in React.JS"
datePublished: Sat May 06 2023 11:12:33 GMT+0000 (Coordinated Universal Time)
cuid: clhbvyju7000009k0a1nyhr4p
slug: enhancing-ux-through-image-loading-in-reactjs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683369179119/41fa65ac-fac6-4158-87b3-6391f28b2dff.jpeg
tags: javascript, ux, images, reactjs, frontend-development

---

Things can quickly go from "I am super excited to view this landing page" to "Why is it taking so long for this image to show? Dev is frustrating me!". Sadly, end users fail to understand that this isn't entirely on you - the dev, but may be due to the client's poor internet connection.

In this tutorial, we'll learn how to tone down the bad UX by rendering the page contents after loading an image resource. We can wait for the entire image resource in a webpage to load, but this may take more time and add to the frustration. Hence this article focuses on listening for a specific image to load, in our case, the hero image.

## **Prerequisites**

* Code editor and browser.
    
* Basic knowledge of JavaScript events and Event Handlers.
    
* Basic knowledge of React and React Hooks.
    
* Basic knowledge of Git, and package managers (npm or yarn).
    

**Let's get started**

## Installation

### Cloning the Starter App

To get started, I have provided a starter app on GitHub. To help us focus on implementation, the UI has been built already. The application has been configured with `Create React App` and `SCSS`. Open your terminal and run the following command:

```markdown
git clone -b starter https://github.com/utin-francis-peter/img-loading-tutorial.git && cd img-loading-tutorial
```

The above command will clone the starter branch of the repo into your local machine and make the project folder your current working directory.

Next, run the following command in your terminal to install the dependencies.

```markdown
yarn
```

Or if you prefer npm, use:

```markdown
npm install
```

### Installing React Spinners

Next, let's install `React Spinners`, which would be conditionally displayed while waiting for our image to finish loading. Use the following command to install it:

```markdown
yarn add react-spinners
```

or

```markdown
npm install react-spinners
```

Once you have installed `React Spinners`, there are no further dependencies to install.

To start the application, run:

```markdown
yarn dev
```

or

```markdown
npm dev
```

Voilà! You should see the hero page displayed on your browser as seen below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683371378981/e273f7aa-bf8c-458d-8b16-93fa3355c51d.png align="center")

*We'll learn to display the page content after fully loading the hero image. Let's dive!*

## Implementing the Logic

Open the `App.jsx` file and paste the following codes just before the `return` statement:

```javascript
const [isLoaded, setIsLoaded] = useState(false);

  useEffect(() => {
    if (document.readyState === "complete") {
      setIsLoaded(true);
    } else {
      if (typeof window !== "undefined") {
        window.addEventListener("load", () => {
          const heroImg = document.getElementsByTagName("img")[0];
          if (heroImg.complete && heroImg.naturalHeight !== 0)
            setIsLoaded(true);
        });
      }
    }
  });
```

In the above snippet, we did the following:

1. Created an `isLoaded` state that tells if the target image is loaded.
    
2. Checked the status of our document. The document status can be either loading, interactive, or complete. `complete` indicates that all resources are fully loaded including the image(s). If this is true, toggle `isLoaded` state to `true`. Else we listen for a `load` event on the window. The subtle difference between `document.readyState` and the `load` event is that the former will fire as soon as the document is ready, even if some resources such as images are still loading. The latter will only fire when the entire page has finished loading, including image resources.
    
3. Using `document.getElementsByTagName("img")[0]`, we received an `HTMLCollection`, whose data structure is similar to an array. Afterward, we accessed its first element at position 0, which is the first image we have on the webpage (the hero image).
    
4. Accessing a single image element then gives us access to the `complete` and `naturalHeight` properties that can be used to know if an image is fully loaded.
    

## Conditionally Displaying Spinner

A spinner in React is a small visual element that shows up on a web page when something is loading or processing. It looks like a little circle that spins around and around. You might have seen it before when you're waiting for a video to load or for a game to start.

Since we now have a state that only toggles to `true` when page resources or target image is fully loaded, let's see how we can conditionally display a spinner that disappears after the image is loaded.

First, import `ClipLoader` component from `React Spinners` into the `App.jsx` file:

```javascript
import ClipLoader from "react-spinners/ClipLoader";
```

Next, replace your existing JSX in the app.jsx file with the codes below:

```javascript
<>
      <div className="spinner" style={{ display: isLoaded ? "none" : "flex" }}>
        <ClipLoader size={70} loading={true} color="#f6921e" />
      </div>

      <div className="app" style={{ display: isLoaded ? "block" : "none" }}>
        <header className="container">
          <h3>logo</h3>

          <nav>
            <ul>
              <li>
                <a href="/">nav</a>
              </li>
            </ul>
          </nav>
        </header>

        <main>
          <section className="hero container">
            <div className="hero-desc-container">
              <p>With the right mind, you will</p>
              <h1 className="fs-lg">SUCCEED</h1>
              <p className="hero-desc">
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Eveniet
                iusto assumenda corporis reprehenderit maxime non veniam.
              </p>
              <button className="btn-lg">BELIEVE IN YOU</button>
            </div>
            <div className="hero-img">
              <img
                src="https://media.istockphoto.com/id/1445687851/photo/portrait-of-an-adult-siblings.jpg?s=612x612&w=0&k=20&c=CtHQM49ho0qkKjIgRk9XwJJlvwSsXm_XTJ2xm6p7nKI="
                alt="img from unsplash"
              />
            </div>
          </section>
        </main>
      </div>
    </>
```

From the snippets above, we created a second `div` that's used to house our `ClipLoader` component. The added inline styles are used to conditionally display or hide either of the `divs` depending on the status of `isLoaded` application state. The idea is to have the page resources loading in the background while displaying the spinner.

## Conclusion

Images play a vital role in enhancing the visual appeal of web pages. However, it's important to optimize image loading to improve user experience. Techniques such as lazy-loading and resizing can help reduce file size and improve load times. Additionally, providing users with a loading spinner can enhance engagement and a good user experience.

A similar principle can also be applied when making API calls. A spinner gets conditionally rendered while awaiting the arrival of requested data.

You can find the [**finished project on GitHub**](https://github.com/utin-francis-peter/img-loading-tutorial) for reference and further exploration.

That's all, folks! I hope this was helpful. Please do well to leave some feedback, share the article with friends, and connect with me on [LinkedIn](https://linkedin.com/in/francis-peter-utin).

Cover image by [vectorjuice](https://www.freepik.com/free-vector/programmers-using-javascript-programming-language-computer-tiny-people-javascript-language-javascript-engine-js-web-development-concept-bright-vibrant-violet-isolated-illustration_10782951.htm#query=react%20js%20spinner&position=7&from_view=search&track=ais) on [Freepik](https://www.freepik.com/).