# EpicTreasure - Batteries included CTF VM

## Tools included
* [Pwntools](https://github.com/gallopsled/pwntools)
* [GEF](https://github.com/hugsy/gef)
* [Radare2](https://github.com/radare/radare2)
* [Firmware tools (fmk / qemu)](http://reverseengineering.stackexchange.com/questions/8829/cross-debugging-for-mips-elf-with-qemu-toolchain)
* [angr](https://github.com/angr/angr)
* [ROPGadget](https://github.com/JonathanSalwan/ROPgadget)

And more!

## Docker

```
docker pull rjwalls/epictreasure
docker run --privileged -v ${PWD}:/root/host-share --rm -it --workdir=/root/host-share rjwalls/epictreasure tmux
```

### Tmux
* A new shell spawns a fresh `tmux` session
* `tmux` leader switched to `Ctrl+A`
* `Ctrl+A -` produces a horizontal pane. `Ctrl+A \` produces a vertical pane.
* `Ctrl+A [hjkl]` moves around available panes as vim motion

## Check correct installation

To check the installation of the tools, run the `test.sh` under `/root/`.
