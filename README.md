# things-you-can-do-in-a-web-worker

(List just started, Will grow soon)

A list of available functionality and use cases for web workers. Have something to add? Submit a PR

## APIS

### Web Notifications
https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API/Using_the_Notifications_API

Web Notifications allow you to send pop up style notifications to users even when they do not have your site open.

### XMLHttpRequest
https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest

Lets you make a network request.

### Fetch
https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

The Fetch API is a modern replacement for XMLHttpRequest and is closer to a lot of the libraries we are used to.\

## USE CASES

#### All use cases will use inline workers using the following function

for more info https://medium.com/@dee_bloo/make-multithreading-easier-with-inline-web-workers-a58723428a42#.4m4uweub3
```JS
function createWorker(fn) {
  var blob = new Blob(['self.onmessage = ', fn], { type: 'text/javascript' });
  var url = URL.createObjectUrl(blob);
  
  return new Worker(url);
}

```

### Filtering

Filter large data sets without blocking the UI thread and without making a full round trip to the server.

```JS
var filterWorker = createWorker(function (e) {
  self.postMessage(e.data.filter(function () {
    return e.flagged;
  }));
});

var hugeData = [ ... ];

worker.postMessage(hugeData);
```
