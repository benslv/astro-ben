---
title: Creating a reusable media query function
datePublished: 2021-06-03
description: A quick guide on how to make a reusable function to handle media queries.
tags:
    - snippet
---

## In short

```js
// mixins.js

const breakpoints = {
	sm: "640px",
	md: "768px",
	lg: "1280px",
};

export const media = (size = "sm") =>
	`@media screen and (min-width: ${breakpoints[size]})`;
```

## Explanation

So it turns out [you can't use CSS variables with media queries](https://stackoverflow.com/a/40723269/12944841), which is a bit of a bummer.

The main reason you might want to do something like this is to create a bunch of reusable media query mixins for yourself, keeping all your breakpoints the same and letting you change them at a moment's notice. It also saves a few keystrokes and keeps you from having to remember what the exact syntax for the query should be ("is it `min-width` or `max-width`? Hmm...")

Since the function returns a template literal, it can be inserted whatever CSS-in-JS solution you're using!

The code above is basically what you'll need to write. Feel free to extend it with more breakpoints if you like, or add some checks to ensure you can't enter any incorrect values for the parameter!

### Usage

```js
// text.js

import styled from "styled-components";

import { media } from "./mixins.js";

const Text = styled.p`
	color: red;

	${media("sm")} {
		color: green;
	}

	${media("md")} {
		color: orange;
	}

	${media("md")} {
		color: blue;
	}
`;
```
