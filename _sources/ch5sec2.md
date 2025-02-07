
## Test du $\chi^2$ : test d'homogénéité et tests d'indépendance

$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

### Test d'égalité de loi (dit _d'homogénéité_)

On considère $(x_1,...,x_n)$ et $(y_1,...,y_n)$ deux échantillons d'observation, et l'on se demande si ces échantillons ont été tirés avec la même loi. L'on cherche donc à tester

$$H_0 : F_X=F_Y \qquad \text{ contre } \qquad H_1 : F_X\neq F_Y.$$

Notons alors, pour $C_1,...,C_l$ des classes d'une partition de $\R$, les valeurs 

$$\forall k \in \{1,...,l\} \quad p_{k,X}=\mathbb{P}(X\in C_k) \qquad \text{ et } \qquad p_{k,Y}=\mathbb{P}(Y\in C_k).$$
$$\qquad n_{k,x}=Card(x_i \in C_k) \qquad \text{ et } \qquad n_{k,y}=Card(x_i \in C_k).$$

Sous l'hypothèse nulle $H_0$, $p_{k,X}=p_{k,Y}:= p_k$, on peut alors montrer que l'estimateur du maximum de vraisemblance sera :

$$\hat{p_k} = \frac{n_{k,x}+n_{k,y}}{2n}$$

Nous pouvons alors considérer le test du $\chi^2$ avec $2l$ classes  et $l$ paramètres estimés :

::::{prf:proposition}
:class: dropdown
On pose 

$$T_n=\sum_{k=1}^l\frac{(n_{k,x}-n_{k,y})^2}{n_{k,x}+n_{k,y}}$$

Si l'on se donne $\alpha$ un risque de première espèce, et $s_\alpha$ le quantile d'ordre $1-\alpha$ d'une loi du $\chi^2_{l-1}$, 

Alors le test 

$$\text{On rejette }H_0 \text{ si }\ T>s_\alpha \qquad  \text{On ne rejette pas }H_0 \text{ si }\ T\leq s_\alpha$$

est un test de niveau asymptotique $\alpha$.
```{prf:proof} 
Pour montrer cela, il suffit de montrer que $T_n \overset{Loi}{\to} \chi^2_{l-1}$.


Mais ceci est immédiat, puisque 

$$\sum_{k=1}^l\frac{(n_{k,x}-n_{k,y})^2}{n_{k,x}+n_{k,y}}= \sum_{k=1}^l \frac{(n_{k,x}-n\frac{n_{k,x}+n_{k,y}}{2n})^2}{n\frac{n_{k,x}+n_{k,y}}{2n}} +\sum_{k=1}^l \frac{(n_{k,y}-n\frac{n_{k,x}+n_{k,y}}{2n})^2}{n\frac{n_{k,x}+n_{k,y}}{2n}}  $$

qui est exactement la statistique de test du $\chi^2$ avec $2l$ classes (observation de x ou de y et classe d'appartenance) et $l$ paramètre estimé (probabilité des diverses classes).
```
    
### Test d'indépendance 

On considère $(x_1,...,x_n)$ et $(y_1,...,y_n)$ deux échantillons d'observation (regroupé en classes si nécessaire), et l'on se demande si ces échantillons ont été tirés avec des lois indépendantes. 
L'on cherche à tester

$$H_0 : F_X \text{ et }F_Y \text{ sont indépendants }\qquad \text{ contre } \qquad H_1 : F_X \text{ et }F_Y \text{ ne sont pas indépendants}.$$

On note $\Omega_1$ (de cardinal $l_1$) l'ensemble des classes pour $X$  et $\Omega_2$ (de cardinale $l_2$) l'ensemble des classes pour $Y$. Notons aussi $C_{1,x},...,C_{l_1,x},C_{1,y},...,C_{l_2,y}$ les classes respectives des deux échantillons. Alors pour toute paire d'indice $(i,k)$, on pose 

$$p_{i,k}=\mathbb{P}(X\in C_{i,x}, Y \in C_{k,y})\quad p_{i,\cdot}=\mathbb{P}(X\in C_{i,x}) \quad p_{\cdot,k}=\mathbb{P}(Y \in C_{k,y}),$$
$$n_{i,k}=Card((x_m,y_n)\in C_{i,x}\times C_{k,y}) \quad n_{i,\cdot}=Card(x_m\in C_{i,x}) = \sum_{k=1}^{l_2} n_{i,k}\quad n_{i,\cdot}=Card(x_m\in C_{i,x}) = \sum_{i=1}^{l_1} n_{i,k}.$$


::::{prf:proposition}
On pose 

$$T_n=\sum_{i=1}^{l_1}\sum_{k=1}^{l_2}\frac{(n_{i,k}-\frac{n_{i,\cdot}n_{\cdot,k}}{N})^2}{\frac{n_{i,\cdot}n_{\cdot,k}}{N}}$$

Si l'on se donne $\alpha$ un risque de première espèce, et $s_\alpha$ le quantile d'ordre $1-\alpha$ d'une loi du $\chi^2_{(l_1-1)\times(l_2-1)}$, 

Alors le test 

$$\text{On rejette }H_0 \text{ si }\ T>s_\alpha \qquad  \text{On ne rejette pas }H_0 \text{ si }\ T\leq s_\alpha$$

est un test de niveau asymptotique $\alpha$.

```{prf:remark}
:class: dropdown
L'hypothèse d'indépendance peut se réécrire comme le fait que la loi jointe est le produit des lois marginales. Il faut donc trouver les lois marginales avec un estimateur du maximum de vraisemblance, et il y aura $(l_1-1)$ et $(l_2-1)$ possibilité respectivement pour chaque loi marginales, soit $l_1+l_2-2$ paramètres à déterminer.

_Remarquons que sur $\Omega_1\times \Omega_2$ il y a $l_1\times l_2 -1$ lois possibles._

Sous l'hypothèse nulle $H_0$, $p_{i,\cdot}\cdot p_{\cdot,k}=p_{i,k}$ et l'on peut alors montrer que l'estimateur du maximum de vraisemblance sera bien les valeurs :

$$\hat{p_{i,k}} = \frac{n_{i,\cdot}}{n} \times \frac{n_{\cdot,k}}{n} $$

Ceci justifie l'utilisation du test du $\chi^2$ avec $l_1\times l_2 -1$ classes  et $l_1+l_2-2$ paramètres estimés.

```

```{prf:proof}
Pour montrer cela, il suffit de montrer que $T_n \overset{Loi}{\to} \chi^2_{(l_1-1)\times(l_2-1)}$.

Mais ceci est immédiat, puisque la statistique $T_n$ est exactement la statistique de test du $\chi^2$ avec $l_1\times l_2 -1 $ classes et $l_1+l_2-2$ paramètres estimés (probabilités des diverses classes pour les marginales). Soit bien un total de $l_1\times l_2 -1 -(l_1+l_2-2)= (l_1-1)\times(l_2-1)$ degré de liberté.
```

::::

:::{prf:remark}

Attention à ne pas trop utiliser ce test, qui n'est performant que pour des échantillons de grande taille
:::






