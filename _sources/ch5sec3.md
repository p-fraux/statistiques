
## Tester la loi d'observations
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

### Test d'adéquation à une loi de Kolmogorov

Pour de petits nombres d'observation et pour des lois $F_0$ continues, l'on pourra préférer utiliser le test de Kolmogorov, qui utilise toute l'information des observations à l'exception de l'ordre dans lesquelles elles ont été obtenues. Pour cela, ce test utilise la fonction de répartition empirique (voir {ref}`Statistiques_usuelles`).

$$\hat{F_n} : t\mapsto \frac{Card\{k\in [\![1,n]\!], X_k \leq t\}}{n} = \frac{1}{n} \sum_{k=1}^n 1_{]-\infty,t]}(X_k).$$

```{exercise}
:class: dropdown
:label: exer19

Soit $(X_i)$ une suite de variables aléatoires indépendante et de même loi que la variable $X$. L'on note $F : t\mapsto \mathbb{P}(X\leq t)$ la fonction de répartition de la loi et $\hat{F_n}$ la fonction de répartition empirique de l'échantillon.

Montrer que la loi de la variable 

$$\sup\limits_{t\in \R}|\hat{F_n}(t)-F(t)|$$

ne dépend pas de la loi de $X$ lorsque F est continu.

_L'on pourra se servir de l'inverse généralisé de la fonction de répartition_

    
:::{admonition} Solution 
:class: dropdown
 Nous allons suivre l'indication. Notons $F^{\leftarrow}$ l'inverse généralisé de la fonction de répartition F.
 
Rappelons que $U$ une variable suivant une loi uniforme sur $[0,1]$, $ F^{\leftarrow}\circ U$ à la même loi que X (voir {ref}`inverse-generalise`). Nous pouvons donc, sans perte de généralité sur les lois, supposer qu'il existe $(U_i)$ une suite de variables aléatoires indépendante et suivant une loi uniforme sur $[0,1]$ telle que $X_k=F^{\leftarrow}\circ U_i$.

Or 

$$F_n(t)=\frac{Card\{k\in [\![1,n]\!], X_k \leq t\}}{n}$$
$$=\frac{Card\{k\in [\![1,n]\!], U_i \leq F^{\leftarrow}(t)\}}{n}$$

et
    
$$ F(t)= \mathbb{P}(X\leq t)= \mathbb{P}(U\leq F^{\leftarrow}(t)).$$

Ce qui nous donne, en posant $s=F(t)$, que 

$$\sup\limits_{t\in \R}|\hat{F_n}(t)-F(t)|=\sup\limits_{s\in F(\R)}|\hat{F_{n,U}}(s)-s|= \sup\limits_{s\in ]0,1[}|\hat{F_{n,U}}(s)-s|.$$

Car si F est continue, 
    $F(\R) = ]0,1[$ et donc la loi de la variable aléatoire 
    $\sup\limits_{t\in \R}|\hat{F_n}(t)-F(t)|$ ne dépend pas de la loi de X (puisqu'elle est égale en loi à une variable aléatoire ne dépendant que de la loi uniforme).
:::



```

Au vu de l'exercice, posons la statistique 

$$D_n=\sup\limits_{t\in \R} |\hat{F_n}(t)-F(t)|$$


::::{prf:proposition}
La statistique $D_n$ vérifie que pour tout $\mu>0$,

$$ \mathbb{P}(D_n>\mu) \sim 2\sum_{k=0}^\infty (-1)^{k-1} \exp{(-2k^2\mu^2n)}  $$

Comme la loi de $D_n$ peut-être tabulé, nous pouvons alors construire un test d'ajustement (l'hypothèse nulle est $H_0 : F_X=F$) à partir des quantiles d’ordre $1-\alpha$ de la distribution de $D_n$ noté $s_\alpha(n)$. On prend comme règle de décision

