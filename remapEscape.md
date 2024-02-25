
Don't use xmodmap. It's a trap!

Use gnome-tweaks to turn capslock into control
```
sudo apt install gnome-tweaks
gnome-tweaks
```

22.04 with wayland

Install and use gnome-tweak-tool > Keyboard & Mouse > Keyboard > Additional Layout Options > Caps Lock behavior.

"Make Caps Lock an additional Esc

Then

Set `setxkbmap -option 'caps:ctrl_modifier' && xcape -e 'Control_L=Escape'` in Startup Applications or ~/.profile
