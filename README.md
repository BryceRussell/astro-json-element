# Astro JSON Element

Define HTML elements using JSON

## Example

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

<Element {...my_header}/>
```

## API

### tag

### text

### innerHTML

### ...attrs