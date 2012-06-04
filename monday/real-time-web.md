# Real time web

Why can we even talk about this? Because of the shift from IE to chrome (and
other related things).

We need to run fast!

### Definitions

- UI before technology
- Proactive, not reactive.
- Synchronised with the 'read world'

### MVC

- Developed in the late 70s - now is THE dominant UI design pattern.
- MultiMVC - makes things more complicated when multiple units of MVC (apps)
  talk to eachother.
- Standard implementation: Start - do stuff - shut down. (In an event loop).
- Web is different! Listen, do stuff for an individual request, return a
  response. End. Session is separate. HTTP is stateless.

### REST

- Coined in 2000 in a CS doctorial dissertation. Descriptive but not
  prescriptive. **RE**presentational **S**tate **T**ransfer.
- The user walks through a state machine by doing things.
- Contraints:
    - Client-server
    - stateless
    - cacheable
    - layered
    - code on demand (optional)
    - uniform
- Websockets: Real TCP connectino via magic HTTP to port 80. Reduces latency
  and allows for real-time push.
    - We lose most of the REST bits here. e.g. can't load balance a websocket
      between servers. Harder to cache etc.
- #! belongs in ONE place only - `#!/bin/bash`!

### Version Control

In the beginning there was a Centralised VCS. Now we get a DVCS - everyone has
a full copy.

### Synthesis

We kinda need eveyrthing everywhere. Bit like in DVCS.

- Backbone.js is the biggest implementation
- Also cappuccino which is Cocoa in JS (mostly)
- We have IMAP but we need SMTP (whatever the difference is?)
- If Alice makes a PUT to the server then the server should make a PUT to Bob.

What does this give us?

- Caching. Read RFC2616. Read the spec for the HTTP protocol. Seriously.
  There's some boring stuff in there, but a lot of wisdom too.
- Etags. A string identifier in an HTTP response which identifies an object.
- Cache-control???

- Confict resolution. We normally completely ignore this. But we shouldn't. How
  to handle it without reimplementing git?
- 3-tuple of (uri, etag, dirty?)

    if not uri:
        CREATE
    elif is_dirty:
        if local_etag == remote_etag:
            OK
        else:
            CONFLICT
    else:
        if local_etag == remote_etag:
            NOOP
        else:
            REDOWNLOAD

- Implications:
    - Assumes that resources are orthogonal. Once change results in one change
      for everyone.
    - Lossless representations
    - Authentication and Autorization.
    - Pub/sub. It's expensive to do this kind of app! You need a clever
      scaleable architecture.
    - Resource oriented client. You will want something like Backbone. Design
      your API to match the UI, not necessarily the other way around.

- Pub/Sub:
    - Message queueing: AMQP? 0MQ? Or just Django Signals?

- Barriers: What makes it hard in Django?
    - Django ORM. Do stuff which only works in YOUR db. Who cares if it doesn't
      work on some other DB? This matters for the framework, not for your app.
    - Content negotiation. Make the same view do different things depending on
      what is asked of it (and on the same URI!)
    - Javascript. We've got to have some!
    - Proxies and Middleware. A standard HTTP site can be given Varnish or
      Memcached or whatever which makes it FAST. Can't do that on a websocket
      (yet).
