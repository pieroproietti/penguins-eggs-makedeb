# penguins-eggs-makedeb

A PKGBUILD for Debian

## Build and install penguins-eggs on Debian

### developer
Copy and paste follow instructions 
```
git clone https://github.com/pieroproietti/penguins-eggs-makedeb
cd penguins-eggs-makedeb
makepkg -srcCi
```


## Configuration (default)

```sudo eggs dad -d```

## add calamares installer (optional)
```sudo eggs calamares --install```

## Create your first iso (default)
All the users will be removed from your live system.

```sudo eggs produce --fast```

### Create a live system including all users
You can use the flag --clone, all users will be saved uncrypted on the live.

```sudo eggs produce --fast --clone```

### Create a live system including all users crypted

You can add the flag --backup: all users will be saved crypted in a LUKS volume inside the live system. The users will be not accessible on the live, but will be restored with krill during installation.

```sudo eggs produce --fast --backup```

### More compressed?

```sudo eggs produce --max``` 



## Copy your iso image and boot the son of your system
You can use ventoy, simple USB with balena etcher or similar, iso file with proxmox ve, virtualbox, vmware etc.

# Binaries
It would be very useful to have the binaries for penguins-eggs and calamares freely created and shared by the community from the PKGBUILDs in AUR, if anyone wants to help can contact [me](https://t.me/penguins_eggs).

# Develop and collaborations link
* facebook group: [facebook group](https://www.facebook.com/groups/128861437762355)
* telegram: [telegram penguin's eggs](https://web.telegram.org/z/#-1447280458)
* penguins-eggs [sources](https://github.com/pieroproietti/penguins-eggs)
* penguins-eggs [book](https://penguins-eggs.net/book/)
* penguins-eggs [blog](https://penguins-eggs.net)

