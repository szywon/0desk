# Zero Desktop Environment Survivor Kit

An opinionated set of configs and tools for living without a "proper" desktop environment.

Here's how it looks like:

![0desk screenshot](http://szywon.github.com/0desk/screenshot.png)

Included stuff:

- some utils in bin
- xinitrc and Xresources
- configs for fontconfig with pretty rendering and some common overrides (for sans-serif override you need the Source Sans Pro font)
- configs for openbox
- a simple GTK2 and GTK3 theme (based on Reverse and Adwaita respectively, they share colours but look is mostly like in the originals)
- tint2 theme

## Scripts in bin

**xlock** and **autolock**: `autolock` is a background task that listens to dbus and launch xlock when computer is going to sleep or hibernate modes. `xlock` is a wrapper for i3lock that show an image of a lock :).

**zzz** puts computer to sleep using dbus. `zzz hard` puts computer to hibernate mode.

**deadmouse** is a dead pilot for DeaDBeeF.
It's designed to be used with a wireless mouse to control the player.
It displays a full-screen window to catch all mouse input (and so you can turn off the monitor).
To turn it off you have to use keyboard like Alt-Tab, Alt-F4, etc.
Button mapping:

- left: toggle play/pause
- back/forwad (the buttons usually under thumb): previous/next track
- middle: `zzz`
- scroll wheel: control volume using `amixer`

**monitors**

    A simple video output controller.
    Allows to compose connected outputs in various ways.
    Discards LVDS1 (the usual laptop screen output) if the lid is closed.

    Usage: monitors <command>

    Commands:

      mirror - set a maximum resolution possible on all monitors
               and display the same view on them
      auto   - set all screens to their automatic resolutions, no change
               to the relative positions is made
      clone  - like 'auto' and positions all views to a shared upper left
               corner
      horiz  - like 'auto' and arrange views horizontally
      vert   - like 'auto' and arrange views vertically

## Usage

Some extra global short-cuts defined Openbox config:

Commands:

- right click on the desktop shows Openbox menu with some predefined apps and actions such as zzz, hibernate power off, etc.
- Alt-F2 -- `xfrun4` (simple run dialog)
- Alt-F3 -- `xfce4-appfinder` (list of all installed apps)
- Win-Return -- `terminal`
- PrintScreen -- screenshot of the whole screen (xfce4-screenshooter)
- Alt-PrintScreen -- screenshot of the active window

Monitors management:

- Win-P -- `monitors auto` (a safe default to activate all connected monitors)
- Brightness Up/Down -- does what's advertised

Windows management:

- Win-F11: full screen (even if application doesn't support this)
- Win-Up/Down: minimizes / maximizes / restores the active window depending on its current state (Win-Up Maximizes, Win-Down restores if maximized and minimizes if it's in normal state).
- Win-Left/Right: maximizes the active window vertically and grows it left or right (shrinks if given edge is met).
- Scroll Up on a title bar: maximize
- Scroll Down on a title bar: restore / minimize
- Scroll Up on task bar: activate
- Scroll Down on task bar: minimize

## Installation

Dependencies (names as in ArchLinux):

> i3lock alsa-utils openbox tint2 feh network-manager-applet batti volumeicon thunar exo terminal pygtk xorg-xrandr xorg-xrdb xorg-xev gnome-icon-theme xfce4-appfinder xfce4-notifyd xfce4-screenshooter

From AUR:

> otf-source-sans-pro

Clone to ~/.0desk or ~/.config/0desk

TDB.

## Development and Pull Requests

Please base your patches on the `src` branch.

## License

MIT, check the COPYING file.
