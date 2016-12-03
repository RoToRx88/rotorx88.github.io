---
layout: post
title:  "Les PID"
description: "Les PID et les multirotors"
tags: [algorithmie, multirotor]
---

# Les PID

Les PID... 3 lettres qui font peurs à tous les débutants... ou non débutants d'ailleurs !

Dans cet article je vais tenter de vous expliquer comment fonctionnent ces derniers et comment les régler dans le cas de vos multirotors.

# Introduction, pourquoi les PID

> Un régulateur PID ou correcteur PID (pour « proportionnel intégral dérivé ») est un organe de contrôle permettant d’effectuer une régulation en boucle fermée d’une grandeur physique d'un système industriel ou « procédé » (voir Automatique). C’est le régulateur le plus utilisé dans l’industrie, et il permet de régler un grand nombre de grandeurs physiques.

*source: [Wikipedia][1]*

Pour qu'un multirotor vol, il faut qu'il ait au moins 3 points d’appuis dans l'air (ou deux pour les bi-rotors, mais ce sont des cas particuliers). Prenons l'exemple d'un quadricoptère, qui à donc 4 moteurs. En vol stationnaire notre quadri aura donc ces 4 moteurs qui tourneront exactement à la même vitesse si l'ont veut qu'il soit stable. Mais ca, s'est valide uniquement si nous somme dans un environnement sans perturbations. Or sa n'existe pas. Notre quadri donc en permanence influencé par des courants et autres perturbations. Aussi, il faut donc corriger ses perturbations sans quoi il ne tiendra pas bien longtemps en l'air.

Sa tombe bien, car un outil répond exactement à notre besoin, c'est la boucle PID. Les PID sont un outil mathématique permettant de stabiliser un système. Vous les retrouvez de partout autour de vous. En effet, votre four utilise les PID pour tenir la bonne température afin de faire cuire votre pizza comme il faut, ou encore le thermostat de votre chauffage, et enfin les pilotes automatique d'avions de ligne.

# Fonctionnement d'une boucle PID

Le principe de fonctionnement est simple. La boucle PID prend en entrée deux valeurs:

*   La position que vous désirez, appelée la consigne (celle que vous donnez aux manches, par exemple: Je veux que mon quadri soit à plat)
*   La position réel dans l'espace (cette valeur vient des capteurs qu'il y a dans votre carte de vol)

Une erreur va ensuite être calculée à partir de ces deux valeurs. Si l'erreur est nul on saura alors que notre quadri est bien à plat et à ce moment la il n'y à rien à faire à part attendre qu'une erreur arrive. Dès qu'une erreur sera calculée, une correction devra être appliquée car cela signifie que notre quadri n'est pas dans la position désirée (à cause d'un coup de vent par exemple). Une fois que nous avons notre erreur (une valeur non nul), il faut calculer la force à appliquer pour ramener notre quadri dans la position voulue (dans notre cas on veux le garder à plat). Evidemment cette force doit être proportionnelle à l'erreur. Si notre quadri ne dévie que de 2 ou 3 degrés, on n'appliquera pas la même force que si il dérive de 40 degrés (oula, grosse bourrasque de vent la quand même). Afin de calculer la commande (force que l'on va appliquer), on va se servir de l'erreur calculée en la multipliant au facteur Kp (notre P), en l'intégrant par le facteur Ki (notre I) et enfin en la dérivant par le facteur Kd (notre D). Une fois ces trois valeurs calculées, on les sommes pour obtenir la commande finale que l'on va envoyer au quadri pour le remettre à plat.

# Utilité des valeurs P, I, D

Nous allons maintenant voir comment régler les valeurs Kp, Ki, Kd qui sont des constantes à régler afin d'avoir notre multi le plus stable possible.

## La valeur P

Cette valeur représente la force avec laquelle on va corriger l'erreur. Si notre quadri penche alors qu'on le voulait à plat, doit-on corriger avec une vitesse de rotation de 2°/sec, ou de 40°/sec ? C'est en faisant varier P qu'on va définir cela. Plus le P est haut, plus la correction sera rapide.

### Les effets de P

*   Un P trop haut aura tendance à faire sur-compenser votre quadri. Ainsi au lieu de le remettre à plat, on va dépasser la consigne et pencher de l'autre coté.
*   Un P trop bas aura l'effet inverse. Le multi va mettre trop de temps à atteindre la consigne.

## La valeur I

La valeur I permet de corriger une erreur dans le temps. Mettons que notre P soit réglé comme il faut, si il y a toujours un peu de vent, même a plat, notre quadri aura tendance à glisser dans l'air au lieu de rester vertical d'un point fixe. C'est la que I interviens, il corrige la déviation lente liée au vent.

## La valeur D

Le D permet de donner une réponde d'autant plus grande que la rapidité avec laquelle grandit l'erreur dans le temps.

# Réglage des PID

Il faut régler les PID en mode acro/rate dans un premier temps afin d'avoir une machine stable, puis régler les PID du mode angle si vous voulez utiliser ce mode.

## Réglage de P

Tout d'abord diminuez la valeur de I significativement. Puis faites monter la valeur de P progressivement jusqu'à obtenir des vibrations du quadri en l'air. Une fois ces vibrations atteintes, il suffit de diminuer la valeur jusqu'à ce qu'elles disparaissent.

## Réglage de I

Il n'y a pas de méthode miracle pour régler le I. Cela se fait selon votre ressenti. Cependant, il existe une méthode qui consiste à mettre du lest à l’extrémité d'un des bras du quadri, et à monter le I jusqu'à ce qu'il ne glisse presque plus en l'air et qu'il corrige automatiquement le fait que son centre de gravité soit dévié par le lest.

## Réglage de D

Cela dépend de votre ressenti. Si vous voulez un quadri nerveux, augmentez D, si vous voulez adoucir les réactions du quadri, diminuez D.

# Conclusion

Je me suis inspiré de beaucoup de sites et vidéos parlant des PID afin d'essayer de les rendre le plus simple à comprendre. J'ai même créé une [page][2] sur github regroupant toutes les doc que j'ai pu trouver. Si vous avez quelque remarque que ce soit faites le moi savoir j'adapterai l'article et essayerais de vous aider. Vous avez toutes les clefs en main pour bien régler votre multi alors foncez, et bon vol !

 [1]: https://fr.wikipedia.org/wiki/R%C3%A9gulateur_PID
 [2]: https://github.com/RoToRx88/pid_explanation/blob/master/README.md
