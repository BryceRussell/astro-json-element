# Astro JSON Element

Create/define HTML elements using JSON objects

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

Define any attribute you want for your element

```
my_element: {
    class: "my-element",
    id: "my-element",
    style: "background-color: red;",
    [attribute]: value
}
```

(tag, text, innerHTML, and _child elements will not be added as attributes)

### _[child]

Defined another JSON Element inside of your JSON object by putting a _ in front of the key of your child element (name does not matter)

![Header](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/header.PNG)

```
header: {
    tag: "header",
    style: "display:flex;justify-content:center;background-color:white;border:3px solid purple",
    _heading: {
        tag: "h1",
        text: "Purple Heading",
        style: "font-weight:bold;font-size:3rem;color:purple;"
    }
}
```

Children can also be nested inside of other children to make deeply nested elements

![List](https://raw.githubusercontent.com/BryceRussell/astro-json-element/master/examples/list.PNG)

```
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
```