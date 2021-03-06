# peekaboo.js

Do something with _everything_ when it's in viewport.
E.g. use it for lazy-loading images or fancy animation.

Plain JS (no frameworks required). AMD or CommonJS ready.

## Usage

Add to your HTML:

```html
<script src="path/to/peekaboo.js"></script>

// ... or minified version
<script src="path/to/peekaboo.min.js"></script>
```

The actual call looks like: 

```js
peekaboo(ELEMENTs, OPTIONS);

// AMD
reguire(['peekaboo'], function(peekaboo) {
    peekaboo(ELEMENTs, OPTIONS);
});
```

### Variables

You can pass two variables to the peekaboo function.

The fist one (ELEMENTs) is required.
The second one (OPTIONS) is optional. See default values below.

#### `@param *` ELEMENTs

ELEMENTs could be anything of type:
- CSS selector (string)
- NodeList
- HTMLCollection
- HTML...Element

#### `@param object|function` OPTIONS

|Option|Type|Description|Default|
|------|----|-----------|-------|
|threshold|integer or string|Threshold in px when callback should be called. Use a positive number to call before entering the viewport or a negative one to call when element is already in viewport.|0|
|loadInvisible|boolean, integer or string|_Peekaboo_ elements although they are not in viewport yet. Possible values: `true`, `false`, `'vertical'` or `'horizontal'`|`false`
|class|string|Classname the element gets once it's triggered _in viewport_.|peekaboo|
|callback|function|Function to call on the _event_. The current element is binded to the function (`this`) and the object of options is passed as variable with it.|`function(options) {}`|
... or any custom option you want to pass.

**Shortcut**: If you only have a callback to pass you can simply pass the function instead of an object with the item `callback`.

No matter what, the `options['class']` is set to the element once the peekaboo action is triggered,
so you don't even need a `callback` to do awesome stuff. Just use `options['class']` in CSS.

```css
/* by default class is 'peekaboo' */

*:not(.peekaboo) {
    /* whatever should happen before seen */
}

.peekaboo {
    /* whatever should happen when in viewport */
}
```

### Examples

#### Lazy load images

This is the simplest way to _lazy load_ your images and thereby decrease the browser requests and the page's load time.

```html
<img src="path/to/placeholder" data-src="path/to/actual/image" />

<script type="text/javascript">
    peekaboo('img[data-src]', function() {
        this.src = this.getAttribute('data-src');
    });
</script>
```

## Questions, concerns, needs, suggestions?

Don't hesitate! [Issues](https://github.com/enoks/peekaboo.js/issues) welcome.
