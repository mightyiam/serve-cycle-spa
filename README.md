# serve-cycle-spa

> Front-end server for Cycle.js single-page apps

This isn't implemented yet.
Suggestions are very welcome.

## `serve(run, spa[, additionalDrivers])`

<dl>
  <dt>run</dt>
  <dd>Your choice of a Cycle.js run function</dd>
  <dt>spa</dt>
  <dd>Your awesome single-page app</dd>
  <dt>additionalDrivers</dt>
  <dd>An object of drivers for your SPA other than DOM and history</dd>
</dl>

## Your SPA is Bootstrapped

Both in the server
and in the client
your app is bootstrapped *similarly*:

It is
[`run`](https://cycle.js.org/documentation.html#run)
with
a DOM driver, a history driver
and whatever other drivers
you provide.

## On the Server

Server-side bootstrapping
is implemented by
`run`ning your SPA with
an
[HTML driver](https://github.com/cyclejs/cyclejs/tree/master/dom#makeHTMLDriver)
as `DOM`
and
a
[server history driver](https://github.com/cyclejs/cyclejs/tree/master/history#-createserverhistorylocation)
as `history`.

If your SPA
provides output
to the DOM driver
when it
receives input
from the history driver
then you have
server-side rendering.

## On the Client

Client-side bootstrapping
is implemented by
`run`ning your SPA with
[a DOM driver](https://github.com/cyclejs/cyclejs/tree/master/dom#makeDOMDriver)
as `DOM`,
that is "mounted"
in an element
that is in the body.

If you have server-side rendering
then this element
should already be populated
with DOM from the HTML.

It is also provided with
[a history driver](https://github.com/cyclejs/cyclejs/tree/master/history#-makehistorydriverhistory-options)
with [`mjackson/history`](https://www.npmjs.com/package/history).

## Example

``` sh
$ npm i --save serve-cycle-spa @me/my-awesome-cycle-spa
```

`index.js`:

``` js
const serve = require('serve-cycle-spa')

// this is your SPA
const spa = require('@me/my-awesome-cycle-spa')

// your choice of `run`
const { run } = require('@cycle/xstream-run')

// whatever other drivers your SPA uses
const someOtherDriver = require('some-other-driver')
const additionalDrivers = {someOtherDriver}

serve(run, spa, additionalDrivers)
```

``` sh
$ node index.js
Cycle.js SPA is served on port <random port>
```
