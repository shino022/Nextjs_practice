# [static rendering, dynamic rendering in ssr](https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering)
# Fetching data
- sync fetching -> blocking
- async fetching like
```
    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);
```
Problem: one data request is slower than all the others? -> divide ui into smaller chuck, one component one fetch call so partially render
