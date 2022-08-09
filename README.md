# Web Concept

Concept for a pure JS isomorphic HTML library.

Creating your HTML with Javascript functions has the following benefits:

- Reasonably fast
- Isomorphism, functions work both on the server and client side
- No missing end tags or attributes
- Easy to structure your application for imports and testing
- Use only one language to build your application

### How it works

The library consists of a single function `h` that lets you create HTML. It is a proxy object and can be used in a variety of ways.

The proxy object lets you create tags by trying to access non-existent properties on it. It can also be called as a function to let you insert HTML into the DOM for client side rendering.

Some properties have special handling, like `script`, which is used only to embed functions for use client side. Functions passed to `script` will be returned as a string.

Tags are created by passing 3 parameters its function:

- The content (string)
- Attributes (Object)
- More elements (Array)

All strings are escaped unless you wrap them in h['!']:

```js
h['!']('<div>Raw HTML</div>')
```

All arrays are joined with empty strings.

### Usage

```js
function renderList(items) {
  h('#list', h.ul(items.map((item) => h.li(h['!'](item.name)))))
}

function renderSomething(h) {
  h.div('hello', { class: 'nisse' }, [
    h.span('What is going on?', {
      class: 'juletre',
      id: 'funk'
    }),

    h.img({ src: 'https://pixabay.org/hello/1' }),

    h.a({
      href: '/hello',
      onclick: function (e) {
        e.preventDefault()
        alert('Clicked the link!')
      }
    }),

    h.script([
      function doSomething() {
        console.log('What')
      },

      function doSomethingMore() {
        console.log('Do more')
      }
    ]),

    h.script('doSomething()')
  ])
}
```

### Variants

A Weblang version has been explored, but is not really feasible.

```yaml

div:
  @text: hello
  class: nisse

  - span:
    @text: What is going on?
    class: juletre
    id: funk

  - img:
    src: https:ixabay.org
```

WTFPL licensed. Enjoy!
