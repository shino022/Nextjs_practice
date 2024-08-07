# [static rendering, dynamic rendering in ssr](https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering)
# Fetching data
- sync fetching -> blocking
- async fetching:
```
    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);
```
Problem: one data request is slower than all the others? 

-> divide ui into smaller chuck, one component one fetch call. once the data is delivered, partially render with [streaming](https://nextjs.org/learn/dashboard-app/streaming)
<details>
  <summary>detail</summary>
 Without Next.js streaming, React components will render only after all subcomponents have resolved their data. Next.js streaming, however, allows for partial rendering, meaning that as soon as a child component's data is available, it can be rendered. This enables a smoother and faster user experience, as parts of the page can be displayed incrementally rather than waiting for all data to load.
</details>

# Streaming
- to isolate `loading.tsx` make a folder with () and put the `loading` and `page` file inside 

- [route groupe](https://nextjs.org/learn/dashboard-app/streaming#fixing-the-loading-skeleton-bug-with-route-groups): escaping the map(filestructure -> route)
- loading: page level streaming
- suspense: component level within a page, more granular, 
    - nextjs is [suspense enabled](https://react.dev/reference/react/Suspense#usage), so it doesn't work in default react unless you use React.lazy bc suspense is built to react to a Promise
    - If one of the child components (without Suspense) has not finished data fetching, it can block the rendering of the parent component, causing the fallback UI of other Suspense-wrapped child components not to be rendered
  
# Partial Prerendering
- a way to handle `Suspense`(react) internally at the frame work level(nextjs)
- with ppr enabled, the suspenses fallback ui is injected (prerendered) into html during build time so it's static

# Router cache
- [client side cache](https://nextjs.org/docs/app/building-your-application/caching#router-cache): prefetched, visited
- use revalidate function to avoid stailed cache
