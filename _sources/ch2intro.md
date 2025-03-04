# <i class="fas fa-book fa-fw"></i> Estimateur : exemple de l'Estimateur de Maximum de Vraisemblance

Dans ce chapitre, nous allons introduire la notion d'estimateur, ainsi que les propriétés générales que l'on peut attendre d'un bon estimateur.

Afin d'évaluer la performance d'un estimateur, nous devrons choisir un coût pour l'écart entre la _vrai_ valeur que l'on cherche à estimer et ce que l'on estime. Il y a de nombreux choix possibles de tels coûts. Le plus simple à calculer, manipuler et  le plus répandu est le coût en moyenne quadratique que nous utiliserons dans ce cours.

````{card-carousel} 3
```{card} 
:link: ch2sec1
:link-type: doc
:text-align: center 
:shadow: md 
:class-header: bg-light

<i class="fas fa-book fa-fw"></i> **Estimateur et premiers critères**
^^^

On donne deux critères essentiels que doivent vérifier des estimateurs. 
```
```{card} 
:link: ch2sec2
:link-type: doc
:text-align: center 
:shadow: md 
:class-header: bg-light

<i class="fas fa-book fa-fw"></i> **Efficacité d’un estimateur**
^^^
On étudie la variance d'un estimateur à l'aide du theoreme de Cramer et Rao. On définit alors l'éfficacité d'un estimateur.
```
```{card} 
:link: ch2sec3
:link-type: doc
:text-align: center 
:shadow: md 
:class-header: bg-light

<i class="fas fa-book fa-fw"></i> **Estimateur de Maximum de Vraisemblance**
^^^
On donne la méthode pour déterminer une classe d'estimateur souvent de bonnes qualitées.
```
```{card} 
:link: ch2sec4
:link-type: doc
:text-align: center 
:shadow: md 
:class-header: bg-light

<i class="fas fa-book fa-fw"></i> **Amélioration théorique d’estimateurs (HP)**
^^^
On discute de comment améliorer des estimateurs. Les résultats de cette page sont hors programme pour une première année à l'ENSEEIHT.
```

````


Parmi les autres, l'on pourra citer les coûts $L^p$. Plus adapté aux tests et à l'estimation non paramétrique, on peut également citer la distance en variation, l'entropie relative et la distance de Hellinger entre la loi de la statistique et la loi théorique. On pourra ainsi s'intéresser à :

```{admonition} Théorie de l'information
:class: hint, dropdown
pour les définitions des mesures d'informations, distance en variation et entropie relatives, et leurs propriétés, voir {cite:ps}`Information-Theory`.
```

    
```{admonition} Distance de Hellinger
:class: hint, dropdown
Pour l'utilisation de la distance de Hellinger en analyse paramétrique,, voir {cite:ps}`vaart_1998`.
```

```{admonition} Statistiques bayésiennes non paramétriques
:class: hint, dropdown
Pour l'utilisation de boules pour la distance de Hellinger en estimation robuste, voir {cite:ps}`Birg2013RobustTF`.
```


 