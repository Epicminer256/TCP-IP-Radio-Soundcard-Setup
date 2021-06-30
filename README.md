# TCP-IP-Radio-Soundcard-Setup
This is a tutorial on how to get TCP-IP connection though a soundcard

# Ubuntu or Debian Setup 
(This is written only for debian systems at the moment)

### First, you are going to install Direwolf and TNCAttach

```sh
# Install needed programs using this command
sudo apt install direwolf wget


# Downloads latest build of TNCAttach and places itself inside your home directory
# The folder should be ~/tncattach_amd64/
# You may need to replace this url in the future
cd ~/
wget https://github.com/markqvist/tncattach/releases/latest/download/tncattach_0.1.9_amd64.tar.xz
tar -xf tncattach*.tar.xz
chmod +x ~/tncattach_amd64/tncattach
```

### Now you are going to copy the default config of direwolf to your home directory

```sh
cp /usr/share/doc/direwolf/examples/direwolf.conf ~/direwolf.conf
```

### Now if everything went to plan, we are going to run Direwolf First, then TNCAttach ()

```sh
# Run direwolf in one terminal
direwolf -c ~/direwolf.conf

# Now run tncattach
# Make sure the last IP is changed on every system

sudo ~/tncattach_amd64/tncattach -T -H localhost -P 8001 --ethernet --mtu 576 --noipv6 --ipv4 10.0.0.2/24

# Or use TMUX instead
tmux new-session \; send-keys 'direwolf -c ~/direwolf.conf' C-m \; split-window -v \; send-keys 'sleep 1 && sudo ~/tncattach_amd64/tncattach -T -H localhost -P 8001 --ethernet --mtu 576 --noipv6 --ipv4 10.0.0.2/24' C-m
```
