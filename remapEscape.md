
    Don't use xmodmap. It's a trap!
    Install xcape
    `sudo apt install xcape`
    Use gnome-tweaks to turn capslock into control
    ```
    sudo apt install gnome-tweaks
    gnome-tweaks
    ```
    Use xcape -d to verify that capslock is key 66
    Set xcape -e '#66=Escape' in Startup Applications or ~/.profile
