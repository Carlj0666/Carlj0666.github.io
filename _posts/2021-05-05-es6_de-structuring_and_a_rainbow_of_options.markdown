---
layout: post
title:      "ES6, (...), destructuring & (=>), a rainbow of options"
date:       2021-05-05 22:00:01 -0400
permalink:  es6_de-structuring_and_a_rainbow_of_options
---


[For wonderfully fitting music to read by, "roygbiv" by: Boards of Canada](https://www.youtube.com/watch?v=0nnqGDZnWhU)

<img src="https://i.pinimg.com/originals/6c/0d/a4/6c0da408447d74a03a08ea9898d5dbad.jpg" alt="drawing" width="600px"/>


ES6 added the Spread Operator (...) which spreads out the elements of objects that can be iterated over, such as an array! This can be accomplished with .concat, but the spread operator saves us some time. Let's look at .concat:
```
let rain = ["blue", "indigo", "violet"]
let bow = ["red", "orange", "yellow", "green"]
rainbow = bow.concat(rain)
console.log(rainbow) 
// (7) ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
```

Using the Spread Operator it looks like this:
```
const rain = ["blue", "indigo", "violet"]
const  bow = ["red", "orange", "yellow", "green", ...rain]
console.log(bow)

// (7) ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]

```
The concept of passing by reference vs. passing by value comes into play when using the spread operator. Passing by reference refers to for instance declaring a variable (A), that references another variable (1), so (A) contains the reference to the value of (1). When passing by value, as one does with a spread operator, you effectivly clone the value of the referenced. When using this with object, the key and value pairs are copied into the new object. 

You can see here that the attributes from "newColors" are being copied into a new object:
```
const newColors = new Color({id: color.data.id, ...colordata.attributes})
```
## Destructuring
<img src="https://www.wallpapertip.com/wmimgs/79-791323_colors-colorful-abstract-blue-purple-red-orange-yellow.jpg" alt="Red, Yellow, Blue and Violet" width="600px"/>

ES6 also provides destructuring. Desctructuring gives us a quick way to declare and assign variables. One way we can do with arrays is like the following: 
```
const rainbowArray =["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
let colorR = rainbowArray[0]
let colorO = rainbowArray[1]
let colorY = rainbowArray[2]
let colorG = rainbowArray[3]
let colorB = rainbowArray[4]
let colorI = rainbowArray[5]
let colorV = rainbowArray[6]
```

Let's try it with destructuring this time:

```
const rainbowArray =["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
let [colorR, colorO, colorY, colorG, colorB, colorI, colorV] = rainbowArray
```

From here we can access those same variables in the console:

```
colorR
// "red"
```

We can also skip variables like so:

```
const rainbowArray =["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
let [colorR, , colorY, , colorB, , colorV] = rainbowArray
```

A nice way to get contrasting colors from the spectrum! Keep in mind order is super important when doing this with arrays. We can however name the variables anything we like.

```
const rainbowArray =["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
let [colorR, , colorY, , colorB, , colorV] = rainbowArray
```

```
colorO
// Uncaught ReferenceError: colorO is not defined
```

### De-structure with objects

<img src="https://i.pinimg.com/originals/33/32/cf/3332cf004dbdf8e500af68f7f4876164.jpg" alt="Color Wheel Abstract Art" width="600px"/>

The first difference here is that we de-structure using curly braces, also the variables must match the keys in our object as you will see:

```
const rainbowObject ={colorR: "red", colorO: "orange", colorY: "yellow", colorG: "green", colorB: "blue", colorI: "indigo", colorV: "violet"}
let {colorR, colorO, colorY, colorG, colorB, colorI, colorV} = rainbowArray
```

```
colorG
// "green"
colorY
// "yellow"
```

```

const rainbowObject ={colorR: "red", colorO: "orange", colorY: "yellow", colorG: "green", colorB: "blue", colorI: "indigo", colorV: "violet"}

function rainbowMaker ({colorR, colorO, colorY, colorG, colorB, colorI, colorV}) {
    return `<div>
		<p>${colorR}</p>
		<p>${colorO}</p>
		<p>${colorY}</p>
		<p>${colorG}</p>
		<p>${colorB}</p>
		<p>${colorI}</p>
		<p>${colorV}</p>
		</div>`
}
```

```
rainbowMaker(rainbowObject)
// "<div>\n\t\t<p>red</p>\n\t\t<p>orange</p>\n\t\t<p>yellow</p>\n\t\t<p>green</p>\n\t\t<p>blue</p>\n\t\t<p>indigo</p>\n\t\t<p>violet</p>\n\t\t</div>"
```

## Arrow function => Return Statements
<img src="https://assets.atlasobscura.com/article_images/20785/image.jpg" alt="kaleidoscope" width="600px">

As before we will look at some examples of Arrow functions first:

```
const colorsInRainbow = 7
const doubleRainbow = function(colorsInRainbow) {
  return colorsInRainbow * 2
}
```

```
doubleRainbow(colorsInRainbow)
14
```
 We can refactor this into an Arrow function like so which will return the same result:

```
const doubleRainbow = (colorsInRainbow) => {
  return colorsInRainbow * 2
}
```

The Arrow Function return statements can be shortened. If the function is returning a single line of code, we can take out the curly braces, and we can also remove the RETURN!

The following is exactly the same as the above code snippet:
```
const doubleRainbow = colorsInRainbow => colorsInRainbow * 2
```

But an issue arises from. To contrast we can see the following example:
```
function gimmeTheRainbow() { return "Amazing Rainbow" }
gimmeTheRainbow()
```
```
// "Amazing Rainbow"
```

However this next example returns undefined because functions return undefined without a Return statement:

```
function gimmeTheRainbow() { "Amazing Rainbow" }
gimmeTheRainbow()
```

```
// undefined
```

So now thanks to ES6 and Arrow functions as long as the Arrow Function is "curly braced" we can get statements into the function body:

```
const howManyRainbows = () => {
    const rainbowRandomizer = Math.random() > 0.5
    return rainbowRandomizer? 'One Rainbow!' : 'Double Rainbows!!'
}
howManyRainbows() 
```

So with curly braces it's necessary to use the return statement, if we remove the curly braces and write our code on one line, we no longer need to use return. With our multi-line example above however, those curly braces allow us to use more than one expression or statement.
# THANKS RETURN STATEMENT!
<img src="https://www.publicdomainpictures.net/pictures/220000/velka/double-rainbow-1494515919gKs.jpg" alt="kaleidoscope" width="600px">









