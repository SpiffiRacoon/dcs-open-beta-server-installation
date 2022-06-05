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
```● xrdp.service - xrdp daemon
     Loaded: loaded (/lib/systemd/system/xrdp.service; enabled; vendor preset: >
     Active: active (running) since Thu 2022-06-02 19:49:58 CEST; 27min ago
       Docs: man:xrdp(8)
             man:xrdp.ini(5)
 ```
             
This tells us it's active and loaded.

## 2 Remote into server from windows.

Now that xrdp is setup in linux we should make sure we have the servers ip-address. You can do this in multiple ways but two them are the following:

### For public ip:
```curl http://ipinfo.io/ip```

### For private ip(lan):
```sudo apt install net-tools```

then

```ifconfig```

and then look for inet... where your ip should be.

Now we should be done with linux for a little bit so we can logout of the ssh session.

### Starting Remote Desktop Connection.

Search for Remote Desktop Connection in windows:

![image](https://user-images.githubusercontent.com/66997364/171703613-36f81409-daf5-4eaf-9375-a0035dc421e5.png)

Start it and type the ip address that you fetched earlier into the computer field:

![image](https://user-images.githubusercontent.com/66997364/171704101-6d125d44-a529-4025-8f57-f7f9ec617711.png)

Now a login window should appear. Type in the username of the user on the server you want to login as like the (admin account) and the password for that account.

![image](https://user-images.githubusercontent.com/66997364/172075457-e1bfb4f8-4745-442f-9075-c3c3c13d1a95.png)

If you have trouble logging in make sure that no other person is logged into the same acoount that you are trying to connect to at the same time.

Now we should have a remote desktop linux environment infront of us!!!!

## 3 Install wineHQ

Now we wanna install wine in order for us to be able to run windows applications.

The most up to date installation guide can be found at: https://www.winehq.org/

You can find instructions for diffrent distros but in my case the package was installed on ubuntu 22: https://wiki.winehq.org/Ubuntu

### The following commands is for installing it on ubuntu 22.04:

**Make sure you have 32 bit architecture enabled before installing the package**

```sudo dpkg --add-architecture i386```

**then download and add repo key:**

```wget -nc https://dl.winehq.org/wine-builds/winehq.key```

*then*

```sudo mv winehq.key /usr/share/keyrings/winehq-archive.key```

**after this add the repo:**

```wget -nc https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources```

*then*

```sudo mv winehq-jammy.sources /etc/apt/sources.list.d/```

**install wine:**

```sudo apt update```

*then*

```sudo apt install --install-recommends winehq-staging```

### Some wine configurating before we move on:

Now default compatibility mode in will be set to Windows 7 we need to set it to Windows 8.1, in the terminal type:

```winecfg```

*If it asks you to install wine mono hit install.*

![image](https://user-images.githubusercontent.com/66997364/171719494-63dcc9c6-6c69-4cd6-bf3f-88834d341b6e.png)



