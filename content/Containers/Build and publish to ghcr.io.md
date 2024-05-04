---
tags:
  - docker
  - containers
---
Create `Dockerfile` in an empty directory:
```Dockerfile
FROM alpine
CMD ["echo", "Hey vPotato!"]
```

Build it:
```shell
docker build . -t hey-vpotato
```

Run it:
```shell
; docker run hey-vpotato
```

Create GitHub Personal Access Token (PAT) with the `write:packages` scope at https://github.com/settings/tokens

Save token as environment variable:
```shell
export CR_PAT=[YOUR_TOKEN]
```

Use the token to sign in to the container registry:
```shell
echo $CR_PAT | docker login ghcr.io -u jbowdre --password-stdin
```

Edit the `Dockerfile` to insert a label associating it with a public GitHub repo:
```Dockerfile
LABEL org.opencontainers.image.source="https://github.com/jbowdre/hey-vpotato"

FROM alpine
CMD ["echo", "Hey vPotato!"]
```

Build the image again but this time tag it for the registry, then run it, and push it:
```shell
docker build . -t ghcr.io/jbowdre/hey-vpotato:latest
docker run ghcr.io/jbowdre/hey-vpotato:latest
docker push ghcr.io/jbowdre/hey-vpotato:latest
```

Go to to GH packages page at https://github.com/jbowdre/?tab=packages, click on package name, scroll to the bottom and change package visibility to Public.