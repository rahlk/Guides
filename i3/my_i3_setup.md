# How to _"rice"_ i3

## Packages to install
 - `xbacklight`: Installs backlight control on laptops
 - `arandr`: For controlling display parameters
 - `feh`: For setting wallpaper

## Configurations


### 1. Turn on fn-keys
```
# Pulse Audio controls
bindsym XF86AudioRaiseVolume exec --no-startup-id pactl set-sink-volume 0 +5% #increase sound volume
bindsym XF86AudioLowerVolume exec --no-startup-id pactl set-sink-volume 0 -5% #decrease sound volume
bindsym XF86AudioMute exec --no-startup-id pactl set-sink-mute 0 toggle # mute sound

# Sreen brightness controls
bindsym XF86MonBrightnessUp exec xbacklight -inc 20 # increase screen brightness
bindsym XF86MonBrightnessDown exec xbacklight -dec 20 # decrease screen brightness

# Touchpad controls
bindsym XF86TouchpadToggle exec /some/path/toggletouchpad.sh # toggle touchpad

# Media player controls
bindsym XF86AudioPlay exec playerctl play
bindsym XF86AudioPause exec playerctl pause
bindsym XF86AudioNext exec playerctl next
bindsym XF86AudioPrev exec playerctl previous
```

### Wallpapers
`exec_always --no-startup-id feh --bg-scale absolute/path/to/wallpapers`

### Assign Workspaces
```
set $workspace1 "1. Terminals"
set $workspace2 "2. Browser"
set $workspace3 "3. Coding"
set $workspace4 "4. Email"
set $workspace5 "5. Slack"
set $workspace6 "6. Mendeley"
set $workspace7 "7. Spotify"
set $workspace8 "8. Mics. 1"
set $workspace9 "9. Misc. 2"
set $workspace0 "10. Misc. 3"

# switch to workspace
bindsym $mod+1 workspace $workspace1
bindsym $mod+2 workspace $workspace2
bindsym $mod+3 workspace $workspace3
bindsym $mod+4 workspace $workspace4
bindsym $mod+5 workspace $workspace5
bindsym $mod+6 workspace $workspace6
bindsym $mod+7 workspace $workspace7
bindsym $mod+8 workspace $workspace8
bindsym $mod+9 workspace $workspace9
bindsym $mod+0 workspace $workspace0

# move focused container to workspace
bindsym $mod+Shift+1 move container to workspace $workspace1
bindsym $mod+Shift+2 move container to workspace $workspace2
bindsym $mod+Shift+3 move container to workspace $workspace3
bindsym $mod+Shift+4 move container to workspace $workspace4
bindsym $mod+Shift+5 move container to workspace $workspace5
bindsym $mod+Shift+6 move container to workspace $workspace6
bindsym $mod+Shift+7 move container to workspace $workspace7
bindsym $mod+Shift+8 move container to workspace $workspace8
bindsym $mod+Shift+9 move container to workspace $workspace9
bindsym $mod+Shift+0 move container to workspace $workspace0
```
### 4. Binding applications to workspaces

- Open up a terminal beside your application. Then run `xprop`. Then click on
  the application. This will dump some text on the console like so
  ```
  ...
  WM_CLASS(STRING) = "spotify", "Spotify"
                                 ````````
                                    ^
                                    |__  Copy this string
  ...
  ``` 

