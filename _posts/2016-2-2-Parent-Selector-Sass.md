---
layout: post
title: "& - The Parent Selector in Sass"
---

Sass has a very neat little piece of built in functionality called **the parent selector**.


It's written out as an ampersand (**`&`**) and it allows you to **reference the name of the parent selector while you are inside that selector**.

<br>

What do I mean by that? Consider the following example, which you may have seen in the past:

```sass
a {
  color: blue;

  &:hover {
    color: red;
  }
}
```

**See the `&` in there before the hover?** When your sass gets compiled, the compiler will swap the `&` out and replace it with a reference to the direct parent (in this case, the `a`). So the compiled CSS will look like this:

```css
a {
  color: blue;
}
a:hover {
  color: red;
}
```
**The `&:hover` becomes `a:hover` in the compiled CSS. Voila!**

## Why is this useful?
Because you can't write this:

```sass
a {
  color: blue;
  
  a:hover {
    color: red;
  }

}
```

This would get compiled as:

```sass
a {
  color: blue;
}
a a:hover {
  color: red;
}
```

Which would select an a tag being hovered over nested inside of another a tag. Which, let's be honest, we both know you don't want. 

## When else is this useful?

### BEM

### Adding a parent class

Let's say your website detects whether the user's language preference is Arabic or Hebrew, or any of the other right-to-left languages, and if it is, adds a class of `rtl` to the body (`<body class="rtl"></body>`).

Let's say you're using an awesome feature detection library like [Modernizr](https://modernizr.com/) to determine whether or not you can use Flexbox.

The way that Modernizr works is that it adds a class to the `<body>` tag (let's say `.no-flexbox`, for this example) if the user's browser doesn't support Flexbox. 

In order to 