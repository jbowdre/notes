---
tags:
  - linux
  - shell
---
Hung/unresponsive SSH session? Type `~.` after a newline to immediately terminate the connection from the client side.

Other useful escape sequences:
```text
 ~.   - terminate connection (and any multiplexed sessions)
 ~B   - send a BREAK to the remote system
 ~C   - open a command line
 ~R   - request rekey
 ~V/v - decrease/increase verbosity (LogLevel)
 ~^Z  - suspend ssh
 ~#   - list forwarded connections
 ~&   - background ssh (when waiting for connections to terminate)
 ~?   - this message
 ~~   - send the escape character by typing it twice
```