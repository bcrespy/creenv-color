# @creenv/color

The color class was designed to fasten the usage of colors and operations over colors. It is recommended to use such a class within the Creative Environement @creenv.

## Why should you use Color inside @creenv

If you're not interested into the why, you can directly jump to the next question :)

The Color class extends the [@creenv/vector Vector](https://github.com/bcrespy/creenv-color) class, which means any operations over the vectors can be applied between colors. However, you may want to be carefull with the alpha channel. It is stored as a regular component, so operations could alter it's value. This is probably a design issue and will change in the future.

While using the Creative Environment and some of its modules, using the Color class will allow other components to process the data faster. For instance, if you provide a Color object to a controller of [@creenv/gui GUI](https://github.com/bcrespy/creenv-gui), it will automatically understand that this is a colro provided, and will not have to execute computations to understand if weither a string #040404 is a color or not. 

Moreover, it gives you the ability, for a given color, to be used in many different manners without the need of transformations. If you want to change the active color of the native canvas API, just do like so: 

```js 
let color = new Color(255,55,20);
context.fillStyle = color.string;
```

You may think it is fastidious, but trust me, in the end it is not. How many times did I have to transform a 3d array into a css compliant string ? vice-versa ? The answer is too many times. By storing and manipulating the Colors using **one and only way**, and because such a way provides fast call to transform the data into other forms, you won't need to wrap your head arround stupid questions such as "shall i store my colors as a 3d array ? 4d array ? wait, I could only leave it as a string since i'm not going to make operations over it ? or maybe will I afterwards ?...

## How to use

These are quick examples on how to use Color. If you need more informations full doc is below.

```js
// instanciation 
let color = new Color(255, 0, 255); // magenta 

// some getters 
console.log(color.components); // ouput: [255, 0, 255, 1.0]
console.log(color.rgb); // output: [255, 0, 255]
console.log(color.hex); // output: #ff00ff
console.log(color.g); // ouput: 0

color.r = 0;
console.log(color.components): // output: [0, 0, 255, 1.0]

color.invert(); // color.components: [0, 255, 0]
```

```js
// conversion
let color;
color = Color.fromString("#f5336f");
color = Color.fromString("rgba(245,51,111,1.0)");
color = Color.fromArray([245,51,111]);
color = Color.fromHSL(341,0.91,0.58);
color = Color.fromHSV(320,0.50,0.40);
```

## How is the color stored

The components are stored in a 4 dimensions array [r; g; b; a]. Operations are only performed over this array, whose values can be retrived using such as .r, .rgb or .string.

## Full doc

Following is a full list of Color available members and methods.

___ 

### [Inherits @creenv/vector - all Vector members and methods are accessbile](https://github.com/bcrespy/creenv-vector#full-doc)

___

### constructor (**red**: *number*, **green**: *number*: **blue**: *number*, **alpha**: *number*)

| Name | Type | Definition | Default |
| ---- | ---- | ---------- | ------- |
| **red** | *number* | The red component of the color, in a **[0; 255]** range | 255 |
| **green** | *number* | The green component of the color, in a **[0; 255]** range | 255 |
| **blue** | *number* | The blue component of the color, in a **[0; 255]** range | 255 |
| **alpha** | *number* | The alpha component of the color, in a **[0; 1]** range | 1 |

___

### Class members

| Name | Type | Definition |
| ---- | ---- | ---------- |
| **.components** | *Array.\<number\>* | a 4d array of the components, [r, g, b, a] |

___

### Class getters / setters 

| Name | Getter / Setter | Type | Definition |
| ---- | --------------- | ---- | ---------- |
| **.r** | yes / yes | *number* | The red component of the color, .component[0] |
| **.g** | yes / yes | *number* | The green component of the color, .component[1] |
| **.b** | yes / yes | *number* | The blue component of the color, .component[2] |
| **.a** | yes / yes | *number* | The alpha component of the color, .component[3] |
| **.rgb** | yes / yes | *Array.\<number\>* | A 3d array of the red green and blue components [r, g, b] |
| **.rgba** | yes / yes | *Array.\<number\>* | A 4d array of the red green blue and alpha components [r, g, b,a] |
| **.string** | yes / no | *string* | A css compliant string of the color, on the form: "rgba(red, green, blue, alpha)" |
| **.hex** | yes / no | *string* | Hexadecimal representation of the color, on the form "#rrggbb" |
| **.hx** | yes / no | *string* | Hexadecimal representation of the color, on the form 0xrrggbb |
| **.hsl** | yes / no | *Array.\<number\>* | A 3d array of the same color, is the color space HSL, [hue; saturation: luminosity] |
| **.hsv** | yes / no | *Array.\<number\>* | A 3d array of the same color, is the color space HSV, [hue; saturation: value] |

```js
let color = new Color(255,255,255,1.0);

console.log(color.hex); // #ffffff
console.log(color.string); // rgba(255,255,255,1.0)
color.g = 0;
console.log(color.rgb); // [255,0,255]
console.log(color.hsl); // [300, 100, 0.5]
```
___

### static fromHSL (**h**: *number*, **s**: *number*, **l**: *number*): *Color*

Returns a new **Color**, with rgb components, given the HSL components in arguments.

___

### static fromHSV (**h**: *number*, **s**: *number*, **v**: *number*)

Returns a new **Color**, with rgb components, given the HSV components in arguments.

___

### static fromString (colorString)

Returns a new **Color** from any css compliant string. [W3C color specs](https://www.w3.org/TR/2018/REC-css-color-3-20180619/)

___

### static fromColor (color)

Returns a new **Color**, copy of **color** in arguments. #Duplicate of **color.copy()**

___

### static fromArray (components)

Returns a new color, from an array of 3 or 4 components, [r, g, b, ?a].

___

### toArray ()

Returns the components of the color as an array of 4 components, #Duplicate of **color.rgba** and **color.components**. color.components is the fastest.

___

### toObject ()

Returns the color as a key value Object, {r: red, g: green, b: blue, a: alpha}

___

### rounded ()

Returns a **new** Color which as the same components, but rounded.

___

### apply (func, alpha = false)

Applies a function **func** to all the components of the color, except alpha if **alpha** argument is set to false.

___

### convert (Class, func = x => x)

Converts the Color class to any other Class which accepts 4 arguments: red, green, blue, alpha. Can be useful if a tierce library only accepts its own Classes. If specified, the function **func** will be applied to all the components.

___

### interpolateWith (endColor, t)

Linear interpolation of all the components between this and **endColor**, **t** in range of [0;1] 

___

### invert () 

Inversion of the color

___

### grayscale ()

Applies a grayscale to the color. The result is the average of the [r; g; b] components.

___

### grayscaleLuminance ()

Computes the grayscale value fo the color, using the grayscale luminance formula grayscale = (Red * 0.2126 + Green * 0.7152 + Blue * 0.0722)

___

### grayscaleFastest () 

**This should only be used if a fast result is desired**. Set the value of the red and blue components equals to the green components. Innacurate but fast.

___

### relativeLuminance ()

Computes the [relative luminance](https://www.w3.org/TR/WCAG20/#relativeluminancedef) of the color.

___

### contrastWith (color)

Computes the [contrast](https://www.w3.org/TR/WCAG20/#contrast-ratiodef) with **color**.

___