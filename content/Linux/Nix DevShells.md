---
tags:
  - "#linux"
  - nix
---
Want to use specific packages when you `cd` into a directory? Handy for ensuring consistent build environments across multiple machines...

`flake.nix`:
```nix
{
  description = "example devshell environment";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
  };

  outputs = { self, nixpkgs }:
  let
    pkgs = import nixpkgs { system = "x86_64-linux"; };
  in
   {
    devShells.x86_64-linux.default = pkgs.mkShell {
      packages = with pkgs; [
        package1
        package2
        package4
      ];
      shellHook = ''
	    source .env 
      '';
    };
  };
}
```


`.envrc`:
```shell
#!/usr/bin/env direnv
use flake .
```

```shell
direnv allow
```
