# Fedora + Hyprland setup

- [Fedora](https://fedoraproject.org/)
- [Hyprland](https://github.com/hyprwm/Hyprland)

# Screenshots

System
<img allign="center" src="/images/system.png">

Firfeox
<img allign="center" src="/images/firefox.png">

Code Editors
<img allign="center" src="/images/code_editors.png">

# install

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
# intel (recent)
sudo dnf install intel-media-driver
# intel (Old)
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
sudo dnf install ninja-build cmake meson gcc-c++ libxcb-devel libX11-devel pixman-devel wayland-protocols-devel cairo-devel pango-devel wayland-devel libdrm-devel libxkbcommon-devel mesa-libEGL-devel mesa-libgbm-devel vulkan-loader-devel glslang systemd-devel libseat-devel hwdata-devel libdisplay-info-devel libinput-devel xorg-x11-server-Xwayland-devel xcb-util-renderutil-devel xcb-util-wm-devel imagmagick wl-clipboard nvim thunar ristretto rofi lutris steam wine android-tools waybar wlogout dunst sddm grim slurp jq zsh neofetch btop cava kitty
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

[Nix-env setup](https://github.com/dnkmmr69420/nix-installer-scripts)

```sh
# Nixpks have over 80,000 pkgs to install from and are more up to date than fedora's. You can use nix-env --install to install packages 
curl -s https://raw.githubusercontent.com/dnkmmr69420/nix-installer-scripts/main/installer-scripts/regular-installer.sh | bash
nix-env --install swww
```

# Copy the files from .config to your .config folder or copy the entire thing to ~/

```sh
git clone https://github.com/VelvetMuffin/dotfiles.git Dotfiles
cd Dotfiles
cp .config ~/
```

# Firefox css and fonts are present in Fonts and firefox css folder

# Credits
- linuxmobile https://github.com/linuxmobile (Almost all of this setup was based on one of his older setup)
- rxyhn https://github.com/rxyhn (The zsh config was borrowed from his setup)
- yokoffing https://github.com/yokoffing (Betterfox)
- andreasgrafen https://github.com/andreasgrafen (Cascade One-Line Firefox css)
- black7375 https://github.com/black7375 (FirefoxUI-fix)
- miguervila https://github.com/migueravila (The startpage)