$$\left\{\begin{matrix}
    \text{Si } d_n(x_1,...,x_n) > s_\alpha(n) & \text {On rejette }H_0\\
    \text{Si } d_n(x_1,...,x_n) \leq s_\alpha(n) & \text {On ne peut pas rejetter }H_0.
\end{matrix}\right.$$

```{prf:remark}
Plutôt que de chercher dans les tables, il est possible lors de la recherche de $s_\alpha(n)$, quantile d’ordre $1-\alpha$ de la distribution de $D_n$, d'utiliser que pour $n>80$, $s_{0.05}(n)\sim \frac{1.3581}{\sqrt{n}}$ et $s_{0.01}(n) \sim \frac{1.6276}{\sqrt{n}}$.
```
::::

:::{admonition} Méthode pour simplifier le calcul 
:class: tip
Pour calculer la statistique $d_n$, il suffit de remarquer que $F$ est croissant et que $\hat{F_n}$ ne change qu'en les points $x_i$. Ce point va nous permettre de simplifier la recherche du supremum. Notons $(x^*_1,...,x^*_n)$ les observations rangées par ordre croissant (on parle de la statistique de l'ordre), et supposons pour simplifier qu’elles soient toutes distinctes, c’est-à-dire que $\forall i\in \{1,...,n-1\}, x^*_i<x^*_{i+1}$ (ce qui est presque-sûr puisque X est supposé continu). On a alors la réécriture

$$d_n = \sup\limits_{t\in \R} |\hat{F_n}(t)-F(t)| = \sup_{i\in \{1,...,n\}}\left(\max[|\frac{i-1}{n}-F(x^*_i)|,|\frac{i}{n}-F(x^*_i)| ]\right).$$

Dit autrement, il suffit de regarder l'écart au niveau des observations, comme illustré dans la figure {ref}`CalculKolmogorov` :



```{image} Kolmogorov.png
:alt: CalculKolmogorov
:width: 600px
:align: center
:name: CalculKolmogorov
```
:::

    
```{exercise}
:class: dropdown
:label: exer20

Au cours d'une année, les sites de productions d'une entreprise d'électronique de pointe doivent renouveler certains des outils d'usinages nécessaires à la production d'une entreprise. L'hypothèse de modélisation la plus simple est de dire que le nombre d'outils à remplacer dans un site de production suit une loi de Poisson, de paramètre $\lambda$ inconnu. 

Au cours de l'année passée, l'entreprise a compté le nombre d'outils remplacé dans ses divers sites. Les résultats sont présentés dans le tableau suivant :

$$\begin{array}{|c|c|c|c|c|c|c|c|c|c|c|}
        \hline
         \text{Nombre d'outils renouvelés} & 0&1&2&3&4&5&6&7&8&9  \\
         \hline
         \text{Nombre de sites}  & 1&2&2&3&3&5&5&2&3&2\\
         \hline
    \end{array}$$

Nous admettrons que l'estimateur de maximum de vraisemblance pour le paramètre des lois de Poisson est la moyenne empirique.

L'entreprise souhaite vérifier que les données $(x_i)$ sont bien issues d'un échantillon de loi de Poisson de paramètre inconnus.


La documentation Matlab de la fonction POISSCDF décrit "$POISSCDF(X,Lambda)$ compute the Poisson cumulative distribution function with parameter $Lambda$ at the value $X$". L'ordinateur donne les réponses suivantes :

poisscdf([0 1 2 3 4 5 6 7 8 9 10 11], 3) = [0.0498, 0.1991, 0.4232, 0.6472, 0.8153, 0.9161, 0.9665, 0.9881,
       0.9962, 0.9989, 0.9997, 0.9999]
       
poisscdf([0 1 2 3 4 5 6 7 8 9 10 11], 4)=[0.0183, 0.0916, 0.2381, 0.4335, 0.6288, 0.7851, 0.8893, 0.9489,
       0.9786, 0.9919, 0.9972, 0.9991]
       
poisscdf([0 1 2 3 4 5 6 7 8 9 10 11], 5)=[0.0067, 0.0404, 0.1247, 0.265 , 0.4405, 0.616 , 0.7622, 0.8666,
       0.9319, 0.9682, 0.9863, 0.9945]
       
poisscdf([0 1 2 3 4 5 6 7 8 9 10 11], 6)=[0.0025, 0.0174, 0.062 , 0.1512, 0.2851, 0.4457, 0.6063, 0.744 ,
       0.8472, 0.9161, 0.9574, 0.9799]

a) L'entreprise souhaite effectuer un test du $\chi^2$ avec un risque $\alpha=0.05$. Calculez la statistique d'un tel test en répartissant les données dans trois classes judicieusement choisies. Combien de degré de liberté aura-t-on ? En s'aidant de la table {ref}`fig:Chi-Square-table`, donnez la région d'acceptation. Conclure.
    
:::{admonition} Solution a)
:class: dropdown
 On trouve $\hat{\lambda}\approx 5$.

Au vu de la fonction de répartition correspondante, ont choisi les classes : 
            $C_1= \{0,1,2,3\}$, $C_1= \{4,5\}$ et $C_3$ les autres valeurs. En particulier, $\mathbb{P}(Y\in C_1)= 0.256$, $\mathbb{P}(Y\in C_2)= 0.36$ et $\mathbb{P}(Y\in C_3)= 0.384$.
            
L'on compte 8 valeurs dans $C_1$, 8 dans $C_2$ et 12 dans $C_3$. Comme il y a 3 classe et un paramètre estimé, il faut comparer à un test du $\chi^2$ avec 1 degré de liberté.

Après calcul, la statistique de test vaut $\sum_{l=1}^3\frac{(n_i-np_i)^2}{np_i} = 0.67$

Il faut comparer cela à la valeur critique de 3.841, qui nous donne comme région d'acceptation $[0,3.841]$.

Nous ne pouvons donc pas rejeter l'hypothèse que ces données suivent bien une loi de Poisson.


:::

b) Effectuer à présent un test de Kolmogorov. Est-ce que votre conclusion évolue ?

:::{admonition} Solution b)
:class: dropdown
Le tableau des fréquences empiriques est :

$$\begin{array}{|c|c|c|c|c|c|c|c|c|c|c|}
        \hline
         \text{Nombre d'outils renouvelés} & 0&1&2&3&4& 5&6&7&8&9 \\
         \hline
         \text{Fréquence cumulée de sites}  & 0.0357& 0.1071& 0.1785 &0.2857 & 0.3928& 0.5714& 0.75 &0.8214&0.9285&1 \\
         \hline
             \text{Fréquence cumulée théorique}&0.0067& 0.0404& 0.1247& 0.265& 0.4405&0.616 & 0.7622& 0.8666&0.9319& 0.9682\\
           \hline
        \end{array}$$
        
On trouve donc que 

$$\sup|\hat{F_n}(t)-F(t)|=0.047$$

Il faut comparer cette valeur à 0.26404 (voir table {ref}`fig:quantile-Kolmogorov`), et donc encore une fois, nous ne pouvons pas rejeter l'hypothèse que ces données suivent bien une loi de Poisson.


:::

```

