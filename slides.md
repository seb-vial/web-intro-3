---
theme: light-icons
image: ./images/intro.jpg
title: Web development - Introduction | Part 3
transition: slide-left
mdc: true
layout: intro
download: true
favicon: "https://scratchmy.dev/favicon.ico"
---

<div class="mb-4 absolute top-20 left-12">
  <span class="text-6xl text-teal-400 font-500" >
    Web development<light-icon icon="code"/>
  </span>
  <div class="text-4xl text-white text-opacity-60 font-300 uppercase" >
    Introduction – Part 3
  </div>
</div>

<div class="mb-4 absolute bottom-4 right-12">
  <div class="flex gap-x-4 items-center">
    <div class="rounded-full p-0.5 shadow-lg shadow-zinc-800/5 ring-1 backdrop-blur bg-white ring-white/10">
      <img src="/images/profile.webp" sizes="4rem" class="rounded-full object-cover h-16 w-16" alt="Profile picture" width="400" height="400" loading="lazy" decoding="async">
    </div>
    <div class="flex flex-col">
      <p class="!my-1 text-xl">Sébastien VIALLEMONTEIL</p>
      <p class="!my-1">Full stack web developer</p>
      <a href="mailto:sebastien.viallemonteil@institut-agro.fr"><light-icon icon="mail" class="inline-block mb-0.5"/> sebastien.viallemonteil@institut-agro.fr</a>
    </div>
  </div>
</div>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
Hold your position

<v-clicks>

- As the name suggests, positioning is way to define how elements should be postioned in the page
- Should they be placed according to the normal flow of the document or should they be transported to a higher plane of existence?
- There are **five** different positions (**static**, **relative**, **absolute**, **fixed** and **sticky**)
- And **four** ways to control the offset of postioned elements, one for each side (**top**, **bottom**, **left**, **right**)

</v-clicks>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
Just go with the flow

### Static
The **static** position is set by default by browsers. Static elements take their rightful place in the normal flow of the page.

<div v-click>

```css {*}{lines:true}
.my-element {
  position: static; /* <== Default behavior */
  /* Setting offsets won’t have any effect */
  top: 55px; /* Nope */
  left: 20px; /* Nice try */
}
```

</div>

<ComplementaryMessage bordered>As this this the default behavior, you should never have to do this, <strong>except</strong> if you have to overwrite existing code on a project</ComplementaryMessage>

<div v-motion v-click="3" :initial="{x: 999, y: -999}" :enter="{x: 570, y: -230}" class="absolute max-w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <section class="p-2 border inline-block">Hey i’m static 🙋</section>
  <p class="border p-2 inline-block !m-0">Yep, me too 🙄</p>
  <div class="border border-blue">As am I, dear!</div>
</div>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
I sense a disturbance in the flow.

### Relative
With **relative** position, elements are still positioned according to the normal flow but they can be offset *relative* to themselves using **top**, **bottom**, **left** and **right** rules.

<div v-click="1">

````md magic-move {lines: true}
```css {*|all}
.my-element {
  /* Something is missing here */
  top: 25px;
  right: 25px;
}
```
```css {*}
.my-element {
  /* There we go */
  position: relative;
  top: 25px;
  right: 25px;
}
```
````

</div>
<div v-motion v-click="1" :initial="{x: 999, y: -999}" :enter="{x: 570, y: -230}" class="absolute max-w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <section class="p-2 border inline-block">Hey i’m static 🙋</section>
  <p v-if="$clicks < 2" class="border p-2 inline-block !m-0">Yep, me too 🙄</p>
  <p  v-motion v-if="$clicks >= 2" :initial="{x: 0, y: 0}" :enter="{x: -25, y: 25, delay: 1000}" class="border p-2 inline-block border-red !m-0">I’m relative now!</p>
  <div class="border border-blue">As am I, dear!</div>
</div>

<Transition
  enter-active-class="transition-opacity duration-75 delay-800"
  enter-from-class="opacity-0"
  enter-to-class="opacity-100"
  leave-active-class="transition-opacity duration-150"
  leave-from-class="opacity-100"
  leave-to-class="opacity-0"
