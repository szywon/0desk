# Zero Desktop Environment Survivor Kit

An opinionated set of configs and tools for living without a "proper" desktop environment.

Here's how it looks like:

![0desk screenshot](http://szywon.github.com/0desk/screenshot.png)

Included stuff:

- some utils in bin for setting wallpaper and configuring monitors (check the bin section below)
- some opinionated configs usable from lift off
  - xinitrc and Xresources
  - configs for fontconfig with pretty rendering and some common overrides (for sans-serif override you need the Source Sans Pro font)
  - configs for openbox
  - tint2 theme

## Scripts in bin

**xlock** and **autolock**: `autolock` is a background task that listens to dbus and launch xlock when computer is going to sleep or hibernate modes. `xlock` is a wrapper for i3lock that show an image of a lock :).

**wallpaper** is a simple GUI wallpaper selector (uses `feh` as the wallpaper setter).

**deadmouse** is a remote control for MPD (used to be for DeaDBeeF).
It's designed to be used with a wireless mouse to control the player.
It displays a full-screen window to catch all mouse input (and so you can turn off the monitor).
To close the application you have to use keyboard like Alt-Tab, Alt-F4, etc.

![deadmouse button mapping](http://szywon.github.com/0desk/dead-mapping.svg)

Button mapping:

- left: toggle play/pause
- back/forwad (the buttons usually under thumb): previous/next track
- middle: `zzz`
- scroll wheel: control volume using `amixer`

**monitors**

    A simple video output controller.
    Allows to compose connected outputs in various ways.
    Treats LVDS1 (the usual laptop screen output) as disconnected
    if the lid is closed.

    Usage: monitors <command> [resolution] [output1 [output2 [...]]]

    Normally connected outputs are detected but you can override
    them by passing them explicitly

    Commands:

      auto [outputs...]
        set all connected or selected monitors to their native resolutions,
        position them all with shared left upper corner
        (useful when setting one monitor only)

      mirror [resolution] [outputs...]
        set selected resolution or the same optimal resolution on all screens

      horiz [outputs...]
        arrange monitors horizontally with their native resolutions
      vert [outputs...]
        arrange monitors vertically with their native resolutions

## Installation

Dependencies (names as in ArchLinux official repos):

> alsa-utils
  batti
  exo
  feh
  gnome-icon-theme
  gnome-themes-standard
  htop
  i3lock
  network-manager-applet
  openbox
  pygtk
  system-config-printer-gnome
  thunar
  tint2
  volumeicon
  xfce4-notifyd
  xfce4-appfinder
  xfce4-screenshooter
  xorg-xrandr
  xorg-xrdb

Optional dependencies from AUR:

-   Source Sans Pro from AUR or from the [repo](https://github.com/adobe/Source-Sans-Pro):
    > otf-source-sans-pro
-   xbrightness to controll brightness in software (if your monitor is too bright in the lowest setting)

Clone to `~/.0desk` or `~/.config/0desk`

The `install.sh` script is intended to set links to files in the repo but it's a TDB for now.

## Usage Tips

There's no menu or launchers in the task bar.
Instead the Openbox menu is used.
It can be reached clicking the right button anywhere on the desktop *or* on the taskbar.

Some extra global short-cuts defined Openbox config:

Commands:

- right click on the desktop shows Openbox menu with some predefined apps and actions such as zzz, hibernate power off, etc.
- Alt-F2 -- `xfrun4` (simple run dialog)
- Alt-F3 -- `xfce4-appfinder` (list of all installed apps)
- Win-Return -- whatever application you have set in "Preferred Applications" `exo-preferred-applications`
- PrintScreen -- screenshot of the whole screen (xfce4-screenshooter)
- Alt-PrintScreen -- screenshot of the active window
- Pause -- play/pause MPD

Monitors management:

- Win-P -- `monitors auto` (a safe default to activate all connected monitors)
- Win-Shift-P -- `monitors mirror`
- Brightness Up/Down -- does what's advertised

Windows management:

- Win-F11: full screen (even if application doesn't support this)
- Win-Up/Down: minimizes / maximizes / restores the active window depending on its current state (Win-Up Maximizes, Win-Down restores if maximized and minimizes if it's in normal state).
- Win-Left/Right: maximizes the active window vertically and grows it left or right (shrinks if given edge is met).
- Scroll Up on a title bar: maximize
- Scroll Down on a title bar: restore / minimize
- Scroll Up on task bar: activate
- Scroll Down on task bar: minimize
- Middle button on task bar: close

## Configuration Tips

### X11 on Login

It's convenient to set X11 to start after login on first virtual terminal (tty1), put this in your `~/.zlogin` or `~/.bash_login`:

    if [ `tty` = /dev/tty1 ]; then
      mv .xsession-errors .xsession-errors.old
      exec startx > .xsession-errors 2>&1
    fi

### SSH Agent

To start SSH agent in your session put this in your `~/.zlogin` or `~/.bash_login`:

    eval `ssh-agent`

## Collaboration

Changes that goes to the visual customization category probably belong to forks but I will welcome any suggestions on how to improve the default configuration even if it doesn't match my taste exactly :).
In that case we can create a fork for the default config and this repo will become an another customization fork.

Any contributions improving the functionality are welcome :).

Some suggestions and how originally I thought about this project:

- minimize dependencies but don't write something if it already exists and can be used without its DE (for example some stuff from XFCE like the exo is used)
- graphical utilities probably should be written in pygtk (like the wallpaper setter and deadmouse) because of the previous point
- avoid hard dependencies (leave the choice of things like a terminal, file manager and a browser to the user, so use `exo-open --launch TerminalEmulator` instead of hardcoding `terminal` for example)

## License

MIT, check the COPYING file.
