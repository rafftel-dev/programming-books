# Linux Basic Command
- make new directory
```
mkdir directoryName
```
- change into directory
```
cd directoryName
```
- delete 
```
rm fileName
rm -r directoryName
```
- superpower
```
add sudo to access restricted permissions
```
- make new file
```
touch fileName
```
- listing directory
```
ls
```
- add text into file
```
touch hello.txt
echo "Hello World" >> hello.txt
```
- extract file text
```
cat fileName <!-- print file content into console -->
```
- compiling apps
Compiling apps usually has it's installation instruction on it's README.md or INSTALL.md of project directory.
But, some of it are using GNU/Make or usually typed as below
```
./configure <!-- if there's config -->
make <!-- compiling apps -->
sudo make install <!-- installing apps -->
```
## Symlink
```
ln -s $HOME/.oh-my-zsh           /root/.oh-my-zsh
ln -s $HOME/.zshrc               /root/.zshrc
```
# Arch
### Reflector
```
sudo reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist
```
## Record Screen
```
ffmpeg -f x11grab -s 1366x768 -i :0.0 foryoubro.mkv
ffmpeg -f x11grab -s 1366x768 -i :0.0 foryoubro.mkv -f pulse -i default -y
```
## Extract mp3 from video
```
ffmpeg -i video.mkv name.mp3
```
## Mount NTFS
```
yay -S ntfs-3g
```
```
sudo ntfsfix /dev/sda5
sudo mkdir /media
sudo mount /dev/sda5 /media
sudo umount /media
```
## Mount Android
```
yay -S simple-mtpfs
```
- mounting
```
simple-mtpfs -l <!-- to check device list -->
simple-mtpfs --device [number] [mountpoint]
```
- umounting
```
fusermount -u [mountpoint]
```
## Default File Open
check default png viewer app
```
xdg-mime query default image/png
```
set zathura as default pdf viewer
```
xdg-mime default org.pwmt.zathura.desktop application/pdf
```
## Set Keyboard Layout
US
```
setxkbmap -layout us
```
Arabic
```
setxkbmap -layout ara 
```
Etc
```
setxkbmap -layout etc 
```
