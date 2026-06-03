---
title: Event element selectors
description: This article describes the element selectors used with event listeners.
url: https://docs.tealium.com/iq-tag-management/events/selectors/
---
Most event listeners require that you specify which element on a page you want trigger the event listener. For example, configuring a click event to track when a visitor clicks on a specific ad banner or button, or when a visitor plays a specific embedded video.

Specify the element to track by element ID, class, or a complex selector.

| Selector type | Example | Description |
| ------------- | ------- | ----------- |
| Element ID    | `#email-address` | A form field to collect email address |
| Class         | `.form-field`| Any form field|
| Complex selector | `div#feedback-form:not(.main) input[name=&#39;email&#39;]` | A form field named email in a `div` with ID `feedback-form`, but not within a `div` with class `main`. |
| Multiple elements | `.btn-cart, .btn-cart span` | Tracks clicks on the main element and any clickable nested elements. |

The event system uses the `Element.matches()` method for the selector. For more information about this method, see [Element.matches() at Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/API/Element/matches).

## When to use multiple-element selectors

Sometimes, an event doesn’t trigger even when the selector is valid. This often happens when the clicked element is nested inside the intended target element.

Tealium events attach cursor-based event listeners (such as `click`, `mousedown`, or `mouseup`) to the page’s `&lt;body&gt;`. When a user interacts with the page, the event handler checks whether the clicked element (`event.target`) matches the selector you provided. This behavior differs from the jQuery `onHandler` extension, which binds events directly to the elements that match the selector.

Here’s an example of how a click event listener works in Tealium:

```js
document.body.addEventListener(&#34;click&#34;, function(event) {
  if (event.target.matches(&#34;SELECTOR&#34;)) {
    console.log(&#34;Element clicked:&#34;, event.target.textContent);
    // Track event
  }
});
```

If your selector only targets the outer element (such as a button), and a user clicks a nested element (such as a `&lt;span&gt;` inside the button), the event listener won&#39;t trigger. In this case, use a multiple-element selector that includes both the main element and its nested clickable content.

### Example - Add to Cart button

Suppose you want to track clicks on an &#34;Add to Cart&#34; button with the following HTML:

```html
&lt;button class=&#34;btn-cart&#34;&gt;
  &lt;span&gt;Add to Cart&lt;/span&gt;
&lt;/button&gt;
```

Using the selector `.btn-cart` alone won’t always work. If the user clicks on the `&lt;span&gt;`, `event.target` is the `&lt;span&gt;`, not the `&lt;button&gt;`. To reliably track clicks on both the button and its nested elements, use a multiple-element selector:

```css
.btn-cart, .btn-cart span
```

This ensures that clicks on either the `&lt;button&gt;` or the `&lt;span&gt;` inside it are captured.

### Tips for finding the right selector

To find a working selector:

1. Open the page and right-click the element you want to track.
1. Select **Inspect** to open the browser&#39;s developer tools.
1. Identify the outermost element that should trigger the event.
1. Check for nested elements like `&lt;span&gt;`, `&lt;svg&gt;`, or `&lt;img&gt;` that users might click.
1. Build a selector that includes all possible clickable targets.

You can also use tools like [SelectorGadget](https://selectorgadget.com/) bookmarklet or browser extension to help build a selector. Here&#39;s how:

1. Load the page and open the SelectorGadget bookmarklet or browser extension.
1. Click the element text (for example, &#34;Add to Cart&#34;).
1. If the initial selector is too generic (like `&lt;span&gt;`), click other parts of the button to refine it.
1. Stop when all intended clickable parts are correctly highlighted.
1. Copy the final selector and use it in your event configuration.

For more information about how to determine an element&#39;s selector, see [How to Determine the CSS Selector of an Element](https://support.tealiumiq.com/en/support/solutions/articles/36000363465-how-to-determine-the-css-selector-of-an-element).

