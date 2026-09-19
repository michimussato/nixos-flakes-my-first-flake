

Create flake:
```shell
nix --experimental-features "nix-command flakes" flake init
```

Flakes need to be tracked
```shell
nix-shell -p git
git init --initial-branch=main
git config user.email "michimussato@etik.com"
git config user.name "Michael Mussato"
git add flake.nix
exit
```

Execute flake
```shell
nix --experimental-features "nix-command flakes" run path:./flake.nix
```

Rebuild system from flake:
```shell
nixos-rebuild switch --flake .
```

Creates `flake.lock`
Update `flake.lock`
```shell
nix --experimental-features "nix-command flakes" flakes update
```

Globally enable experimental features:
```nix
{
  # Enable experimental Features
  nix.settings.experimental-features = [
  	# for `nix run`
    "nix-command"
    "flakes"
  ];
}
```

[Misterio77/nix-starter-configs](https://github.com/Misterio77/nix-starter-configs)

```shell
nix flake init --template github:misterio77/nix-startet-config#standard
# edit flake.nix  # => FIXMEs
# keep ./nixos/configuration.nix
# but change ./hardware-configuration.nix
git add -A
# --impure because access to absolute path /etc/nixos/configuration.nix is forbidden in pure evaluation mode
# --log-format https://nix.dev/manual/nix/2.18/command-ref/new-cli/nix3-log#opt-log-format
sudo nixos-rebuild switch --flake .#<hostname> --impure
```

Reset to default (leave flake?):
```shell
sudo nixos-rebuild switch -I nixos-config=/etc/nixos/configuration.nix
```

https://wiki.nixos.org/wiki/Flakes#See_also

download buffer is full; consider increasing the 'download-buffer-size' setting

---

```shell
NUKE="Nuke15.2v9-linux-x86_64"
tar -tf ${NUKE}.tgz
# tar -xOzvf ${NUKE}.tgz ${NUKE}.run | bash ${NUKE}.run --accept-foundry-eula
tar -xzvf ${NUKE}.tgz
# chmod +x ${NUKE}.run
bash ${NUKE}.run --accept-foundry-eula --prefix=./Nuke
rm ${NUKE}.tgz
rm ${NUKE}.run
```

---

# RnD

```shell
sudo nixos-rebuild boot --flake github:michimussato/nixos-flakes-my-first-flake
```

- https://nixos.asia/en/nixos-install-flake
- https://discourse.nixos.org/t/how-to-get-nixos-install-flake-to-work/10069