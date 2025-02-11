(Cochran)=
## Théorème de Cochran (HP)

Une des propositions étonnante des espaces gaussiens est que l'indépendance s'y lit très facilement, et se réduit même à un problème géométrique :
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

::::{prf:proposition} Espace Gaussien et indépendance
:class: dropdown
Soit $Y,Z$ deux variables aléatoires centré appartenant à un même espace gaussien.
    
Alors Y et Z sont indépendantes si et seulement si elles ont orthogonales pour le produit scalaire sur les vecteurs centré qu'est la covariance (_i.e._ si elles sont décorrélées) : 

$$\mathbb{E}[<Y.Z>] = Cov(Y,Z)=0.$$

```{prf:proof}
On peut, sans perte de généralité, supposer que le vecteur gaussien $(X_1,...,X_n)$ générant l'espace gaussien est un vecteur standard (centré de variance $I_n$).

Comme le sens direct est immédiat, nous allons prouver le sens réciproque. On écrit pour cela $Y= \sum_{i=1}^n \lambda_i X_i$ et $Z= \sum_{i=1}^n \tilde{\lambda}_i X_i$.

Le caractère décorrélé des variables $Y$ et $Z$ se lit dans les paramètres comme $\mathbb{E}[YZ]=\sum_{i=1}^n\lambda_i\tilde{\lambda}_i=0$.

Pour montrer l'indépendance, nous allons montrer que la fonction caractéristique du couple $(Y,Z)$ est le produit de leurs fonctions caractéristiques respectives. Soit $\mu\in \R$ et $\tilde{\mu} \in \R$. Alors, 

$$\mathbb{E}[e^{i\mu Y} e^{i\tilde{\mu}Z}]=\mathbb{E}[e^{i\mu \sum_i \lambda_iX_i} e^{i\tilde{\mu}\sum_i \tilde{\lambda}_iX_i}],$$
$$=\mathbb{E}[\prod_i e^{i(\mu \lambda_i+\tilde{\mu}\tilde{\lambda}_i)X_i}],$$

Et par indépendance des $X_i$,

$$\mathbb{E}[e^{i\mu Y} e^{i\tilde{\mu}Z}]=\prod_i \mathbb{E}[ e^{i(\mu \lambda_i+\tilde{\mu}\tilde{\lambda}_i)X_i}] $$
$$=\prod_i e^{-\frac{(\mu\lambda_i+\tilde{\mu}\tilde{\lambda}_i)^2}{2}} $$
$$= exp(-\frac{1}{2}\sum_i(\mu\lambda_i+\tilde{\mu}\tilde{\lambda}_i)^2) $$

Par orthogonalité des coefficients - hypothèse de décorrelation
$$=  exp(-\frac{1}{2}\sum_i \mu^2\lambda_i^2+\tilde{\mu}^2\tilde{\lambda}_i^2) $$
$$=  \mathbb{E}[e^{i\mu \sum_{i}\lambda_i X_i}]\mathbb{E}[e^{i\tilde{\mu} \sum_{i}\tilde{\lambda}_i X_i}]$$
$$= \mathbb{E}[e^{i\mu Y}] \mathbb{E}[e^{i\tilde{\mu} Z}].$$


Ce qui nous donne bien l'indépendance.
```

```{prf:corollary}
Considérons deux sous espaces vectoriels $E$ et $E'$ d'un espace gaussien. Alors toutes les variables aléatoires de E sont indépendantes de toutes les variables de $E'$ si et seulement si $E$ et $E'$ sont orthogonales.
```

::::






::::{prf:proposition} Décomposition 
:class: dropdown
Soit $X=(X_1,...,X_n)^t$ un vecteur gaussien centré de matrice de covariance $K$ et soit $M\in S_n^+$ une matrice symétrique semi-définie positive. On considère également $(Z_i)$ des variables aléatoires indépendantes de loi $\chi^2_1$.
    
