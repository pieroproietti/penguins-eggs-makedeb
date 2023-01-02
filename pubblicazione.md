# Pubblicazione in AUR

penguins-eggs è pubblicato su [AUR](https://aur.archlinux.org/packages/penguins-eggs) alla pagina:

```
https://aur.archlinux.org/packages/penguins-eggs
```

E' presente un link in sola lettura:

```
git clone https://aur.archlinux.org/penguins-eggs.git
```

ed uno per lettura e scrittura:

```
git clone ssh://aur@aur.archlinux.org/penguins-eggs.git
```

Per clonare il repository in lettura e scrittura, è necessario essere in possesso della chiave.



# Aggiornamento
Per aggiornare, con un utente in possesso della chiave privata:

```git clone ssh://aur@aur.archlinux.org/penguins-eggs.git```

## .SRCINFO
Prima di poter pubblicare occorre ri-creare il file .SRCINFO con il comando:

```makepkg --printsrcinfo > .SRCINFO```

 