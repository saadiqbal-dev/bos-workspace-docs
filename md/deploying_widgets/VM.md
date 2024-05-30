### Working with the VM

In reviewing the nuances of working with the NearSocial/VM, here are some unique properties and handling guidelines for BOS:

1. **Fetch Operation**:

   - The `fetch` function does not return a Promise. Instead, it operates behind a caching layer that will initially miss, invalidate shortly after, and then retrigger a rerender with the populated data. Consequently, you can assume `const data = fetch(…)` will either be null or contain the response. This eliminates the need to handle Promises directly.

2. **AsyncFetch Operation**:

   - Conversely, `asyncFetch` does return a Promise. It can be used with `then` to update state and rerender your component. However, it's generally more efficient to use `fetch`. Reserve `asyncFetch` for cases where requests need to be chained.

3. **Promise Web API**:

   - The traditional Promise Web API remains available for use. Although it's considered old-school, it is reliable and offers a range of helpful methods, such as `Promise.all()`, which handles multiple promises and returns a single Promise that resolves when all input promises are fulfilled.

4. **Improving Promises with useCache**:

   - When working with Promises, the `useCache` function can enhance them. It accepts a key and is utilized across the entire VM, allowing any Widget to access them.

5. **Widget Context**:

   - Widgets operate within their own VM context, essentially acting as individual VMs. When installing near-social-vm into a React gateway, everything begins with `<Widget />`.

6. **Widget Execution**:

   - A widget context parses and executes code line-by-line, only running once unless triggered by a state update or cache invalidation. Consequently, the widget itself cannot be cached.

7. **VM.require**:

   - The `VM.require` method is used for importing stateless modules, which can be cached. These modules will initialize once or when called, making them suitable for static components like Templates and Layouts or reusable functions in SDKs and packages.

8. **Line-by-Line Execution**:

   - Due to the VM’s line-by-line execution, it builds the stack as it reads, leading to some unique quirks, such as being able to access an object while it is being defined.

9. **Importing Packages**:
   - Typical package import syntax is not supported. However, you can fetch modules from a CDN and communicate with them through an iframe.

### Building on BOS

Building on BOS involves mastering the fundamentals while abstracting away complexities to streamline development. The near-social-vm package facilitates easy development, leading to production builds that could potentially replace React dependency for state management with libraries like Zustand.

Our goal is to support web components and engage the community in this development conversation.

For further interaction and updates, visit:

- [near.social](https://near.social)
- [social.near](https://social.near)
- [every.near.page](https://every.near.page)

These platforms allow you to comment on and post pages with various content types, facilitating a collaborative and interactive environment.