Alors si l'on note $K=LL^t$ une décomposition de Cholesky ($L$ triangulaire supérieure, voir {ref}`Choleski`) et $(\lambda_i)$ les valeurs propres avec multiplicités de la matrice $L^tML$, la variable aléatoire $X^tMX$ est distribué comme $\sum_i \lambda_i Z$.

```{prf:proof}
Sans perte de généralité, on peut supposer (on ne travaille qu'avec des égalités en loi) que $X=LY$ avec $Y\sim \mathcal{N}(0,I_n)$ un vecteur gaussien standard. 

D'après le théorème spectral, il existe $O$ une matrice orthogonale telle que 

$$L^tML = O^t\text{diag}(\lambda_1,...,\lambda_n) O. $$

Or $OY$ est encore un vecteur standard, puisque $O^tO=I_n$. Donc 

$$X^tM X= Y^tL^tMLY = (OY)^t\text{diag}(\lambda_1,...,\lambda_n) (O Y)$$

Ce qui nous donne directement le résultat.
```
::::

::::{prf:theorem} Théorème de Cochran}

Soit $X\sim \mathcal{N}(0,I_n)$ un vecteur gaussien standard. L'on considère une décomposition orthogonale $\R^n = \oplus_{i=1}^k E_i$ où les $E_i$ sont des sous-espaces vectoriels deux à deux orthogonaux de $\R^n$. On note $\pi_{E_i}$ la projection orthogonale sur l'espace $E_i$.

Alors la famille $(\pi_{E_i}X)_{1\leq i \leq k}$ est une famille indépendante, et pour chaque $j$, on connait la loi de la norme :

$$ ||\pi_{E_j}X||^2_2\sim \chi^2_{dim(E_j)}$$

```{prf:proof}
Remarquons d'abord que la loi de la norme quadratique est une conséquence immédiate de la proposition précédente. En effet, la matrice de covariance de $ \pi_{E_j}X$ est $\pi_{E_j}\pi_{E_j}^t=\pi_{E_j}$. Or les valeurs propres d'une matrice de projection sont 1 avec comme multiplicité la dimension de l'espace stable $dim(E_j)$ et 0.

Pour montrer l'indépendance, nous pouvons utiliser la première proposition et son corollaire pour montrer que $\pi_{E_j}$ est indépendant de $(\pi_{E_i})_{i<j}$. En effet, les $\pi_{E_i}$ sont bien dans un espace gaussien comme image par une application linaire d'un espace gaussien, et sont orthogonaux puisque $\pi_{E_j}X \in E_j  \bot \oplus_{i=1}^{j-1} E_i$ (et donc en particulier $\forall Y \in Vect(\pi_{E_i})_{i<j}, \mathbb{E}(<\pi_{E_j}X,Y>)=0\ $).

```
::::



Ceci nous permet de montrer directement le résultat suivant d'estimation d'une loi gaussienne en dimension 1 que nous avions admis :

::::{prf:theorem} Moyenne et variance empirique de loi normales 

Soit $(X_i)$ une suite iid de variables, de loi $\mathcal{N}(m,\sigma^2)$. Alors :

$$\overline{X} \sim \mathcal{N}(m,\frac{\sigma^2}{n}), \qquad \overline{X} \text{ et } S_X^2 \text{ sont indépendants}$$

$$\frac{(n-1)S_X^2}{\sigma^2} = \frac{\sum_{i=1}^n \left(X_i-\overline{X}\right)^2}{\sigma^2}\sim \chi_{n-1}^2 $$

_loi du chi-2 à (n-1) degré de libertés_

