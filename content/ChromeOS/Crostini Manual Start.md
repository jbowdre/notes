---
tags:
  - chromeos
  - crostini
  - troubleshooting
---
If the Linux Development Environment isn't starting normally for you, you might see if you can start it manually.

Start by pulling up the Chrome OS developer shell (`Ctrl` + `Alt` + `T`) and executing `vmc list`. If it's there, you should see information about the `termina` VM returned:

```shell
crosh> vmc list
termina
Total Size (bytes): 3939495936
```

If it's there, try manually starting it with `vmc start termina`:

```shell
crosh> vmc start termina
(termina) chronos@localhost ~ $
```

From the `(termina)` prompt, check for the default Linux container (named `penguin`) with `lxc list`:

```shell
(termina) chronos@localhost ~$ lxc list
To start your first container, try: lxc launch ubuntu:18.04
 
+---------+---------+------+------+------------+-----------+
|  NAME   |  STATE  | IPV4 | IPV6 |    TYPE    | SNAPSHOTS |
+---------+---------+------+------+------------+-----------+
| penguin | STOPPED |      |      | PERSISTENT | 0         |
+---------+---------+------+------+------------+-----------+
```

If the `penguin` container is listed, you can then try manually starting it as well - but you'll want to logout back to the `crosh` prompt and then execute `vmc container termina penguin`:

```shell
(termina) chronos@localhost ~ $ logout
crosh> vmc container termina penguin
username@penguin:~$ 
```

If `vmc container termina penguin` doesn't work, you can go back into `termina` and try to run it with `lxc start penguin` and then `lxc exec penguin bash`. That *should* give you a root shell in the container, though without any of the nice ChromeOS integrations. You might be able to fix things from there.

These commands may or may not fix the problem but I hope they will at least provide a bit more information about the issue(s) you're encountering and perhaps allow you to troubleshoot it further.