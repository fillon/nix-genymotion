# Genymotion on Nix

240503:

- nixpkgs-unstable = 3.6.0, doesn't work out of the box - `unable to start the virtual device`

## Delete files from previous installations

```bash
rm -rf ~/.config/Genymobile
rm -rf ~/.local/state/Genymobile
```

## Run genymotion from command line

```bash
nix run github:fillon/nix-genymotion#default
```

## Add to your flake.nix

```nix
# flake.nix

{
    inputs = {
        #...
        nix-genymotion.url = "github:fillon/nix-genymotion";
        nix-genymotion.inputs.nixpkgs.follows = "nixpkgs";
    };
}
```

```nix
# modules/user-stephane/default.nix
...
users.users.stephane = {
    #...
    packages = with pkgs; [
        #...
        inputs.nix-genymotion.packages.x86_64-linux.default
    ];
};
```
