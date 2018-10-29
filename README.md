# herbstluftwm-floaty

herbstluftwm-floaty is a fork of [herbstluftwm](http://www.herbstluftwm.org/), a manual tiling
window manager for X. It licensed under the "Simplified BSD License" (see `LICENSE`).

- the layout is based on splitting frames into subframes which can be split again or can be filled with windows (similar to i3/ musca)
- tags (or workspaces or virtual desktops or …) can be added/removed at runtime. Each tag contains an own layout
- exactly one tag is viewed on each monitor. The tags are monitor independent (similar to xmonad)
- it is configured at runtime via ipc calls from herbstclient. So the configuration file is just a script which is run on startup. (similar to wmii/ musca)

For more, see the herbstluftwm homepage http://herbstluftwm.org -- in
particular the [herbstluftwm tutorial](http://herbstluftwm.org/tutorial.html)
for the first steps (also available as `man herbstluftwm-tutorial` after
installing herbstluftwm on your system).

You are welcome to join the IRC channel `#herbstluftwm` on `irc.freenode.net`.

# Floating windows

herbstluftwm-floaty allows you to make individual windows floating without using hacks like
max + pseudotile, unmanaging dialogs, or using an extra monitor locked to a floating tag.

This is done with the `popup` property.  You can toggle this manually with a keybind:

    hc keybind $Mod-Shift-f popup toggle

Or you can set a rule to make dialogs and similar windows popups:

    hc rule windowtype~'_NET_WM_WINDOW_TYPE_(DIALOG|UTILITY|SPLASH)' popup=on

Make sure you have mousebinds for manipulating floating windows:

    # mouse
    hc mouseunbind --all
    hc mousebind $Mod-Button1 move   # Mod + left-click
    hc mousebind $Mod-Button2 zoom   # Mod + middle-click
    hc mousebind $Mod-Button3 resize # Mod + right-click

If the saved size or position of a window is undesirable or makes the dialog unusable, simply
move and resize it as desired. Floating windows typically "remember" their last size; the last
position may be used sometimes, although dialogs are often centered over their parent or
appear in the middle of the screen.

Floating windows can disappear behind other windows. Make sure you can cycle through windows:

    hc keybind $Mod-Tab         cycle_all +1
    hc keybind $Mod-Shift-Tab   cycle_all -1
    hc keybind $Mod-c cycle

`cycle` cycles through windows in a frame and `cycle_all` cycles through the entire tag.
