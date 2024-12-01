## hyde-gen

working on a tool to generate hyde themes for easier testing and customization
mostly docs for generating hyde themes for now

### Prerequisites

Before starting, you'll need:

1. Required components:
   - A GTK theme (mandatory)
   - Icon pack (optional) - defaults to Tela-circle
   - Cursor theme (optional) - defaults to Bibata-Modern-Ice
   - Font (optional)

2. A collection of wallpapers that match your desired style/color scheme

## Quick Start Guide

1. Choose your base components:
   - Select a GTK theme that you know works well
    - see [Generate GTK](#generate-gtk-from-wallbash) for generating GTK theme from wallpaper
    - or search [Gnome-Look](https://www.gnome-look.org/browse?cat=135&ord=latest) for existing themes
   - (Optional) Pick complementary icon and cursor themes

2. Create your theme:
   - Browse existing themes in `~/.config/hyde/themes`
   - Choose a theme that aligns with your vision
   - Copy and rename it as your new theme

3. Configure your theme:
   - add wallpapers to `~/.config/hyde/Your-Theme/wallpapers`
   - edit the *.theme file to customize the theme

Your theme should have the following structure:

```
~/.config/hyde/Your-Theme/
├── kvantum
├── wallpapers
├── *.theme - hypr, kitty, rofi, waybar, etc
├── wall.set - optional symlink to first wallpaper in wallpapers directory
├── theme.dcol - optional dcol for hard
```

4. Test your theme:
   - Enable wallbash
   - Set your chosen wallpaper as the current wallpaper
   - Observe how wallbash adapts the colors to your wallpaper for the following applications:
     - GTK (nwg-look?)
     - Kitty (kitty)
     - QT (qt5ct + qt6ct)
     - Waybar (waybar)
     - Spotify (spotify)
     - VSCode (code)
     - Cava (cava)

### Understanding *.theme Files:
   - Each *.theme file contains configuration lines
   - The format is: file_path | command_to_execute
   - The first field specifies the target path to be overwritten, ksthe second field (optional) defines commands or scripts to run
      - hypr.theme - `$HOME/.config/hypr/themes/theme.conf|> $HOME/.config/hypr/themes/colors.conf`
      - kitty.theme - `$HOME/.config/kitty/theme.conf|killall -SIGUSR1 kitty`
      - rofi.theme - `$HOME/.config/rofi/theme.rasi`
      - waybar.theme - `$HOME/.config/waybar/theme.css|${scrDir}/wbarconfgen.sh`
   - hypr.theme tips:
      - becomes ~/.config/hypr/themes/theme.conf
      - requires variables and exec commands, variables are first and preffered for performance
       - example: [Bad Blood hypr.theme](https://github.com/HyDE-Project/hyde-gallery/blob/Bad-Blood/Configs/.config/hyde/themes/Bad%20Blood/hypr.theme)

### Generate GTK from wallbash

If your theme doesn't include GTK4 support, pavucontrol and other GTK4 applications may appear with a plain white theme. Here's how to generate GTK4 theme files using wallbash:

1. Use wallbash in auto mode (Meta + Shift + R) and select a wallpaper you like
2. Wallbash will generate two CSS files:
   - `$HOME/.themes/Wallbash-Gtk/gtk-4.0/gtk.css`
   - `$HOME/.themes/Wallbash-Gtk/gtk-4.0/gtk-dark.css`

3. Copy these files to your theme directory:
   ```bash
   # Create GTK4 directory in your theme
   mkdir -p $HOME/.themes/Your-Theme/gtk-4.0
   
   # Copy the generated CSS files
   cp $HOME/.themes/Wallbash-Gtk/gtk-4.0/*.css $HOME/.themes/Your-Theme/gtk-4.0/
   ```

### Generating kvantum from wallbash
1. wallbash auto mode (Meta + Shift + R) and select a wallpaper you like
2. `cp ~/.config/Kvantum/wallbash.kvconfig ~/.config/hyde/themes/Your-Theme/kvantum/kvconfig.theme`
3. `cp ~/.local/share/wallbash/wallbash.svg ~/.config/hyde/themes/Your-Theme/kvantum/kvantum.theme`

### Adding Themes to hyde-gallery

1. Create a directory for your theme:

`mkdir -p ~/Your-Theme/Config/.config/hyde/themes/Your-Theme`
`cp -r ~/.config/hyde/Your-Theme ~/Your-Theme/Config/.config/hyde/themes/Your-Theme`
Copy icons and cursor archives to `~/Your-Theme/arcs` with the following structure:

```
mkdir -p ~/Your-Theme/Source/arcs/
├── Gtk_<Your-GTK-Theme>.tar.xz
├── Cursor_<Your-Cursor-Theme>.tar.xz
└── Icon_<Your-Icon-Theme>.tar.xz
```

Add some screenshots to `~/Your-Theme/screenshots`
run `generate_readme.py` from the hyde-gallery directory to create a README.md file in your theme directory

`git init && git add . && git commit -m "Initial commit"`

git clone https://github.com/HyDE-Project/hyde-gallery
add your theme to the list and hyde-themes.json

### Misc resources
- good theme reference [Bad-Blood](https://github.com/HyDE-Project/hyde-gallery/tree/Bad-Blood/Configs/.config/hyde/themes/Bad%20Blood)

### what hydegen will do
- provide color templates for 
 - gtk
 - kvantum
- a tool that allows easier testing and color customization of themes

# TODO:
- arc creation guide
- theme.dcol & wall.set.dcol creation guide
- cleanup instructions
- plan the tool and what exactly it will do
