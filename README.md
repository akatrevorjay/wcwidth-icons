# wcwidth-icons

Support fonts with double-width icons in xterm/rxvt-unicode/zsh/vim/…

If fonts with icons like [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts/)
are used with some terminals like rxvt-unicode then icons must have
single-width (Nerd Fonts calls this "Mono" font, generated by Nerd Fonts
Font Patcher with option `--use-single-width-glyphs`) to work correctly.
**This makes icons too small (about ¼ of normal size for most icons).**

To fix this for most applications (like xterm/rxvt-unicode/zsh/…) which
use libc function (like `wcwidth(3)` or `wcswidth(3)`) to get symbol width
you can use provided library in `LD_PRELOAD` environment variable.

To fix some other applications (like vim) you may need to build these
applications with extra patch, provided in [patches/](patches/) directory.

## Install

```sh
# Build libwcwidth-icons.so and copy it to /usr/lib/ by default.
sudo make install
```

### Gentoo Linux

```
sudo layman -a powerman
sudo emerge wcwidth-icons

# Patch Vim
sudo mkdir -p /etc/portage/patches/app-editors/vim{,-core}/
sudo wget https://github.com/powerman/wcwidth-icons/raw/master/patches/vim/wcwidth-icons.patch \
    -O /etc/portage/patches/app-editors/vim/wcwidth-icons.patch
sudo cp /etc/portage/patches/app-editors/vim{,-core}/wcwidth-icons.patch
sudo emerge -1 vim vim-core
```

## Usage

```sh
export LD_PRELOAD=/usr/lib/libwcwidth-icons.so
```

Then run urxvt/xterm/zsh/… using font with double-width icons.
