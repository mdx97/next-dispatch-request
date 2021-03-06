# Next.js API Request Dispatcher

A package to provide a clean way to handle writing discrete method handlers for your Next.js API routes.

# Install

```
npm i next-dispatch-request
```

## Usage

A common way to handle different method types in Next.js is to simply branch based on the method:

```ts
export default function handler(req, res) {
  if (req.method === 'POST') {
    // ... Do POST stuff
  } else if (req.method === 'GET') {
    // ... Do GET stuff
  } else {
    res.setHeader('Allow', ['POST', 'GET']);
    res.send(405).send('Method Not Allowed!');
  }
}
```

This package introduces a new pattern to write request handlers for different methods:

```ts
export default createRequestDispatcher({
  post(req, res) {
    // ... Do POST stuff
  },
  get(req, res) {
    // ... Do GET stuff
  }
});
```

The function that is returned by `createRequestDispatcher` will handle some of the overhead for you by checking if the method has a corresponding handler, and then calling the handler that maps to the method that the requestor sent in the HTTP request. It also handles sending back a 405 error for methods that have no corresponding handler.