>
  <div v-if="$clicks >= 2">
    <arrow x1="926" x2="926" y1="190" y2="209" color="red" width="1" />
    <arrow x1="926" x2="907" y1="213" y2="213" color="red" width="1" />
    <span class="absolute text-[10px] text-red right-15 top-[35%]">25px</span>
  </div>
</Transition>

<ComplementaryMessage type="alert" bordered v-click="3">Notice surrounding elements don’t move, which means a relative element can overlap others.</ComplementaryMessage>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
To above and beyond.

### Absolute
With **absolute** position, elements are removed from the normal flow. The their initial allocated space is given to following elements. They can be positioned *relative* to the closest positioned parent (if any) with **top**, **bottom**, **left** and **right** rules.

<div v-click="1">

````md magic-move {lines: true}
```css {*|all}
.my-element {
  /* Something is missing here, again */
  top: 25px;
  left: 25px;
}
```
```css {*}
.my-element {
  /* There we go */
  position: absolute;
  top: 25px;
  left: 25px;
}
```
````

</div>
<div v-motion v-click="1" :initial="{x: 999, y: -999}" :enter="{x: 570, y: -230}" class="absolute w-1/3 min-h-25 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="relative">
    <section class="p-2 border inline-block">Hey i’m static 🙋</section>
    <p v-if="$clicks < 2" class="border p-2 inline-block !m-0">Yep, me too 🙄</p>
    <p  v-motion v-if="$clicks >= 2" :initial="{x: -151, y: 0}" :enter="{x: -126, y: 25, delay: 1000}" class="absolute p-2 inline-block text-white bg-red !m-0">I’m absolute now!</p>
    <div class="border border-blue inline-block">As am I, dear!</div>
  </div>
</div>

<Transition
  enter-active-class="transition-opacity duration-75 delay-800"
  enter-from-class="opacity-0"
  enter-to-class="opacity-100"
  leave-active-class="transition-opacity duration-150"
  leave-from-class="opacity-100"
  leave-to-class="opacity-0"
>
  <div v-if="$clicks >= 2">
    <arrow x1="639" x2="639" y1="202" y2="221" color="red" width="1" />
    <arrow x1="639" x2="659" y1="225" y2="225" color="red" width="1" />
    <span class="absolute text-[10px] text-red right-79 top-[37%]">25px</span>
  </div>
</Transition>

<ComplementaryMessage type="alert" bordered v-click="3">If the <strong>absolute</strong> positioned element has no positioned parent, it will be positioned relative to the <strong>body</strong></ComplementaryMessage>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
If it ain’t broke, don’t fix it.

### Fixed
As for **absolute**, the **fixed** position, removes the element from the normal flow. Its initial allocated space is given to following elements. It will be be positioned *relative* to the **body** (viewport) with **top**, **bottom**, **left** and **right** rules.

<div v-click>

```css {*}{lines:true}
.my-element {
  position: fixed;
  top: 50px;
  left: 100px;
}
```

</div>
<div v-click="2" class="absolute overflow-y-auto [scrollbar-width:thin] w-1/3 top-[40%] right-10 max-h-35 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="min-h-3xl">
    <section class="p-2 border inline-block">Hey i’m static 🙋</section>
    <p  v-motion v-click="3" :initial="{x: 0, y: -999}" :enter="{x: -59, y: 42}" class="fixed p-2 inline-block text-white bg-red !m-0">I’m fixed, scroll and see!</p>
    <div class="border border-blue inline-block">As am I, dear!</div>
  </div>
</div>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
Sticky ain’t so easy.

### Sticky
**Sticky** elements stay postioned in the normal flow (like **static** and **relative**). They can be offset to the nearest scrolling ancestor (parent, grand-parent, and so on)  with **top**, **bottom**, **left** and **right** rules. But it will only **stick** to its containing ancestor (direct parent) as long as this ancestor is within the **viewport**.

<div v-click>

```css {*}{lines:true}
header {
  height: 200px;
}
nav {
  height: 50px;
  position: sticky;
  top: 10px;
}
```

