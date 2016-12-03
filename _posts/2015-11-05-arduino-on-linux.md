---
layout: post
title: Arduino sur linux
tags: [linux, electronique]
---

# Arduino sur linux

Pour résoudre les problèmes liés au compilateur arduino sous linux.

{% highlight bash %}
cd /usr/share/arduino/hardware/tools/avr/bin
mv ./avr-gcc ./avr-gcc-backup
ln -s /usr/bin/avr-gcc ./
{% endhighlight %}

Et pensez à `chmod 666` le `/dev/ttyX` quand vous plugez une carte arduino si vous n'etes pas dans le groupe `dialout`
Sinon ajoutez-vous tout simplement dans le groupe `dialout` comme suit:

{% highlight bash %}
sudo usermod -a -G dialout <votre_user>
{% endhighlight %}
