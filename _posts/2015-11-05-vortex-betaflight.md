---
layout: post
title:  Betaflight et le Vortex d'immersionRC
tags: [multirotor]

---

# Comment installer betaflight sur le Vortex d'immersionRC.

Voilà un petit guide que j'ai traduit de jojo Polinga sur le groupe anglophone des processeurs de vortex.
Donc voici un guide rapide pour ceux qui veulent essayer le logiciel betaflight de Boris B sur leurs Vortex.
J'ai pu suivre le développement de son travail depuis le tout début jusqu'à la version finale qui fonctionne bien sur mes autres quad, et maintenant sur mon Vortex aussi. __VOUS POUVEZ REVENIR EN ARRIERE A TOUT MOMENT__

ATTENTION: Je ne pourrais être tenu pour responsable en cas de problèmes causé à votre Vortex. Ceci n'est qu'un guide et vos problèmes ne sont pas de ma responsabilité.

## Etape 1: Télécharger les outils ImmersionRC 1.41.7

https://www.dropbox.com/sh/9fosn0s7ntbig6q/AABDmnpAX-rVcDuM20pKdJnja/ImmersionRCToolsSetup_v1.41.7.zip?dl=0
Cet outil est nécessaire car la dernière version (1.42.2) ne nous permet pas de mettre à jour l'OSD depuis que je l'ai passé en 1.0.15. Mais beaucoup d'utilisateurs ont pu mettre à jour leurs OSD avec cette vielle version.

## Etape 2: Télécharger et flasher l'OSD en version beta 1.0.16 avec la vielle version de l'outil d'immersionRC (1.41.7) téléchargé à l'étape 1.

http://www.immersionrc.com/?download=4554
Ce firmware d'OSD permettra une bonne communication entre betaflight et l'OSD. (note du traducteur: j'ai essayé la dernière version stable de l'OSD et elle ne peut pas communiquer avec betaflight mais le reste fonctionne correctement) Si vous essayez une ancienne version de l'OSD vous aurez "API error" quand vous entrerez dans le menu des PID ou des protune.

## Etape 3:

Téléchargez le fameux hex de Boris B. Nous prendrons la version pour Naze.
https://github.com/borisbstyle/cleanflight/blob/betaflight/obj/betaflight_NAZE.hex
- Vous allez voir beaucoup de code. Faites clic droit sur le bouton "RAW" a droite, et "sauvegardez le lien comme" ("Save link as...") et sauvegardez le sur votre bureau.

## Etape 4: Flashez votre Vortex avec le Naze.hex que vous avez enregistré sur votre bureau.

Pour ce faire: ouvrez cleanflight et utilisez l'onglet "load firmware (local)" et clickez sur naze.hex que vous avez téléchargé sur votre bureau depuis le github de Boris B.
Rappelez vous: __TOUJOURS CLICKER SUR SAVE POUR CHAQUE ETAPE DANS CLEANFLIGHT__

1. Dans l'onglet de configuration: clickez sur RX_PPM. et clickez sur "motor_stop" si vous utilisez ca, et cochez OneShot125 si besoin. Enregistrez.

2. Dans l'onglet "modes" configurez vos inter pour armer le multi si vous utilisez ca, et sauvegardez.

3. Vérifiez vos voix qu'elles soient de 1000 à 2000 et ajustez votre radio en fonction.

4. Dans l'onglet "receiver" vérifiez le mappage de vos voix radio, et si vous utilisez une taranis, cliquez sur JR/Graupner dans le menu déroulant. Cela va mapper en TAER1234.

5. Onglet "PID tuning", changez le PID controller à 1-multiwii (rewrite) pour le profile 1. et 2- luxfloat pour le profile 2. Ici est le point fort de betaflight. Les valeurs par défaut sont juste impressionnante ! vous pourrez utiliser le profile 3 pour vos propres pro-tunes. Vous devrez sauvegarder avant pour que cela charge les PID par défaut. __RAPPELEZ VOUS QUE POUR CHAQUE PROFILE PID CONTROLLER VOUS DEVREZ MODIFIER L'ONGLET DE MODE__ Toujours cliquer sur le bouton de sauvegarde pour chaque onglet sinon vous perdrez vos réglages.

6. Si vous voulez que votre baro fonctionne, allez dans l'onglet CLI et entrez "set baro_harware = 0" puis "save". Cela va redémarrer le vortex puis cliquez sur n'importe quel onglet.

7. Dans l'onglet des PID ajustez vos rates. C'est selon vous, et votre style de vol.

Cela résume ce que j'ai fait. J'espère que ca vous aura aidé !