</div>
<div v-click="2" class="absolute overflow-y-auto [scrollbar-width:thin] w-1/3 top-[40%] right-10 max-h-35 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="min-h-3xl text-xs">
    <header class="p-2 h-50 bg-blue white-text">
      I am the header
      <nav  v-click="3" class="sticky h-12 top-[10px] p-2 text-white bg-red">I am a nav inside the header and sticky!</nav>
    </header>
  </div>
</div>

<div v-click="4">
  <ComplementaryMessage type="alert" bordered>The <strong>nav</strong> element goes out of the viewport when the <strong>header</strong> does.</ComplementaryMessage>
</div>

---
layout: dynamic-image
image: ./images/stacking.jpg
equal: false
left: false
---

# Positioning
ZzzzZ 😴.

With multiple positioned elements, overlapping can happen. Sometimes you need to decide which element should be on top of others. That’s when ~~Zoro~~ **z-index** comes into play.

<div v-click="1">

````md magic-move {lines: true}
```css {*|all}
.first {
  postion: absolute;
  top: 50px;
  left: 40px;
  background: red;
}
.second {
  postion: absolute;
  top: 40px;
  left: 60px;
  background: blue;
}
```
```css {*}
.first {
  postion: absolute;
  top: 50px;
  left: 40px;
  background: red;
  z-index: 1;
}
.second {
  postion: absolute;
  top: 40px;
  left: 60px;
  background: blue;
}
```
````

<div v-motion v-click="1" :initial="{x: 999, y: -999}" :enter="{x: 570, y: -230}" class="absolute w-1/3 min-h-30 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="relative text-white">
    <template v-if="$clicks < 2">
      <div class="bg-red absolute top-12 left-10 p-2">I’m first and absolute!</div>
      <div class="bg-blue absolute top-10 left-15 p-2">Not so fast!</div>
    </template>
    <template v-if="$clicks >= 2">
      <div class="bg-red absolute top-12 left-10 p-2 z-1">I said I’m absolute!</div>
      <div class="bg-blue absolute top-10 left-15 p-2">What??</div>
    </template>
  </div>
</div>

</div>

<div v-click="3">
  <ComplementaryMessage type="alert"><strong>z-index</strong> only has effect on positioned elements relative to the same ancestor.</ComplementaryMessage>
</div>

---
layout: intro
image: ./images/meditation.jpg
---

<h1 class="absolute left-12 bottom-12">You’re OK, just breath.</h1>
<p class="opacity-80 absolute left-12 bottom-6">In… and out</p>

<img src="/images/gifs/breather.webp" class="absolute right-12 top-[20%] border-2 border-white rounded-md" alt="Sheldon panick Gif" />

---
layout: intro
image: ./images/meditation.jpg
---

<h1 class="absolute left-12 bottom-12">You’re good to go.</h1>
<p class="opacity-80 absolute left-12 bottom-6">You wouldn’t want to run out of air…</p>

<img src="/images/gifs/ready.webp" class="absolute right-12 top-[20%] border-2 border-white rounded-md max-h-[50%]" alt="Cat ready Gif" />

---
layout: intro
image: ./images/quiz.jpg
---

<h1 class="absolute left-12 bottom-12">Quiz time! Mouahahah</h1>
<p class="opacity-80 absolute left-12 bottom-6">Come on, it was so obvious…</p>

<img src="/images/gifs/evil-laugh.webp" class="absolute right-12 top-[20%] border-2 border-white rounded-m max-h-[50%]" alt="Evil laugh Gif" />

---
layout: dynamic-image
image: ./images/question.jpg
equal: false
---

# What position is it again?
Feel the ~~pain~~ pen in your hand

<v-clicks>

- Create a block with an id of **container** and a left margin of 100px
- Add two paragraphs which possess the same class
- Both paragraphs have a padding of 10px on each side
- Add a figure containing a piture with a caption. This figure is positioned relatively and offset to the right by 50px

</v-clicks>

---
layout: dynamic-image
image: ./images/time.jpg
equal: false
left: false
---

# Time’s up!
Who wants to write some code?

