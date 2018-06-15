# HAgAl

```
  .............................................
  |   @  SHOW  MOVE  ADD  EDIT  DELETE  NEXT  |
  '''''''''''''''''''''''''''''''''''''''''''''
       ==[]====== MOLECULAR DESIGN ============
       |                 H                   /\
       |        AG    H                      ||
       |          .--''. .--..  AG           ||
       |          '.    '     ''             ||
       |  H. .H     |   |                    []
       |  '   '.    '. |      AL             ||
       |       '----'   '-----.        AL    ||
       |             H       '----''''       ||
       |      AL            H                ||
       |                                     ||
       | T R A N S P A R E N T               ||
       |   A L U M I N I U M                 ||
       |                                     \/
       <[]==================================>[]

```

An abstraction over asynchronous, message-driven protocols to allow for full
location transparency, similar in purpose to Akka's transport plugin system.

This allows for code to be developed independently of the underlying messaging
system; for instance, the same application and business logic for a
client/server application could be used in an Electron desktop app (with HAgAl
implementations abstracting the IPC between the Main and Render processes) and
an Express/SPA web app (with HAgAl implementations abstracting a WebSocket
server and client).

[JSON schemas](http://json-schema.org/) are used to define message types ahead
of time, which is then used for message validation, and could be used by HAgAl
implementations for de/serialization.

Message types sent and received are asymmetric to support client/server
scenarios.

All HAgAl implementations use at-most-once, in-order delivery; no message will
be received more than once, and messages may be dropped, but they will never be
received in any order other than that sent for a given client/server pair.

## Implementations

| NPM Package                                           | Transport    | Validation | Connections |
| ----------------------------------------------------- | ------------ | ---------- | ----------- |
| [@hagal/electron-ipc-main](electron-ipc-main)         | Electron IPC | ❌         | 0 ... ∞     |
| [@hagal/electron-ipc-renderer](electron-ipc-renderer) | Electron IPC | ❌         | 1           |
| [@hagal/web-socket-client](web-socket-client)         | WebSocket    | ❌         | 1           |
| [@hagal/web-socket-server](web-socket-server)         | WebSocket    | ✔          | 0 ... ∞     |

The [@hagal/core](core) package additionally defines shared types, but is not
itself a HAgAl implementation.
