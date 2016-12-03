---
layout: post
title: Scaler une valeur
tags: [algorithmie, dev]

---

Juste ici un petit snippet pour passer d'une échelle à l'autre une valeur comme peut le faire la fonction `map` en Arduino.


{% highlight python %}
NewValue = (((OldValue - OldMin) * (NewMax - NewMin)) / (OldMax - OldMin)) + NewMin
{% endhighlight %}


Ou en plus lisible:

{% highlight python %}
OldRange = (OldMax - OldMin)  
NewRange = (NewMax - NewMin)  
NewValue = (((OldValue - OldMin) * NewRange) / OldRange) + NewMin
{% endhighlight %}

Et si vous voulez protéger votre code dans le cas ou l'ancien range est de 0:

{% highlight python %}
OldRange = (OldMax - OldMin)
if (OldRange == 0)
    NewValue = NewMin
else
{
    NewRange = (NewMax - NewMin)  
    NewValue = (((OldValue - OldMin) * NewRange) / OldRange) + NewMin
}
{% endhighlight %}