```html {*|1,10|2-3|4-9}{lines:true}
<div id="container">
  <p class="para">Some text</p>
  <p class="para">Some text, again...</p>
  <figure>
    <img src="images/grumpy_cat.jpg" alt="Grumpy cat" />
    <figcaption>
      Still this grumpy cat !
    </figcaption>
  </figure>
</div>
```

---
layout: dynamic-image
image: ./images/time.jpg
equal: false
left: false
---

# Time’s up!
Who wants to write some code?

```css {*|1-3|4-6|7-10|all}{lines:true}
#container {
  margin-left: 100px;
}
.para {
  padding: 10px;
}
figure {
  position: relative;
  left: 50px;
}
```

<div v-motion v-click="4" :initial="{x: 999, y: -999}" :enter="{x: 570, y: -275}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="border border-gray-6 ml-25 text-xs">
    <p class="p-3">Some text</p>
    <p class="p-3">Some text, again...</p>
    <figure class="relative left-12">
      <img class="max-h-20" src="/images/grumpy_cat.jpg" alt="Grumpy cat" />
      <figcaption>
        Still this grumpy cat !
      </figcaption>
    </figure>
  </div>
</div>

---
layout: dynamic-image
image: ./images/printer.jpg
equal: false
---

# CSS for printing
Ink outside the box

Sometimes, users want to print parts of your website. On paper, a page should look differently, and we need to remove unnecessary elements via CSS. In order to do that, we create specific CSS for printing.

<div v-click>

```html {*}{lines: true}
<link type="text/css" rel="stylesheet" href="style.css" media="print">
```

</div>

<ComplementaryMessage bordered>You can preview what your page would look like by using the «&nbsp;print preview&nbsp;» feature of your browser</ComplementaryMessage>

---
layout: dynamic-image
image: ./images/gradient.jpg
equal: false
left: false
---

# Gradients
Make a great color transition

CSS3 blesses us with the possibility of creating our own gradients in place of image backgrounds. There are three types of gradient:

<v-clicks>

- **linear-gradient**: transition colors in a straight line
- **radial-gradient**: your gradients will radiate and spread from a point
- **conic-gradient**: rotate differents colors around a specific point

</v-clicks>

<ComplementaryMessage bordered>Gradients, whatever their type, can possess an infinite number of colors and can also be stacked on top of other gradients.</ComplementaryMessage>

<div v-click>

More on [gradients](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_images/Using_CSS_gradients)

</div>

---
layout: dynamic-image
image: ./images/gradient.jpg
equal: false
left: false
---

# Gradients (1/3)
Make a great color transition

### Linear gradient
```css {*}{lines:true}
.my-block {
  /* Named direction, to top, to right, to bottom left, etc. */
  background-image: linear-gradient(to right, blue, white, red);
}
```

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -175}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="h-20 bg-gradient-to-r from-[blue] via-white to-red">
  </div>
</div>

<div v-click>

### Linear gradient with color stops
```css {*}{lines:true}
.my-block {
  /* Using angle as direction and color stops */
  background-image: linear-gradient(90deg, blue 20%, white, red 80%);
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -125}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-block-graddeg {
      background-image: linear-gradient(90deg, blue 20%, white, red 80%);
    }
  </style>
  <div class="h-20 my-block-graddeg">
  </div>
</div>

<div v-click>

### Stacking gradients
```css {*}{lines:true}
.my-block {
  background-image: linear-gradient(to bottom, lime 10%, red 30%,
    purple 50%, transparent),
    linear-gradient(to left, red, yellow, white);
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-block-grad {
      background-image: linear-gradient(to bottom, lime 10%, red 30%, purple 50%, transparent), linear-gradient(to left, red, yellow, white);
    }
  </style>
  <div class="h-20 my-block-grad">
  </div>
</div>

---
layout: dynamic-image
image: ./images/gradient.jpg
equal: false
left: false
---

# Gradients (2/3)
Make a great color transition

<Transform scale="0.85">

### Radial gradient
```css {*}{lines:true}
.my-block {
  /* Radial gradients are ellipsis by default.
  Colors radiate equally from center to "borders" */
  background-image: radial-gradient(purple, green, yellow);
}
```

</Transform>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -140}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-basic-radial {
      background-image: radial-gradient(purple, green, yellow);
    }
  </style>
  <div class="h-20 my-basic-radial">
  </div>
