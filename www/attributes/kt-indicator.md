---
layout: layout.njk
title: </> kutty - kt-indicator
---

## `kt-indicator`

The `kt-indicator` attribute allows you to specify the element that will have the `kutty-request` class
added to it for the duration of the request. This can be used to show spinners or progress indicators
while the request is in flight.

The value of this attribute is a CSS query selector of the element or elements to apply the class to.

Here is an example with a spinner adjacent to the button:

```html
<div>
    <button kt-post="/example" kt-indicator="#spinner">
        Post It!
    </button>
    <img  id="spinner" class="kutty-indicator" src="/img/bars.svg"/>
</div>
```

When a request is in flight, this will cause the `kutty-request` class to be added to the `#spinner`
image.  The image also has the `kutty-indicator` class on it, which defines an opacity transition
that will show the spinner:

```css
    .kutty-indicator{
        opacity:0;
        transition: opacity 500ms ease-in;
    }
    .kutty-request .kutty-indicator{
        opacity:1
    }
    .kutty-request.kutty-indicator{
        opacity:1
    }
```

If you would prefer a different effect for showing the spinner you could define and use your own indicator
CSS.  Here is an example that uses `display` rather than opacity:

```css
    .kutty-indicator{
        display:none;
    }
    .kutty-request .my-indicator{
        display:inline;
    }
    .kutty-request.my-indicator{
        display:inline;
    }
```

Note that the target of the `ic-indicator` selector need not be the exact element that you
want to show: it can be any element in the parent hierarchy of the indicator.

Finally, note that the `kutty-request` class by default is added to the element causing
the request, so you can place an indicator inside of that element and not need to explictly
call it out with the `ic-indicator` attribute:

```html
<button kt-post="/example">
    Post It!
   <img  class="kutty-indicator" src="/img/bars.svg"/>
</button>
```

### Demo

This simulates what a spinner might look like in that situation:

<button class="btn" kt-classes="toggle kutty-request:3s">
    Post It!
   <img  class="kutty-indicator" src="/img/bars.svg"/>
</button>

### Notes

* `kt-indicator` is inherited and can be placed on a parent element
* In the absence of an explicit indicator, the `kutty-request` class will be added to the element triggering the
  request