```{prf:proof}
Sans perte de généralité, l'on peut supposer que $m=0$ et que $\sigma=1$. L'on remarque alors que 

$$\overline{X}_n = \frac{1}{n}\begin{pmatrix}1\\\vdots\\1\end{pmatrix}\times\begin{pmatrix}1&\cdots&1\end{pmatrix} \times X.$$

C'est-à-dire que $\overline{X}_n$ est la projection orthogonale de $X$ sur l'espace engendré par $(1,\dots,1)^t$. Notons $\pi$ le projecteur. D'après le théorème de Cochran, $\pi X$ et $X-\pi X$ sont indépendants, et la norme quadratique de $X-\pi X$ suit une loi $\chi^2_{n-1}$.

Ceci nous donne les deux derniers points du théorème, la loi de $\overline{X}_n$ étant immédiate.

```
::::



 
```{exercise}
:label: exer16
 On considère un vecteur aléatoire à valeurs dans $\R^3$, de composantes $X_1$, $X_2$ et $X_3$ dans la base canonique. On suppose que $X_1$, $X_2$ et $X_3$ sont des variables aléatoires réelles indépendantes de loi gaussienne $\mathcal{N} (0, 1)$.
 
a) Quelle est la densité du triplet $(X_1, X_2, X_3)$ ?



:::{admonition} Solution a)
:class: dropdown
 Par indépendance, il s'agit du produit des densités des composantes.

On reconnait alors la densité d'un vecteur Gaussien, de moyenne $0_{\R^3}$ et de matrice de covariance $I_3$.
:::

Soit M la matrice de changement de base orthonormée suivante :

$$ M= \begin{pmatrix}
            \frac{1}{\sqrt{3}}&\frac{1}{\sqrt{3}}&\frac{1}{\sqrt{3}}\\
            \frac{1}{\sqrt{2}}&-\frac{1}{\sqrt{2}}&0\\
            \frac{1}{\sqrt{6}}&\frac{1}{\sqrt{6}}&-\frac{2}{\sqrt{6}}
        \end{pmatrix}$$

Vous pourrez admettre par la suite que $MM^t=I_3$.

b) Donner la loi de $Y=M^tX$.

:::{admonition} Solution b)
:class: dropdown
Il s'agit d'une transformation linéaire d'un vecteur gaussien, donc $Y\sim \mathcal{N}(M^t0_{\R^3},M^tI_3(M^t)^t) =\mathcal{N}(0_{\R^3},I_3).$
:::

c) En déduire la loi des composantes $Y_1,Y_2$ et $Y_3$ de $Y$.

:::{admonition} Solution c)
:class: dropdown
Il s'agit de calculer des lois marginales. L'on trouvera $Y_i \sim \mathcal{N}(0,1).$
:::

d) Montrer qu'avec $\overline{X}=\frac{1}{3}(X_1+X_2+X_3)$, l'on a que 

$$ \sum_{i=1}^3 X_i^2 =\sum_{i=1}^3 Y_i^2  $$

$$ Y_2^2+Y_3^2 =\sum_{i=1}^3 X_i^2 - 3 \overline{X}^2$$

En déduire que les variables $\overline{X}$ et $S_X^2 = \frac{1}{2} \sum_{i=1}^3 (X_i-\overline{X})^2$ sont indépendantes.

:::{admonition} Solution d)
:class: dropdown
Le premier point consiste à remarquer que $M$ étant orthogonale, l'application linéaire canonique associée préserve la norme. 

Le deuxième découle directement du fait que $Y_1= \frac{3}{\sqrt{3}}\overline{X}$.


Enfin, comme $S_X^2 = \frac{1}{2} \sum_{i=1}^3 (X_i-\overline{X})^2 = \frac{1}{2}(Y_2^2+Y_3^3)$. 

Comme $Y_1$ et $(Y_2,Y_3)$ sont indépendantes, nous en déduisons le dernier point.
:::

e) Donner la loi de $\overline{X}$ et de $2S_X^2$.

:::{admonition} Solution e)
:class: dropdown
Avec le point précédent,
$\overline{X}\sim \mathcal{N}(0,\frac{1}{3})$ et 
$2S_X^2 \sim \chi^2_2$.

Nous avons bien redémontré le corollaire du théorème de Cochran dans ce cas particulier.
:::

```
 