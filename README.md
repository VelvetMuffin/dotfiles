# Fedora + Hyprland setup

- [Fedora](https://fedoraproject.org/)
- [Hyprland](https://github.com/hyprwm/Hyprland)

https://github.com/VelvetMuffin/dotfiles/assets/132045876/622f9bb0-daeb-4fee-a648-ca9cc0c29227

# Screenshots

System
<img allign="center" src="/images/system.png">

Firefox
<img allign="center" src="/images/firefox.png">

Code Editors
<img allign="center" src="/images/code_editors.png">

Sddm
<img allign="center" src="/images/sddm.png">

# Install

Get a Everything iso of Fedora and do a minimal install

[Rpmfusion](https://rpmfusion.org/)

```sh
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
# AppStream metadata
sudo dnf groupupdate core
# Multimedia
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate sound-and-video
## Hardware Accelerated Codec
# Intel (recent)
sudo dnf install intel-media-driver
# Intel (Old)
sudo dnf install libva-intel-driver
# Hardware codecs with AMD (mesa)
sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
sudo dnf swap mesa-vdpau-drivers mesa-vdpau-drivers-freeworld
# If using i686 compat libraries
sudo dnf swap mesa-va-drivers.i686 mesa-va-drivers-freeworld.i686
sudo dnf swap mesa-vdpau-drivers.i686 mesa-vdpau-drivers-freeworld.i686
# Hardware codecs with NVIDIA
sudo dnf install nvidia-vaapi-driver
```

Dependecies

```sh
sudo dnf install ninja-build cmake meson gcc-c++ libxcb-devel libX11-devel pixman-devel wayland-protocols-devel cairo-devel pango-devel wayland-devel libdrm-devel libxkbcommon-devel mesa-libEGL-devel mesa-libgbm-devel vulkan-loader-devel glslang systemd-devel libseat-devel hwdata-devel libdisplay-info-devel libinput-devel xorg-x11-server-Xwayland-devel xcb-util-renderutil-devel xcb-util-wm-devel imagmagick wl-clipboard nvim thunar ristretto rofi lutris steam wine android-tools waybar wlogout dunst sddm grim slurp jq zsh neofetch btop cava kitty gnome-font-viewer udiskie gcc make pkgconf scdoc pam-devel gtk3-devel gtk-layer-shell-devel
```

Enable sddm service

```sh
sudo systemctl enable sddm
sudo systemctl set-default graphical.target
```

Hyprland

```sh
git clone --recursive https://github.com/hyprwm/Hyprland
cd Hyprland
sudo make install
```

[Xdg-desktop-portal-hyprland](https://github.com/hyprwm/xdg-desktop-portal-hyprland)

```sh
git clone https://github.com/hyprwm/xdg-desktop-portal-hyprland.git
cd xdg-desktop-portal-hyprland
meson build --prefix=/usr
ninja -C build
cd hyprland-share-picker && make all && cd ..
ninja -C build install
sudo cp /hyprland-share-picker/build/hyprland-share-picker /usr/bin
```

[Hyprpicker](https://github.com/hyprwm/hypicker)

```sh
git clone https://github.com/hyprwm/hyprpicker.git
cd hyprpicker
make all
sudo cp /build/hyprpicker /usr/bin
```

[Hyprshot](https://github.com/Gustash/Hyprshot)

```sh
git clone https://github.com/Gustash/hyprshot.git Hyprshot
chmod +x Hyprshot/hyprshot
sudo cp Hyprshot/hyprshot /usr/bin
```

[NvChad](https://github.com/NvChad/NvChad)

```sh
rm -rf ~/.config/nvim
rm -rf ~/.local/share/nvim
git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim
```

[Nix-env setup](https://github.com/dnkmmr69420/nix-installer-scripts)

- Nixpkgs have over 80,000 pkgs to install from and are more up to date than fedora's. You can use nix-env --install to install packages 
```sh
curl -s https://raw.githubusercontent.com/dnkmmr69420/nix-installer-scripts/main/installer-scripts/regular-installer.sh | bash
nix-env --install swww
```
Copying the setup

```sh
git clone https://github.com/VelvetMuffin/dotfiles.git Dotfiles
cd Dotfiles
cp .config ~/
# Sddm theme
git clone https://github.com/aczw/sddm-theme-corners.git
cd sddm-theme-corners
sudo cp -r corners/ /usr/share/sddm/themes/
sudo cp sddm.conf /etc/sddm.conf.d
# Gtklock
git clone https://github.com/jovanlanik/gtklock.git
cd gtklock
make
sudo make install
```

Put the cursor theme and icon theme in .icons folder and put the gtk theme in .themes folder in your home directory

- [Cursor-theme](https://www.pling.com/p/1393084/)
- [Icon-theme](https://gitlab.com/garuda-linux/themes-and-settings/artwork/beautyline)
- [GTK-theme](https://github.com/catppuccin/gtk)

### Firefox css and fonts are present in Fonts and firefox css folder

# Credits
- linuxmobile https://github.com/linuxmobile (Almost all of this setup was based on one of his older setup)
- rxyhn https://github.com/rxyhn (The zsh config was borrowed from his setup)
- yokoffing https://github.com/yokoffing (Betterfox)
- andreasgrafen https://github.com/andreasgrafen (Cascade One-Line Firefox css)
- black7375 https://github.com/black7375 (FirefoxUI-fix)
- miguervila https://github.com/migueravila (The startpage)
- prasnathranagn https://github.com/prasanthrangan (The swww and rofi configs were borrowed from him)
- jovanlanik https://github.com/jovanlanik (Gtklock)
