# Astro JSON Element

Create/define HTML elements using JSON objects

## How to use

#### Install package
```
npm i  astro-json-element
```

#### Define object and import

```
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
```

__Output:__

```
<h1 id="my-heading" class="heading">Heading</h1>
```

## Example

![Navbar](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/navbar.PNG)

```
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

## API

### tag

Defines what HTML tag the element will be

### text

Set the text of an element, automatically escaped

### innerHTML

Set the innerHTML of an element, a string of HTML

### class

The class attribute can be defined using objects, arrays, sets, and strings using [class:list](https://docs.astro.build/en/reference/directives-reference/#classlist) directive

### ...attrs

Define any attribute inside your element

```
my_element: {
    tag: "span",
    id: "my-element",
    key: value,
}

<Element {...my_element}/>
```

__Output:__

```
<span id="my-element" key="value"></span>
```

(tag, text, innerHTML, and _child elements will not be added as attributes)

### _[child]

Define another JSON Element inside of your JSON object by putting a _ in front of the key of your child element (name does not matter)

![Header](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/header.PNG)

```
const header = {
    tag: "header",
    style: "display:flex;justify-content:center;background-color:white;border:3px solid purple",
    _heading: {
        tag: "h1",
        text: "Purple Heading",
        style: "font-weight:bold;font-size:3rem;color:purple;"
    }
}

<Element {...header}/>
```

Elements can be nested inside of each other

![List](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/list.PNG)

```
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

<Element {...list}/>
```
