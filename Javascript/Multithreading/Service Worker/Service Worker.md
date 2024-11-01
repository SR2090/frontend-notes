---
tags:
  - worker
  - serviceworker
---

What is it ?
A type of worker.


Features:

Act as a network proxy browser, webapp and webserver.
A Service Worker sits between the web application and the network, allowing it to manage how network requests are handled.

Intercept and handle network request, cache resources

Enable offline functionality and push notification.
Have a lifecycle managed by the browser (install, activate, update).
No access to DOM and main thread resources for security.



Usage:
Caching
Offline Support
Request Handling
Background Sync


## Code Example
```js
if ('serviceWorker' in navigator) {

  navigator.serviceWorker

    .register('/service-worker.js')

    .then(function (registration) {

      console.log('Service Worker registered:', registration);

    })

    .catch(function (err) {

      console.log('Service Worker registration failed:', err);

    });

}
```

```js
self.addEventListener('fetch', function (event) {

  event.respondWith(

    caches.match(event.request).then(function (response) {

      // return cached response if available

      if (response) {

        return response;

      }

      // Otherwise, fetch from network

      return fetch(event.request);

    }),

  );

});
```