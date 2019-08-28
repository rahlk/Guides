# How to _"rice"_ i3

## Packages to install
 - `xbacklight`: Installs backlight control on laptops.
 - `arandr`: For controlling display parameters.
 - `feh`: For setting wallpaper.
 - `rofi`: dmenu alternative.
 - `lxappreance`: For setting custom gtk themes.

## Configurations


### 1. Turn on fn-keys

First we wanna install `playerctl`. This is best installed from source. 
Download and install the latest version from https://github.com/altdesktop/playerctl/releases/.

Then, add the following to i3 config:
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
bindsym XF86AudioPlay  exec playerctl --player=spotify play-pause
bindsym XF86AudioPause exec playerctl --player=spotify play-pause
bindsym XF86AudioNext  exec playerctl --player=spotify next
bindsym XF86AudioPrev  exec playerctl --player=spotify previous
```

### Wallpapers
`exec_always --no-startup-id feh --bg-scale absolute/path/to/wallpapers`

### Assign Workspaces
```
set $workspace1 "1. "
set $workspace2 "2. "
set $workspace3 "3. "
set $workspace4 "4. "
set $workspace5 "5. "
set $workspace6 "6. "
set $workspace7 "7. "
set $workspace8 "8.  1"
set $workspace9 "9.  2"
set $workspace0 "10.  3"

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

- Open up a terminal beside your application. Then run `xprop | grep CLASS`. Then click on
  the application. This will dump some text on the console like below. Copy
the second string:
  ```
  WM_CLASS(STRING) = "mendeleydesktop", "Mendeley Desktop"
                                                  ↖ 
                                                   Copy this string
  ``` 
- The add the following lines to the i3 config:
  ```
  assign [class="Mendeley Desktop"] $workspace<X> # <-- <X> is the workspace number to force spotify to open on.
  ```
- In some cases, e.g., spotify, this may not work. Here's the work around:
  ```
  for_window [class="Spotify"] mo/=ve to workspace $workspace<X>
  ```

### 5. Fancy fonts

We'll use [Font Awesome](https://fontawesome.com/). 
  - Go to the github repository at:
    https://github.com/FontAwesome/Font-Awesome and clone it.
  - `cd` into the directory, and then go the the `webfonts` subdirectory. 
  - Copy all the `*.ttf` files into `~/.fonts/` (if it doesn't exist, create
    it.)
  - That's pretty much it. Now, rename the workspaces with the icons. You can
    find them here: https://fontawesome.com/cheatsheet

### 6. Force applications to open in the corresponding workspace.
  - It's always useful to open apps in their assigned workspace (except for
    terminal, of course).
  - We use the `assign [class=<class_string>] $workspace<Y>` command in the i3
    config file to achieve this. 
    + To get `class_string` run `xprop|grep CLASS` and click on the window
      (discussed in §4 above). `Y` will be your preferred workspace number.
  - In my case, I have:
    ```
    assign [class="Google-chrome"] $workspace2
    assign [class="Code"] $workspace3
    assign [class="Mailspring"] $workspace4
    assign [class="Slack"] $workspace5
    assign [class="Mendeley Desktop"] $workspace6
    ```

# 

