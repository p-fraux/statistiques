## Les expériences statistiques et les statistiques

$\newcommand{\R}{\mathbb{R}}$


Cette page donne un cadre formel aux statistiques, et peut être omise en première lecture.

Partons de l'exemple de la piece truquée. Nous disposons d'un espace probabilisable $(\Omega, \mathcal{T})$, c'est-à-dire un univers (les résultats possibles des $n$ lancer de pièces, donc $\Omega=\{0,1\}^n$) et d'une tribu (l'ensemble de tous les événements descriptibles, donc ici $\mathcal{T}=\mathcal{P}(\Omega)$).


Sur cette espace, l'on considère une _famille de loi $\mathcal{P}$_, où chaque loi est susceptible de régir le phénomène (ici toutes les lois de variables aléatoires issues de la répétition indépendante d'une expérience de Bernoulli).

On peut alors choisir pour cette famille de loi une _paramétrisation_, qui joue le rôle d'un système de coordonné des lois. C'est-à-dire qu'il s'agit avant tout d'un choix de convenance, qui aide à la description. Une _paramétrisation_ est la donnée d'un ensemble $\Theta$, que l'on demande souvent inclus dans $\R^n$, et  d'une application surjective de $\Theta$ dans la famille des lois $\mathcal{P}$.

Il est alors intéressant de demander qu'il n'y ai pas de redondance dans cette paramétrisation (avec le lancer de pièce, on pourrait choisir comme paramétrisation la probabilité de tirer face avec la pièce, et $\Theta=[0,1]$). Cette hypothèse est surtout une hypothèse de convenance, et n'est absolument pas nécessaire, comme l'on pourrait le voir dans la théorie du mélange (voir par exemple l'introduction <a href="https://snunnari.github.io/SBE/mclachlan.pdf">https://snunnari.github.io/SBE/mclachlan.pdf</a> ou le livre {cite}`mclachlan2019finite`, ) qui dépasse largement le propos de ce cours. 


Maintenant, il est naturel que le statisticien n'ai pas accès à tout l'univers, mais seulement à une partie des données. Tout ceci motive la définition suivante, inspiré des variables aléatoires :
```{prf:definition} Expérience statistique
:label: Expstat
:class: dropdown
On appelle _expérience statistique_ la donnée de 

$$\left(\Omega, \mathcal{T}, \Theta, (\mathbb{P}_\theta)_{\theta \in \Theta} , \mathcal{X}, \mathcal{G}, X\right)$$

où $(\Omega, \mathcal{T})$ est un espace probabilisable, $\mathcal{P}=(\mathbb{P}_\theta)_{\theta \in \Theta}$ est une famille de probabilité sur $\Omega$, $\Theta$ en est une paramétrisation, $\mathcal{X}$ un espace d'observation et $\mathcal{G}$ une tribu sur cet espace. Enfin, $X$ est une variable aléatoire (c'est-à-dire une application mesurable de $(\Omega, \mathcal{T})$ dans $(\mathcal{X}, \mathcal{G})$) modélisant une observation.
:::{prf:remark}
:label: expstatrq
Bien souvent, on se contentera de donner la famille de loi $\mathcal{P}$, le reste étant implicite.
:::
Si les expériences sont construites à partir de répétition indépendante d'une expérience de base, on parlera _d'expérience produit_. Dans ce cas, l'univers doit être une puissance de l'espace de base ($\Omega^n$), et les tribus, lois, et observation doivent être des tribus et lois produits ($\mathcal{T}= \sigma(\times_{i=1}^n \mathcal{T}_0)$, $\mathcal{P}=(\mathbb{P}_n= \mathbb{P}^{\otimes n})$, $\mathcal{X}= {\mathcal{X}_0}^n$).

:::{prf:remark}
:label: identifiable
On dira qu'une paramétrisation est _identifiable_ si l'application qui associe un paramètre à une loie est injective
:::
On notera les concepts probabilistes d'intérêt sous la loi $\mathbb{P}_\theta$ avec un $\theta$ en indice. Par exemple $\mathbb{E}_\theta$ est l'espérance et $V_\theta$ la variance suivant $\mathbb{P}_\theta$.



```





Le statisticien cherche bien souvent à extraire un maximum d'information de ses données, c'est pourquoi il se permet le panel large d'outils le plus large qui puisse avoir un sens physique pour étudier les obsérvations :


```{prf:definition} Statistiques
:label: Statdef
:class: dropdown
On appelle _Statistique_ toute application mesurable depuis l'espace des observations.
```

```{prf:example} 
:label: Statdef
:class: dropdown
La moyenne empirique $\overline{X}=\frac{1}{n}\sum_{i=1}^nX_i.$, la variance empirique $\frac{1}{n-1}\sum_{i=1}^n \left(X_i-\overline{X}\right)^2.$ et la fonction de répartition empirique $F_n : t\mapsto \frac{Card\{k\in [\![1,n]\!], x_k \leq t\}}{n} = \frac{1}{n} \sum_{k=1}^n 1_{]-\infty,t]}(x_k).$ sont trois exemples de statistiques.

```

Dans toute les autres pages de ce site, on fixe $(\Omega, \mathcal{T}, \Theta, (\mathbb{P}_\theta)_{\theta \in \Theta} , \mathcal{X}, \mathcal{G}, X)$ une expérience statistique.