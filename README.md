### General
* Use the SCSS syntax.
* Avoid the use of `!important`
* Order “regular” properties alphabetically.

### Naming
* Do not use ID’s for styling. Use classes only.
* ID’s should be used for Javascript selectors, for aria attributes, ie aria-labeledby, for associating labels with inputs, etc, NOT styling as they have too much specificity.
* Define class names this way: `nav-navbar, .video-player, .video-player-controls` etc. – NOT `.videoPlayerCtrls` (no camel case--this should be used for ID’s for Javascript selectors only for quick differentiation) (and little or no shortening--use your best judgement as to whether someone else could understand what class name does)
* If possible, always use functional class names, e.g. `selected-tab`. Second best is presentational class names, e.g. `solid-border`. Worst for large projects such as ours are content-based names as they are less modular, e.g. `profile-picture`.
Additional reference [here](http://lesscss.org/features/#variables-feature).
* Use variables such as `@link-color` that are function- or content-based if possible, not presentational, such as `@blue-text`.  Additional reference here.
* Always start with the naked element type selector (such as `p` or `h1`), and only add a class if you are extending what it can do for certain elements.
* If possible, avoid the descendant combinator in your selectors high up on the DOM tree that use tags, for example:
```
.header p { }  
.container div { }  
.sidebar h2 { }
```
* Instead, use the closest parent element possible, avoiding any elements that make up major parts of your layout. Additional reference [here](http://www.impressivewebs.com/when-to-avoid-descendant-selector/).
* Better yet, use `>` direct descendant selector, or add classes to right-most tag, especially if there will be a great deal of these elements on the page.
* Do not use `>` direct descendant selector except with tags to right.
```
.selected-tab > a {
   color: #222;
}
```
* Don’t [nest selectors](http://cssguidelin.es/#nesting) unless absolutely necessary, as this makes the style hard to override.

### Sass-specific
* Follow best practices for nesting:
Maximum nesting: three levels deep
See more [here](https://css-tricks.com/sass-style-guide)
* Avoid overusing `@extend.` Unless you are `@extending` vendor code, use a mixin or the [placeholder hack]http://csswizardry.com/2014/01/extending-silent-classes-in-sass/. Additional reference [here](http://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin).
* Use `@extend` to share traits among explicitly related rulesets. For example:
```
.btn,
%btn {
    display: inline-block;
    padding: 1em;
}

.btn-positive {
    @extend %btn;
    background-color: green;
    color: white;
}

.btn-negative {
    @extend %btn;
    background-color: red;
    color: white;
}

.btn-neutral {
    @extend %btn;
    background-color: lightgray;
    color: black;
}
```
* Variablize all common numbers, and numbers with meaning
* Variablize all colors
* Variations on a color can often be handled by the [Sass](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html) or [Bourbon](http://bourbon.io/docs/#tint-shade) color functions like lighten() and darken(). This makes updating colors easier: change in one place, whole color scheme updates.  Use darken() or lighten() for hover states using background-color variable. This way if background-color changes, hover state will change with it, providing consistent contrast.
* Follow this order:
 1. List `@extend(s)` first
 2. List `@include(s)` next
 3. List "Regular" styles next
 4. Nested pseudo classes and pseudo elements next
 5. Nested selectors last
* Never write vendor prefixes. Use Autoprefixer instead.
* Maximum nesting: 50 lines

### Media Queries
* Nest media queries within Sass.

### Architecture
* Global and section-specific Sass files should function as table of contents. Do not include styles directly in them. Keep all styles organized into component parts.
* Break files into as many small files as makes sense. Consult with fellow developers.
* List vendor/global dependencies first, then author dependencies, then patterns, then parts.

Example:
```
Vendor Dependencies
@import "bourbon";

Authored Dependencies
@import "global/colors";
@import "global/mixins";

Patterns
@import "global/tabs";
@import "global/modals";

Sections
@import "global/header";
@import "global/footer";
```
* Partials are prefixed with an underscore such as `_buttons.scss` to give an indication that they will not compile.
* Add a comment to beginning of partial file so that one can easily see at a glance where it is located //  `layout/_container.scss`

### Comments
* Use `//` instead of `/* */`, so comments will get stripped upon compile.

### Specificity
* Spikes in specificity should be avoided. The general trend should be towards higher specificity later in the stylesheet. You can check the specificity of your stylesheet [here](http://jonassebastianohlsson.com/specificity-graph/), and more info is available [here](http://csswizardry.com/2014/10/the-specificity-graph/).
