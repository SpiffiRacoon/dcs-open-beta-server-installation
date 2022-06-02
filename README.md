# dcs-open-beta-server-installation

It should start automatically but just to make sure run:

This repo gives instructions for how to get a dedicated dcs linux server to run on open beta version 2.7 using ubuntu 22.04 LTS.

## 1 Setting up remote display protocol (Optional)
This guide is mostly angled towards users who want to start a remote dcs server but who want to save a little bit of money from not having to pay for the windows licence. Therefore we shall start with setting up a remote desktop environment.

First off if your os doesn't have a desktop environment you will need to install your own. One recommendation is to install the reletivly light weight XFCE. SSH into the server and type the following into the console:

```sudo apt update```
```sudo apt upgrade```

Now we have updated our ppa and distro time to install XFCE (OBS if your OS already has a desktop environment you don't need to do this):

```sudo apt install xfce4 xfce4-goodies```

Once we have a desktop environment we can start setting up RDP. Start by installing and enabling xrdp for your linux server:

```sudo apt install xrdp```

It should start automatically but just to make sure run:

```sudo systemctl status xrdp```

The out put shoudd be something like the following:
```
