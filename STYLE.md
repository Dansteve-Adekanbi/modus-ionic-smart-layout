<!-- markdownlint-disable no-inline-html first-line-h1 -->

<p align="center">
  <img src="images/sass.png" alt="sass Logo" width="150" height="auto" />

# :dart: Theming and Styling ionic apps [Go Back](README.md)

## Theming

Adding a new color to ionic is easy.

```sass
:root {
  /** new-color **/
  --ion-color-new-color: #ea6db9;
  --ion-color-new-color-rgb: 234, 109, 185;
  --ion-color-new-color-contrast: #000000;
  --ion-color-new-color-contrast-rgb: 0, 0, 0;
  --ion-color-new-color-shade: #ce60a3;
  --ion-color-new-color-tint: #ec7cc0;
}


.ion-color-new-color {
  --ion-color-base: var(--ion-color-new-color);
  --ion-color-base-rgb: var(--ion-color-new-color-rgb);
  --ion-color-contrast: var(--ion-color-new-color-contrast);
  --ion-color-contrast-rgb: var(--ion-color-new-color-contrast-rgb);
  --ion-color-shade: var(--ion-color-new-color-shade);
  --ion-color-tint: var(--ion-color-new-color-tint);
}

```

read more in the [Ionic theme documentation](https://ionicframework.com/docs/theming/themes)

### Use Native CSS

Use native CSS when possible. Native [functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions) and [variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties) are easier to override than variables stored in preprocessors like Sass.

```scss
// Good ✔
:root {
  --scale-sm: 0.5rem;
  --scale-md: 1rem;
  --scale-lg: 2rem;
}

.padding-block-lg {
  padding-block-end: calc(--scale-lg);
  padding-block-start: calc(--scale-lg);
}

// Avoid ✘
$scale-sm: 0.5rem;
$scale-md: 1rem;
$scale-lg: 2rem;

.padding-block-lg {
  padding-block-end: $scale-lg;
  padding-block-start: $scale-lg;
}

// Good ✔
.foo + .foo {
  border-block-end: 0.55px solid var(--color-list-item-border);
}

// Avoid ✘
.foo + .foo {
  border-block-end: 0.55px solid color($colors, list-item-border);
}
```

### Relative Units

[Absolute units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units#absolute_length_units) make responsive design hard. Use [relative units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units#relative_length_units) instead.

```scss
// Good ✔
:root {
  --scale-sm: 0.5rem;
  --scale-md: 1rem;
  --scale-lg: 2rem;
}

// Avoid ✘
:root {
  --scale-sm: 5px;
  --scale-md: 10px;
  --scale-lg: 20px;
}
```

### Logical Properties

Use [Logical Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties) in place of direction‐relative equivalents when possible. This gives better support for right-to-left languages.

```scss
// Good ✔
.padding-block-sm {
  padding-block-end: var(--scale-sm);
  padding-block-start: var(--scale-sm);
}

.padding-inline-sm {
  padding-inline-end: var(--scale-sm);
  padding-inline-start: var(--scale-sm);
}

// Avoid ✘
.padding-block-sm {
  padding-bottom: var(--scale-sm);
  padding-top: var(--scale-sm);
}

.padding-inline-sm {
  padding-left: var(--scale-sm);
  padding-right: var(--scale-sm);
}
```

### CSS Specificity Hack

Avoid [ID selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors) and the [`!important` rule](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#the_!important_exception). These are [code smells](https://en.wikipedia.org/wiki/Code_smell) and indicate a deeper problem.

Use [Harry Roberts's Specificity Hack](https://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) instead if needed. Refactoring the code to flatten CSS specificity is always your best option.

```scss
// Good ✔
.text-align-center.text-align-center.text-align-center {
  text-align: center;
}

// Good ✔
[id="widget"] {
    text-align: center;
}

// Avoid ✘
#text-align-center {
  text-align: center;
}

// Avoid ✘
.text-align-center {
  text-align: center !important;
}

```

### More tips to Highlight

1. Use native CSS features when possible.
2. Use <a href="http://sass-lang.com/" target="_blank">Sass</a> as the CSS preprocessing format if needed.
3. Use <a href="https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/" target="_blank">BEM syntax</a> as naming convention for CSS selectors and Sass variable names.
4. Namespace all JavaScript hook classes with the <code>js-</code> prefix. Examples:

```scss
.js-animation-preload
.js-scroll-postevent
```

5. Prefix all dynamic state classes with the verbs <code>did-</code>, <code>is-</code>, <code>was-</code> and <code>will-</code>. Examples:

```scss
.did-select
.is-active
.was-clicked
.will-update
```

6. Alphabetize selector properties and <code>@mixin</code>s when possible.

7. Use only relative units of measure: <code>rem</code>, <code>%</code>, <code>vw</code>, <code>vh</code>, <code>vmin</code>. Use <code>em</code>, <code>ex</code>, <code>ch</code> and <code>vmax</code> with caution.

8. Set the root text size to <code>16</code>. This lets you use 0.5rem increments to build your layouts on an 8-point grid.

9. Import Sass variables and partials into each component stylesheet as needed using <code>@import</code> statements.

10. Store global variables and animations in the <code>src/styles.scss</code> or <code>src/styles.css</code> file.

11. Store hacks and other dirty solutions in the <code>src/hacks.scss</code> or <code>src/hacks.css</code> file. Document all hacks inline with the code. See <a href="https://csswizardry.com/2013/04/shame-css/" target="_blank">Harry Robert’s shame.css</a> for details.

12. Avoid CSS IDs as selectors. IDs make overriding styles hard and are used only as hooks for testing. Use CSS classes for selectors.

13. Avoid absolute units of measure: <code>pt</code>, <code>pc</code>, <code>in</code>, <code>cm</code>, <code>mm</code>. Absolute units make responsive design hard. Use <code>px</code> with caution.

15. Avoid units on <code>line-height</code> properties. <code>line-height</code> is always relative to its container’s units.

16. Avoid <a href="https://css-tricks.com/multiple-class-id-selectors/" target="_blank">selector chains</a>. Selector chains make overriding styles hard. Use a new CSS class name instead.

17. Avoid <code>@extend</code>-ing selectors. <code>@extend</code> is bad for performance. Use <code>@mixin</code>s or Sass variables.

18. Avoid shorthand properties like <code>background</code> and <code>padding</code>. Shorthand properties make overriding styles hard. Use longhand properties like <code>background-color</code> and <code>padding-left</code> instead.

19. Avoid magic numbers. Magic numbers are hard to understand. Use <code>@mixin</code>s or Sass variables instead.

20. Avoid using the <code>!important</code> rule. <code>!important</code> makes it extremely difficult to override styles. Use <a href="https://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/" target="_blank">Harry Robert’s CSS Specificity Hack</a> to increase the specificity of CSS classes.

</ul>
