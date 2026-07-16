# Termux Voidrice

Luke Smith's dotfiles, now in
[Termux](https://f-droid.org/packages/com.termux/).

- Very useful wrappers are in `scripts/`:
  - mimeopen wrapper for termux-share
  - pactl/wpctl wrapper for termux-volume
  - pacman wrapper for apt
- Gruvbox colors for Termux.
- Terminus font for Termux.
- Settings for Termux extra keys.

This config is intended to go with the
[Termux:API](https://f-droid.org/packages/com.termux.api/) companion app.

I also recommend checking out my
[tmux setup](https://github.com/ncv-xyz/tmux-dwm) to make Termux more like
LARBS on tty.

## Install this config and all dependencies

For dependencies, see [progs.csv](progs.csv).

Clone [the Voidrice]() into `~/`, then clone this repo into `~/.config/termux`
and link `~/.termux` and `~/.zprofile`:

```fish

ln -sfT ~/.termux .config/termux
ln -sfT ~/.zprofile .config/termux/profile
```

Also add these lines to the end of `~/.config/zsh/.zshrc`:

```fish
# Load Termux zshrc, will actually load the syntax highlighting.
[ -n "$TERMUX_VERSION" ] && source "${XDG_CONFIG_HOME:-$HOME/.config}/termux/zshrc" 2>/dev/null
```

## Advanced configuration

LARBS also installs these packages not listed in the progs.csv, I recommend
installing them:

```
curl ca-certificates build-essential \autoconf automake binutils findutils gawk grep groff gzip sed bison gettext m4 texinfo flex libtool pkg-config file patch which libllvm git zsh dash
```

Make dash the default non-interactive shell:

```fish
ln -sfT "$PREFIX/bin/dash" "$PREFIX/bin/sh"
```

Do not install "Recommended" packages through apt:

```fish
echo 'APT::Install-Recommends "0";' >"$PREFIX/etc/apt/apt.conf.d/no-recommends.conf"
```

Change DNS from Google to Mullvad:

```fish
echo "nameserver 194.242.2.2" >"$PREFIX/etc/resolv.conf"
```

## Patches

Included in `patches/` are patch files for somethings. To apply them, run from
`~/` (replace `PATCH` with the path to the patch):

```fish
patch -p1 <PATCH.patch
```
