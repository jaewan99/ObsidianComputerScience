
https://www.geeksforgeeks.org/reactjs/react/
https://react.dev/learn


virtual dom VS actual dom

````JSON

// What actually exists in browser memory:
{
  nodeType: 1,
  nodeName: "HTML",
  tagName: "HTML",
  children: HTMLCollection[...],
  childNodes: NodeList[...],
  parentNode: Document,
  offsetWidth: 1920,           // ← Real DOM has this
  offsetHeight: 1080,          // ← Real DOM has this
  getBoundingClientRect: fn,   // ← Real DOM has this
  addEventListener: fn,        // ← Real DOM has this
  style: CSSStyleDeclaration,  // ← Real DOM has this
  classList: DOMTokenList,     // ← Real DOM has this
  // ... 200+ more properties and methods
  children: [
    {
      nodeType: 1,
      tagName: "BODY",
      offsetWidth: 1920,
      offsetHeight: 900,
      // ... tons more properties
      children: [...]
    }
  ]
} 
````

````JSON

// What React stores in memory:
{
  type: "html",               // ← Simple string
  props: {},                  // ← Just the props you set
  children: [                 // ← Simple array
    {
      type: "body",
      props: {},
      children: [
        {
          type: "h1",
          props: {},
          children: ["Hello"]  // ← Text as string
        }
      ]
    }
  ]
}

````

https://stackoverflow.com/questions/52551853/what-is-the-real-world-example-of-real-dom-and-virtual-dom-in-react
