# Linux swapfile

Copied from https://askubuntu.com/questions/927854/how-do-i-increase-the-size-of-swapfile-without-removing-it-in-the-terminal/1177620#1177620

## Setup required for first time creation of swapfile

```sh
# Make a backup copy of your /etc/fstab file just in case you
# make any mistakes
sudo cp /etc/fstab /etc/fstab.bak

# (Run this command in your terminal, too). This adds a swapfile entry 
# to the end of your `/etc/fstab` File System Table file to re-enable 
# the swap file after each boot
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# View the `/etc/fstab` file to ensure the swapfile entry was added to the 
# end. You should see this at the end of the output:
# ```
# /swapfile none swap sw 0 0
# ```
cat /etc/fstab
```

## Create new swapfile

```sh
swapon --show               # see what swap files you have active
sudo swapoff /swapfile      # disable /swapfile
# Create a new 16 GiB swap file in its place (could lock up your computer 
# for a few minutes if using a spinning Hard Disk Drive [HDD], so be patient)
# (Ex: on 15 May 2023, this took 3 min 3 sec on a 5400 RPM 750 GB 
# model HGST HTS541075A9E680 SATA 2.6, 3.0Gb/s HDD in an old laptop of mine)
time sudo dd if=/dev/zero of=/swapfile count=16 bs=1G
sudo mkswap /swapfile       # turn this new file into swap space
sudo chmod 0600 /swapfile   # only let root read from/write to it, for security
sudo swapon /swapfile       # enable it
swapon --show               # ensure it is now active
```