</div>
<Transform scale="0.85">
<div v-click>

### Radial as circle
```css {*}{lines:true}
.my-block {
  /*Forcing gradient to be a circle, specifying a radius for each color*/
  background-image: radial-gradient(circle, purple 20px,
    green 25%, yellow 70%);
}
```

</div>
</Transform>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -130}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-circle-radial {
      background-image: radial-gradient(circle, purple 20px, green 25%, yellow 70%);
    }
  </style>
  <div class="h-20 my-circle-radial">
  </div>
</div>
<Transform scale="0.85">
<div v-click>

### Radial ending size
```css {*}{lines:true}
.my-block {
  /* Setting and ending size for our shape: closest-side,
    farthest-side, etc. */
  background: radial-gradient(circle closest-side at 30% 60%,
    purple, green 10%, yellow 50%, blue);
}
```

</div>
</Transform>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -140}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-circle-grad-cs {
      background: radial-gradient(
        circle closest-side at 30% 60%,
        purple,
        green 10%,
        yellow 50%,
        blue
      );
    }
  </style>
  <div class="h-20 my-circle-grad-cs">
  </div>
</div>

---
layout: dynamic-image
image: ./images/gradient.jpg
equal: false
left: false
---

# Gradients (3/3)
Make a great color transition

### Conic gradient
```css {*}{lines:true}
.my-block {
  /* We start from the center and radiate 360 degrees */
  background-image: conic-gradient(red, blue);
}
```

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-basic-conic {
      background-image: conic-gradient(red, blue);
    }
  </style>
  <div class="h-20 my-basic-conic">
  </div>
</div>
<div v-click>

### Conic with specific center and color stops
```css {*}{lines:true}
.my-block {
  background-image: conic-gradient(at 10% 40%, red 10px,
    yellow 30%, blue 60%);
}
```

</div>
<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-advanced-conic {
      background: conic-gradient(at 10% 40%, red 10%, yellow 30%, blue 60%);
    }
  </style>
  <div class="h-20 my-advanced-conic">
  </div>
</div>

<div v-click>

### Starting from a sepcific angle
```css {*}{lines:true}
.my-block {
  background-image: conic-gradient(from 45deg at 25% 50%, red,
    yellow 50%, blue);
}
```

</div>
<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-conic-angle {
      background: conic-gradient(from 45deg at 25% 50%, red, yellow 50%, blue);
    }
  </style>
  <div class="h-20 my-conic-angle">
  </div>
</div>

<img v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 560, y: -275}" class="absolute rounded-md border-2 border-teal-600 h-56" src="/images/gifs/math1.webp" alt="Math thinking GIF" />

---
layout: dynamic-image
image: ./images/gradient.jpg
equal: false
left: false
---

# Gradients (bonus)
Make a great color transition

### Applying gradient on texts
```css {*}{lines:true}
.my-block {
  background-image: linear-gradient(43deg, #4158D0, #C850C0, #FFCC70);
  color: transparent;
  background-clip: text;
}
```

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 min-h-20 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <style>
    .my-grad-text {
      background-image: linear-gradient(43deg, #4158D0, #C850C0, #FFCC70);
      color: transparent;
      background-clip: text;
    }
  </style>
  <p class="my-grad-text text-xl font-bold">Look at me! I’m beautiful :)</p>
</div>

<div v-click>

