---
tags:
  - linux
  - shell
---
Using [cheat.sh](https://cht.sh)
```shell
curl cheat.sh/TOPIC
curl cheat.sh/TOPIC/SUB
curl cheat.sh/~KEYWORD
```

Install client:
```shell
curl https://cht.sh/:cht.sh > ~/bin/cht.sh
chmod +x ~/bin/cht.sh
cht.sh python :learn
cht.sh --shell
```

Tab completion in bash:
```shell
mkdir -p ~/.bash.d/
curl cheat.sh/:bash_completion > ~/.bash.d/cht.sh
. ~/.bash.d/cht.sh
echo '. ~/.bash.d/cht.sh' >> ~/.bashrc
```

Completion (in fish config):
```shell
complete -c cht -xa '(curl -s cheat.sh/:list)'
```