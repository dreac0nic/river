<div align="center">
  <img src="logo/logo_text_adaptive_color.svg" width="50%">
</div>

## Overview

River is a dynamic tiling Wayland compositor with flexible runtime
configuration.

Install from your [package manager](https://repology.org/project/river/versions) —
Join us at [#river](https://web.libera.chat/?channels=#river) on irc.libera.chat —
Read our man pages, [wiki](https://codeberg.org/river/wiki), and
[Code of Conduct](CODE_OF_CONDUCT.md)

The main repository is on [codeberg](https://codeberg.org/river/river),
which is where the issue tracker may be found and where contributions are accepted.

Read-only mirrors exist on [sourcehut](https://git.sr.ht/~ifreund/river)
and [github](https://github.com/riverwm/river).

*Note: river has not yet seen a stable 1.0 release and it will be necessary to
make significant breaking changes before 1.0 to realize my longer term plans.
That said, I do my best to avoid gratuitous breaking changes and bugs/crashes
should be rare. If you find a bug don't hesitate to
[open an issue](https://codeberg.org/river/river/issues/new/choose).*

## Design goals

- Simple and predictable behavior, river should be easy to use and have a
low cognitive load.
- Window management based on a stack of views and tags.
- Dynamic layouts generated by external, user-written executables. A default
`rivertile` layout generator is provided.
- Scriptable configuration and control through a custom Wayland protocol and
separate `riverctl` binary implementing it.

## Building

On cloning the repository, you must init and update the submodules as well
with e.g.

```
git submodule update --init
```

To compile river first ensure that you have the following dependencies
installed. The "development" versions are required if applicable to your
distribution.

- [zig](https://ziglang.org/download/) 0.11
- wayland
- wayland-protocols
- [wlroots](https://gitlab.freedesktop.org/wlroots/wlroots) 0.17.2
- xkbcommon
- libevdev
- pixman
- pkg-config
- scdoc (optional, but required for man page generation)

Then run, for example:
```
zig build -Doptimize=ReleaseSafe --prefix ~/.local install
```
To enable experimental Xwayland support pass the `-Dxwayland` option as well.

If you are packaging river for distribution, see also
[PACKAGING.md](PACKAGING.md).

## Usage

River can either be run nested in an X11/Wayland session or directly
from a tty using KMS/DRM. Simply run the `river` command.

On startup river will run an executable file at `$XDG_CONFIG_HOME/river/init`
if such an executable exists. If `$XDG_CONFIG_HOME` is not set,
`~/.config/river/init` will be used instead.

Usually this executable is a shell script invoking *riverctl*(1) to create
mappings, start programs such as a layout generator or status bar, and
perform other configuration.

An example init script with sane defaults is provided [here](example/init)
in the example directory.

For complete documentation see the `river(1)`, `riverctl(1)`, and
`rivertile(1)` man pages.

## Licensing

River is released under the GNU General Public License v3.0 only.

The protocols in the `protocol` directory are released under various licenses by
various parties. You should refer to the copyright block of each protocol for
the licensing information. The protocols prefixed with `river` and developed by
this project are released under the ISC license (as stated in their copyright
blocks).

The river logo is licensed under the CC BY-SA 4.0 license, see the
[license](logo/LICENSE) in the logo directory.
