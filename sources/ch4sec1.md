(Rappel-Gaussienne)=
## Rappels sur la loi
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

:::{prf:definition} Variable Gaussienne
:class: dropdown
La loi normale de moyenne $m$ et de variance $\sigma^2$, noté $\mathcal{N}(m,\sigma^2)$, est la loi d'une variable aléatoire réelle X  absolument continue par rapport à la mesure de Lebesgue, de densité :

$$f_X(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-m)^2}{2\sigma^2}}$$

La fonction caractéristique de $\mathcal{N}(m,\sigma^2)$ est 

$$t\mapsto \varphi_X(t):=\mathbb{E}(e^{itx})= e^{itm-\frac{t^2\sigma^2}{2}}.$$
:::


::::{prf:definition} Vecteur Gaussienne
:class: dropdown
On dit qu'un vecteur aléatoire $X= (X_1, ... X_n)^t$ est un _vecteur gaussien_ si pour toute collection de réels $(\lambda_1,...\lambda_n)$, la variable aléatoire $\sum_{i=1}^n \lambda_i X_i$ suit une loi normale.

:::{danger}
Il n'est pas suffisant que chacune des coordonnées suivent une loi normale. En effet, prenons $X\sim\mathcal{N}(0,1)$ et $\epsilon$ une variable aléatoire (indépendante de X) telle que

$$\mathbb{P}(\epsilon=1)=\mathbb{P}(\epsilon=-1)=\frac{1}{2}$$

Alors $X$ et $\epsilon X$ sont des variables gaussiennes, mais $(X,\epsilon X)$ n'est pas un vecteur gaussien puisque $\mathbb{P}(X+\epsilon X=0)=\frac{1}{2}\neq 0$ est impossible pour toute variable aléatoire absolument continue (classe contenant les lois normales).
:::

::::




```{exercise} Construire des vecteur gaussiens
:class: dropdown
Pour  $X_1, ... X_n$ une suite de variable aléatoire gaussienne **indépendante**, le vecteur aléatoire    $X= (X_1, ... X_n)^t$ est gaussien. 

Si en plus les $X_i$ sont centrés et réduit, on parlera alors de _vecteurs gaussiens standard_.

:::{admonition} Solution 
:class: dropdown
La preuve se fait directement en calculant pour toute combinaison linéaire la fonction caractéristique, et en remarquant qu'il s'agit de la fonction caractéristique d'une loi normale.
:::

Si $X= (X_1, ... X_n)^t$ est un vecteur gaussien de matrice de covariance K et $A\in M_{p,n}, B\in M_{p,1}$ est une matrice, montrer que le vecteur $AX+B$ est gaussien, de matrice de covariance 

$$AKA^t.$$

:::{admonition} Solution 
:class: dropdown
Le caractère Gaussien est immédiat, puisque pour tous $\lambda \in \R^n$, l'on a 

$$<\lambda, AX+B> = <A^t\lambda,X>+<\lambda, B> .$$

Pour la matrice de covariance, il s'agit d'une relation générale, issue de la bilinéarité de la covariance :

$$ Cov\left[(AX)_i,(AX)_j\right] = \sum_{q}\sum_{p} a_{i,q}Cov\left[X_q,X_p\right] a_{j,p}= AKA^t_{i,j}$$
:::

Soit $(Y_1,...,Y_n)^t$ un vecteur gaussien, montrer qu'il existe $L\in M_{n,n}$ et $(X_1,...,X_n)^t$ vecteur gaussien standard tels que $Y$ et $LX$ sont de même loi.

_On pourra utiliser que pour $K\in M_{n,n}(\R)$ une matrice symétrique semi-définie positive, il existe (au moins) une matrice $L\in M_{n,n}(\R)$ telle que $K=L^tL$, voir {ref}`Chol`_

:::{admonition} Solution 
:class: dropdown
Il suffit de remarquer que pour Y un vecteur Gaussien, sa fonction caractéristique ne dépend que de sa moyenne $m$ et de sa matrice de covariance $K$ :

$$\forall \lambda \in \R^n, \quad \varphi_Y(\lambda) = \mathbb{E}[e^{i<\lambda,X>}] = e^{i<\lambda,m>-\frac{\lambda^tK\lambda}{2}}$$
:::
```



::::{prf:theorem} Caractérisation

Soit $m \in R^d$, et  $\Lambda$ une matrice $d \times d$ symétrique _définie positive_. On considère X un vecteur aléatoire, alors on a l'équivalence entre les points
- $X$ est un vecteur gaussien de moyenne $m$ et de matrice de covariance $\Lambda $ ;
- $X$ admet une densité par rapport à Lebesgue de la forme

$$\frac{1}{(\sqrt{2\pi})^d\sqrt{det(\Lambda)}} \exp(-\frac{(x-m)^t\Lambda(x-m)}{2})$$

On le note 

$$X\sim\mathcal{N} \left(m=\begin{pmatrix}m_1\\\vdots\\m_n \end{pmatrix}, \Lambda \right).$$

Lorsque c'est le cas, la variable aléatoire $X_j$ est alors de loi $\mathcal{N} (m_j , \Lambda_{jj} )$.

:::{prf:proof}
 La formule est trivialement vraie pour les vecteurs gaussiens standards. Le cas général découle de la formule de changement de variables pour la mesure de Lebesgue et de l'exercice précédent.
:::

::::


:::{prf:definition}
Soit $(X_1,...X_n)^t$ un vecteur gaussien centré. On appelle _espace gaussien_ engendré par les $X_i$ l'espace vectoriel engendré par la famille des $X_i$ :

$$ Vect(X_i) = \left\{ \sum_{i=1}^n \lambda_i X_i | \lambda \in \R^n\right\}$$
:::
