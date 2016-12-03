---
layout: post
title:  "Commander un moteur brushless via une Pi"
description: "Pi-Blaster, une lib pour gérer vos servos, et bien d'autres !"
tags: [linux, electronique]
---

# Pi-blaster

[Pi-Blaster][pi_blaster] est un projet que j'ai trouvé sur github permettant de generer un signal PWM asses personnalisable pour les GPIO de votre pi ou pi2.
Cela vous permet donc de jouer avec des servos, ou encore des ESC (pour contrôler des moteurs Brushless).

# Les ESCs

Ici je veux utiliser un ESC flashé avec [BlHeli14][blheli_github].
Le but est d'avoir un moteur brushless qui tourne dans les deux sens et BlHeli propose cette fonctionnalité.

q# Une histoire bi-directionelle

Mon esc est en mode bi-directionnel, c'est à dire que la position middle correspond en fait au moteur éteins. Si je passe au min, il tournera à fond dans un sens, et au max à fond dans l'autre sens.

## Comment passer l'ESC en mode bi-directionnel

* Il faut aller télécharger la suite BlHeli [ici][blheli_suite]
* Une fois que c'est fait, décompressez et lancez le soft.
* Branchez l'esc _(ici un DYS 30A opto)_ avec l'USB LINKER (ici celui de DYS)
* Alimentez l'ESC
* Selectionnez [le port `COM`][0_port] adéquate
* Selectionnez dans [le menu `Interface`][1_interface] la bonne interface, ici: `4: ATMEL SK  Bootloader (ArduinoUSBLinker)`
* Cliquez sur `connect` en bas à coté du port `COM`
* Flashez l'ESC avec la [dernière version de BlHeli][2_flash]
* Passez l'ESC en mode bidirectional en glissant [le curseur][3_bidir] à droite
* Ecrivez l'ESC avec les bons paramètre via [le bouton][4_write] `Write Setup`
* Cliquez ensuite sur le bouton `Disconnect`
* Vous n'avez plus qu'a débrancher tout ca. C'est fini.

# Fonctionnement de Pi-Blaster

## L'installer

La procédure d'installation est détaillée dans le readme.md du repos, mais pour les non anglophones, procédez ainsi:

* Installez `autoconf`
  * Debian like: `apt-get install autoconf`
  * Archlinux like: `pacman -Sy autoconf`
  * Fedora like: `zypper install autoconf` _(Je n'ai pas test sur ce type de distro)_

* Ensuite, c'est simple, clonez le repo et déplacez-vous:
{% highlight bash %}
git clone https://github.com/sarfata/pi-blaster.git && cd pi-blaster
{% endhighlight %}
* Puis buildez simplement:

{% highlight bash %}
./autogen.sh
./configure
make
sudo make install
{% endhighlight %}

* Pour demarrer Pi-Blaster de façon manuelle: `sudo ./pi-blaster`

* Pour déinstaller Pi-Blaster: `sudo make uninstall`

## Comment l'utiliser

Pi-Blaster créé une fichier spécial `/dev/pi-blaster` de type FIFO (First In First Out). Pas besoin des droits root pour écrire dans ce fichier. Tout utilisateur à les droits donc vous pouvez faire tourner n'importe quelle appli sur votre pi, elle pourra gérer vos GPIO.

__Important: Quand vous utilisez Pi-Blaster les GPIO que vous utilisez sont définies en tant que sorties.__

Pour faire tourner notre moteur qui est par exemple sur le GPIO 4, il faut faire: `echo "4=0.21" > /dev/pi-blaster`
Le principe général est d'écrire dans `/dev/pi-blaster` avec la forme suivante: `<numero_GPIO>=<valeur>` ou `<valeur>` doit être compris entre 0 et 1 inclus.

# Pi-Blaster et BlHeli

Maintenant que notre ESC est à jour et que l'on a Pi-Blaster sur notre pi, il va falloir les utiliser.

Après quelques essais à tâtons, j'ai remarqué les valeurs suivantes:

| Valeur || vitesse moteur || sens rotation |
|:------:||:--------------:||:-------------:|
| 0.080  ||      max       ||  anti-horaire |
| 0.148  ||      nul       ||    	N/A 	|
| 0.210  ||      max       ||    horaire    |

# La suite

La puissance de Pi-Balster réside dans le fait qu'il est modulaire. L'idée est d'arriver à parametrer comme il faut la lib pour pouvoir faire tourner le moteur de 0.000 à 1.000 en adaptant la fréquence PWM et la taille de la trame.



[0_port]:			{{ site.url }}/assets/0.blheli_port.png
[1_interface]:		{{ site.url }}/assets/1.blheli_interface.png
[2_flash]:			{{ site.url }}/assets/2.flash_last_version.png
[3_bidir]:			{{ site.url }}/assets/3.bi_directional.png
[4_write]:			{{ site.url }}/assets/4.write_setup.png
[blheli_suite]:		https://blhelisuite.wordpress.com/
[pi_blaster]:		https://github.com/sarfata/pi-blaster
[blheli_github]:	https://github.com/bitdump/BLHeli