### Test d'égalité de loi de Kolmogorov-Smirnov

Supposons que l'on ne connaisse plus la loi de la variable d'intérêt, mais cherchons plutôt à tester l'égalité des lois de deux séries d'observations. 

Considérons deux  échantillons de tailles $n$ et $m$  respectivement : 

$(X_1,...,X_n)$ des variables aléatoires indépendantes de loi $F_1$

$(Y_1,...,Y_n)$ des variables aléatoires indépendantes de loi $F_2$.


Nous cherchons à tester l'hypothèse 

$$H_0 : F_1=F_2 \text{ et il s'agit d'une loi continue.}$$
contre l'alternative générale.

Soient $\hat{F_1}$ et $\hat{F_2}$ les fonctions de répartition empirique des deux échantillons. Inspiré par le test de Kolmogorov, nous posons comme statistique du test :

$$ \Delta := \sup\limits_{t\in\R}|\hat{F_1}(t)-\hat{F_2}(t)|. $$

Sous $H_0$, la variable aléatoire $\Delta$ suit la loi de Kolmogorov-Smirnov, dont on utilise la table afin de déterminer $s_\alpha$, le quantile d'ordre $1-\alpha$,  qui vérifie :

$$\alpha= \mathbb{P}(\Delta>s_\alpha | H_0)$$

On rejette alors $H_0$ si la valeur observée $\delta$ de la statistique satisfait $\delta>s_\alpha$ et on ne rejette pas $H_0$ lorsque $\delta\leq s_\alpha$.