Link to [CSS gradient generator](https://www.learnui.design/tools/gradient-generator.html)

</div>

---
layout: intro
image: ./images/disco.jpg
---

<h1 class="absolute left-12 bottom-12">You are now ready to disco.</h1>
<p class="opacity-80 absolute left-12 bottom-6">Shake it, shake it!</p>

<img src="/images/gifs/cat-disco.webp" class="absolute right-12 top-[20%] border-2 border-white rounded-md max-h-[50%]" alt="Cat disco Gif" />

---
layout: dynamic-image
image: ./images/shadow.jpg
equal: false
---

# Shadows
Come to the dark side, we have cookies 🍪

CSS3 blesses us with the another gift: shadows! There are two types of shadows:

<v-clicks>

- **box-shadow**: add some depth to your containers, images, etc.
- **text-shadow**: make your texts pop, but with moderation please

</v-clicks>

<ComplementaryMessage bordered>Like gradients, you can apply multiple shadows for a single element.</ComplementaryMessage>

---
layout: dynamic-image
image: ./images/shadow.jpg
equal: false
---

# Shadows (1/2)
Come to the dark side, we have cookies 🍪

### box-shadow
```css {*}{lines:true}
.my-block {
  /* Parameters: offset-x | offset-y | color */
  box-shadow: 2px 5px red;
}
```

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: -350, y: -90}" class="absolute w-1/3 min-h-20 p-2 flex justify-center items-center bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-2 shadow-[2px_5px_#ff0000]">Is this really a shadow?</div>
</div>
<div v-click>

### box-shadow with blur and spread
```css {*}{lines:true}
.my-block {
  /* Parameters: offset-x | offset-y | blur | spread | color */
  box-shadow: 2px -5px 10px 3px blue;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: -350, y: -90}" class="absolute w-1/3 min-h-20 p-2 flex justify-center items-center bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-2 shadow-[2px_-5px_10px_3px_#0000FF]">That’s better!</div>
</div>
<div v-click>

### Inset box-shadow
```css {*}{lines:true}
.my-block {
  /* Parameters: offset-x | offset-y | blur | color |inset */
  box-shadow: 2px 2px 10px green inset;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: -350, y: -90}" class="absolute w-1/3 min-h-20 p-2 flex justify-center items-center bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-2 shadow-[2px_2px_10px_#00FF00_inset]">That’s better!</div>
</div>

<div v-click>

More on [box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow)

</div>

---
layout: dynamic-image
image: ./images/shadow.jpg
equal: false
---

# Shadows (2/2)
Come to the dark side, we have cookies 🍪

### text-shadow
```css {*}{lines:true}
.my-block {
  /* Parameters: offset-x | offset-y */
  text-shadow: 2px 2px;
}
```
<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: -350, y: -90}" class="absolute w-1/3 min-h-20 p-2 flex justify-center items-center bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-2 text-shadow-[2px_2px]">My eyes hurt, make it stop!</div>
</div>
<div v-click>

### Stacked shadows with color and blur
```css {*}{lines:true}
.my-block {
  /* Parameters: offset-x | offset-y | blur | color */
  text-shadow: 1px 1px 3px red, -2px -2px 3px blue;
}
```

</div>
<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: -350, y: -90}" class="absolute w-1/3 min-h-20 p-2 flex justify-center items-center bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-2 text-shadow-[1px_1px_3px_#FF0000,-2px_-2px_3px_#0000FF]">That’s better now.</div>
</div>

<div v-click>

More on [text-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/text-shadow)

</div>

---
layout: dynamic-image
image: ./images/round.jpg
equal: false
left: false
---

# Rouded borders
Is it a circle? Is it an ellipse? Well, it’s rounded

Assign a radius to horizontal and vertical axis so edges of your elements get rounded.

<div v-click>

```css {*}{lines:true}
.my-block {
  /* One parameter sets the radius for every edge */
  border-radius: 10px;
  border: 1px solid red;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-4 border border-red rounded-[10px]">I’m rounded in all the right places.</div>
</div>

<div v-click>

```css {*}{lines:true}
.my-block {
  /* Two parameters set the radius diagonally */
  border-radius: 10px 5px;
  border: 1px solid green;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-4 border border-green rounded-[10px_5px]">I’m rounded but not symmetrical.</div>
</div>

<div v-click>

```css {*}{lines:true}
.my-block {
  /* Four parameters set the radius for each side starting top left */
  border-radius: 2px 4px 6px 8px;
  border: 1px solid blue;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-4 border border-blue rounded-[2px_4px_6px_8px]">I’m rounded but not symmetrical.</div>
</div>

---
layout: dynamic-image
image: ./images/round.jpg
equal: false
left: false
---

# Rouded borders
Is it a circle? Is it an ellipse? Well, it’s rounded

Different radius for horizontal and vertical axis; Ellispis, here we come.

<div v-click>

```css {*}{lines:true}
.my-block {
  /* Radius x-axis / Radius y-axis */
  border-radius: 20px / 10px;
  border: 1px solid blue;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-4 border border-blue rounded-[20px/10px]">I’m all funky!</div>
</div>

<Transition
  enter-active-class="transition-opacity duration-75 delay-600"
  enter-from-class="opacity-0"
  enter-to-class="opacity-100"
  leave-active-class="transition-opacity duration-150"
  leave-from-class="opacity-100"
  leave-to-class="opacity-0"
>
  <div v-if="$clicks >= 2">
    <arrow x1="632" x2="632" y1="191" y2="210" color="red" width="1" />
    <arrow x1="635" x2="665" y1="187" y2="187" color="red" width="1" />
    <span class="absolute text-[10px] text-red right-75 top-[34%]">20px</span>
    <span class="absolute text-[10px] text-red right-81 top-[36%]">10px</span>
  </div>
</Transition>

<div v-click>

```css {*}{lines:true}
.my-block {
  /* Radius x-axis / Radius y-axis */
  border-radius: 10px 5px / 5px 10px;
  border: 1px solid green;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-4 border border-green rounded-[10px_5px/5px_10px]">I’m even more funky!</div>
</div>

<div v-click>

```css {*}{lines:true}
.my-block {
  border-radius: 50%;
  width: 50px;
  height: 50px;
  border: 1px solid red;
}
```

</div>

<div v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 570, y: -100}" class="absolute w-1/3 p-2 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="p-1 flex items-center justify-center border border-red h-12 w-12 rounded-full mx-auto text-[8px]">I’m a circle</div>
</div>

<img v-motion v-click :initial="{x: 999, y: -999}" :enter="{x: 555, y: -285}" class="max-h-50 absolute rounded-md border-2 border-teal-600 h-56" src="/images/gifs/math2.webp" alt="Math thinking GIF" />

---
layout: intro
image: ./images/quiz.jpg
---

<h1 class="absolute left-12 bottom-12">Quiz time</h1>

<img src="/images/gifs/deja-vu.webp" class="absolute right-12 top-[30%] border-2 border-white rounded-md" alt="Déjà vu Gif" />

---
layout: dynamic-image
image: ./images/question.jpg
equal: false
---

# Get crackin’
Who dis?

<div class="p-4 bg-gray-700 text-white dark:text-gray-800 dark:bg-white rounded-md border-2 border-teal-600">
  <div class="shadow-md rounded-md p-8 text-center bg-white/70">
    <img class="max-h-24 rounded-full border border-white shadow-md inline-block" src="/images/hodor.png" alt="This is Hodor of course!" />
    <h6 class="text-3xl my-2">HODOR Hodor</h6>
    <p>Hodor hodor hodor hodor hodor hodor hodor hodor.</p>
  </div>
</div>

<ComplementaryMessage type="alert" bordered>Pay attention to shadows and rounded edges…</ComplementaryMessage>

---
layout: dynamic-image
image: ./images/time.jpg
equal: false
left: false
---

# Time’s up!
Who wants to write some code?

<div v-click>

```html {*}{lines:true}
<div class="hodor">
  <img src="images/hodor.jpg" alt="This is Hodor of course!" />
  <h1>HODOR Hodor</h1>
  <p>Hodor hodor hodor hodor hodor hodor hodor hodor.</p>
</div>
```

</div>
<div v-click>

```css {*}{lines:true}
.hodor {
  background: white;
  width: 500px;
  padding: 2rem;
  border-radius: 5px;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
  text-align: center;
}
.hodor img {
  max-height: 100px;
  border-radius: 50%;
  border: 1px solid white;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.18);
}
```

</div>

---
layout: intro
image: ./images/thinker.jpg
---

<div class="absolute inset-0 flex justify-center items-center">
  <h1 class="text-6xl !text-white font-500">Questions?</h1>
</div>

<div class="absolute bottom-4 right-4 opacity-50 text-sm italic">
  © Unsplash<br>© Giphy
</div>
