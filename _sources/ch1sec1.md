## Motivations : Pour quoi faire des statistiques ?


Pourquoi s'embêter à apprendre les statistiques ? À quoi peuvent-elles me servir ? Nous allons prendre un exemple, un jeu de pile ou face, et voir le type de questions qui trouvent des réponses en statistiques.



L'on s'apprête à jouer à pile ou face avec une pièce de monnaie. Nous soupçonnons que la pièce n'est pas parfaitement équilibrée, c'est-à-dire que la probabilité $p$ de tomber sur face n'est pas $\frac{1}{2}$. Que nous permettent de faires les méthodes statistiques ?
```{image} figure_trois_piliers.png
:alt: figure_trois_piliers
:width: 400px
:align: center
```


```{admonition} Estimer
:class: seealso, dropdown
On veut _estimer_ la vraie valeur $p$, par exemple pour modifier notre stratégie en conséquent.

On n'aura accès qu'a un certain nombre de réalisations $(x_1,...,x_n)$ de l'expérience "tirer une pièce". 
La stratégie de résolution de cette question consiste à construire, à partir des données (_via_ une fonction), une "estimation" $\hat{\theta}$ de p. Bien sûr, cette estimation ne peut pas dépendre de l'estimande p, mais l'on cherchera à s'assurer que $\hat{\theta} $ soit probablement proche de p.


Un tel problème est dit "_d'estimation ponctuelle_", et consiste à donner une valeur précise.
```

```{admonition} Encadrer
:class: seealso, dropdown
Savoir qu'un estimateur est probablement proche de la vraie valeur est parfois d'intérêt limité. On pourra préférer donner une région de confiance, par exemple un intervalle. Pour la pièce, cela consisterait à donner un bon encadrement de la probabilité de tirer face. Un intervalle de confiance est la construction de deux fonctions des données $\overline{\theta_n}$ et $\underline{\theta_n}$ telles que l'estimande appartiennent à l'intervalle aléatoire $[\underline{\theta_n}(x_1,...,x_n),\overline{\theta_n}(x_1,...,x_n)] = [\underline{\theta_n},\overline{\theta_n}]$ avec forte probabilité. La question devient alors de trouver un équilibre entre la taille de l'intervalle (région) que l'on veut petit(e) pour plus de précisions, et la probabilité que l'estimande appartienne à la région, que l'on souhaite grande. Répondre à ce type de question correspond à trouver une "_région ou intervalle de confiance_". 
```

```{admonition} Tester
:class: seealso, dropdown
Un dernier problème que l'on va chercher à résoudre est celui de _tester_ une hypothèse. Par exemple, comment trouver une règle de décision pour refuser l'hypothèse que votre adversaire triche en sa faveur ($p<\frac{1}{2}$) ? Il s'agit de donner une règle de décision qui permette de minimiser le risque de rejeter à tort l'hypothèse, sans pour autant toujours l'accepter. Cette partie des statistiques est ce que l'on appelle les _tests_.
```





Ces problématiques, différentes en essence, ont des réponses intimement liées, comme nous allons pouvoir le voir dans ce cours.


Certaines questions de statistique ne seront pas traitées ici, comme la question de la _mise à jour de la connaissance et de la prise de décision_ avec des méthodes Bayesiennes, et Minimax. Le lecteur intéressé pourra se laisser tenter par les lectures suivantes :
```{admonition} Méthodes bayésiennes
:class: hint, dropdown
Pour une introduction aux méthodes bayésiennes, voir {cite:ps}`Bayesian-choice`.
:::{figure} frequentists_vs_bayesians.png
---
height: 400px
---
Pourquoi avons nous besoin de la méthode bayesienne 

(crédit https://xkcd.com/1132/)
:::
```

    
```{admonition} Espérances conditionnelles
:class: hint, dropdown
Pour les bases théoriques à la constructions des espérances conditionnelles, nécessaire à la méthode bayesienne, voir {cite:ps}`Analysis&Probability`.
```

```{admonition} Statistiques bayésiennes non paramétriques
:class: hint, dropdown
Pour un développement des méthodes Bayésienne pour des statistiques non paramétriques, et une étude de leurs performances, voir {cite:ps}`ghosal_vandervaart_2017`.
```


