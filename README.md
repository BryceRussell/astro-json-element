# Astro JSON Element

Create HTML elements using JS objects

This component was originaly created to interface with html elements inside of a component using props

## Features

- Create html element using js object
- Recursive, create elements inside elements
- Control over render order using `slot` prop
- Add automatically escaped text using `text` prop
- Add a html string using the `innerHTML` prop
- Apply default attributes to all child elements
- `class` attribute uses `class:list` directive (clsx)

## How to use

**Install package**:

```
npm i astro-json-element
```

**Create Element**:

```tsx
---
import { Element } from 'astro-json-element';

const my_element = {
    tag: "h1",
    text: "Heading",
    class: "heading",
    id: "my-heading";
}
---

<Element {...my_element}/>
// <h1 id="my-heading" class="heading">Heading</h1>
```

## Examples

**Headless Pattern Example**: [`<Pagination>`](https://github.com/BryceRussell/astro-bryceguy/blob/master/packages/pagination/pagination/Pagination.astro) component

**Basic Navbar Example**:

![Navbar](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/navbar.PNG)

> **Note**: Styling using the `style` attribute or [tailwindcss classes](https://tailwindcss.com) is easier and keeps your html and css together in the same file/object

```tsx
---
import { Element } from 'astro-json-element';

const header = {
    tag: "header",
    style: "font-family:Arial;display:flex;justify-content:space-around;margin:1rem;border-radius:5px;background-color:white;border:3px solid purple",
    _heading: {
        tag: "h1",
        text: "Purple",
        style: "font-weight:bold;font-size:3rem;color:purple;"
    },
    _ul: {
        tag: "ul",
        style: "display:flex;align-items:center;gap:1rem;font-weight:bold;font-size:1.25rem;color:purple;",
        _item1: {
            tag: "li",
            _link: {
                tag: "a",
                text: "Home"
            }
        },
        _item2: {
            tag: "li",
            _link: {
                tag: "a",
                text: "Products"
            }
        },
        _item3: {
            tag: "li",
            _link: {
                tag: "a",
                text: "About"
            }
        },
        _item4: {
            tag: "li",
            style: "padding:.75rem 1rem;border-radius:5px;background-color:purple;color:white;",
            _link: {
                tag: "a",
                text: "Contact"
            }
        },
    }
}
---

<Element {...header}/>
```

## Render Order

1. slot `first`
2. _[child] slot `first`
3. `text`
4. _[child] slot `before`
5. `slot` (default)
6. _[child] slot `after`
7. `innerHTML`
8. _[child] slot `last`
9. slot `last`

## Slots

**Default**: Elements are slot in at the center of the render order (5 of 9)

### `first`

First element in [Render Order](#render-order)

### `last`

Last elemenet in [Render Order](#render-order)


## Props

### `tag`

**Type**: `string`

**Default**: `div`

Defines what HTML tag the element will be

### `slot`

**Type**: `string`

**Options**: `first`, `before`, `after`, `last`

**Default**: `last`

Controls where a _child element will be rendered inside of a parent json-element

see [Render Order](#render-order)


### `text`

**Type**: `string`

Set the text of an element, automatically escaped

### `innerHTML`

**Type**: `string`

Set the innerHTML of an element, a string of HTML

### `defaults`

**Type**: `object`

Define default props for _child elements

### `debug`

**Type**: `boolean`

**Default**: `false`

If true the element will print its props to the console

### `...attrs`

**Type**: `object`

Any other key/value pairs will be added as attributes to your element

```tsx
---
const my_element = {
    tag: "span",
    text: "Text",
    id: "my-element",
    key: value,
}
---

<Element {...my_element}/>
// <span id="my-element" key="value">Text</span>
```

## `class`

**Type**: `set | object | array | string`

The class attribute uses the `class:list` directive (clsx):

```tsx
---
const my_element = {
    tag: "div",
    class: ['This', 'is', 'a', 'test']
}
---

<Element {...my_element}/>
// <div class="This is a test">Text</div>
```

### `_[child]`

**Type**: `astro-json-element`

astro-json-elements are recursive, you can create elements inside of elements by prefixing a key with `_`

__NOTE:__ Some tags like h1-6 and p tags do not allow children and will slot the child element after the defined element inside the parent element

**Example**:

![Header](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/header.PNG)

```tsx
---
const header = {
    tag: "header",
    style: "display:flex;justify-content:center;background-color:white;border:3px solid purple",
    _heading: {
        tag: "h1",
        text: "Purple Heading",
        style: "font-weight:bold;font-size:3rem;color:purple;"
    }
}
---

<Element {...header}/>
```

![List](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/list.PNG)

```tsx
---
const list = {
    tag: "ul",
    style: "display:flex;align-items:center;gap:1rem;font-weight:bold;font-size:1.25rem;color:purple;",
    _item1: {
        tag: "li",
        _link: {
            tag: "a",
            text: "Home"
        }
    },
    _item2: {
        tag: "li",
        _link: {
            tag: "a",
            text: "Products"
        }
    },
    _item3: {
        tag: "li",
        _link: {
            tag: "a",
            text: "About"
        }
    },
    _item4: {
        tag: "li",
        style: "padding:.75rem 1rem;border-radius:5px;background-color:purple;color:white;",
        _link: {
            tag: "a",
            text: "Contact"
        }
    },
}
---

<Element {...list}/>
```
