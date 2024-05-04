---
tags:
- installs
- linux
- docker
---
[hadolint](https://github.com/hadolint/hadolint)
```shell
cat << EOF > $HOME/.local/bin/hadolint
#!/bin/bash
dockerfile="\$1"
shift
docker run --rm -i hadolint/hadolint hadolint "\$@" - < "\$dockerfile"
EOF
```