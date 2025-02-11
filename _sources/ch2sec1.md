## Estimateur et premiers critères

$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

:::{prf:definition} Estimateur
Soit $F(\theta)$ une quantité qui dépend de la loi $\mathbb{P}_\theta$
On appelle estimateur de $F(\theta)$ une statistique $T_n$(ou une suite de statistique $(T_n)_{n\in \N}$).

:::

::::{prf:example}
:class: dropdown
Prenons $(\mathbb{P}_\theta)_{\theta\in \R_+}$ la famille des lois uniformes $\mathcal{U}([0,\theta])$. Des exemples d'estimateurs de $\theta$ sont :

- deux fois la moyenne empirique, c'est-à-dire ${\displaystyle T_n(x_1,...,x_n) = \frac{2}{n}\sum_{i=1}^n x_i}$.

Il s'agit d'un bon candidat, puisque par linéarité, $\mathbb{E}_\theta(\overline{X}) = \frac{\theta}{2}$.
    
- la plus grande des valeurs, c'est-à-dire ${\displaystyle T_n(x_1,...,x_n)  = \sup\limits_{k\in [\![1,n]\!]} x_k}$

Il s'agit d'un bon candidat, car l'on peut prouver que pour des lois uniformes, $\mathbb{E}_\theta(\sup\limits_{k\in [\![1,n]\!]} X_k) = \frac{n}{n+1}\theta$.
    
- la statistique ${\displaystyle T_n(x_1,...,x_n)  = \sup\limits_{k\in [\![1,n]\!]} x_k +\inf\limits_{k\in [\![1,n]\!]} x_k}$

Il s'agit d'un bon candidat, car l'on peut prouver que pour des lois uniformes, $\mathbb{E}_\theta(\sup\limits_{k\in [\![1,n]\!]} X_k+\inf\limits_{k\in [\![1,n]\!]} X_k) = \theta$.

- la statistique ${\displaystyle T_n(x_1,...,x_n)  = \frac{n+1}{n}\sup\limits_{k\in [\![1,n]\!]} x_k}$.


- la statistique $T_n(x_1,...,x_n)  = x_1$.
::::

:::{prf:remark}
:class: dropdown
 Si $(T_n)$ est une suite de statistique, l'estimateur prendre la limite des $T_n(x_1,...x_n)$ lorsqu'elle existe, et une valeur arbitraire sinon, est un estimateur courant. Nous pourrons définir des qualités similaires à une simple statistique, que l'on appellera asymptotique.

:::

### Comment estimer une performance

Afin d'évaluer la performance d'un estimateur, nous allons chercher à minimiser l'erreur quadratique (c'est-à-dire la moyenne du carré de la distance entre l'estimateur et la quantité désirée).

Formellement, on veut pour le "bon" $\theta$ minimiser la quantité  

$$\mathbb{E}_\theta\left[\left({T_n(X_1,...,X_n)-F(\theta)}\right)^2 \right].$$

 Nous allons chercher à comprendre cette quantité. Remarquons que nous pouvons appliquer une relation de Pythagore (avec comme produit scalaire entre variables aléatoire l'espérence du produit) :

::::{prf:property}
:class: dropdown
:label: Biais_Variance
Soit $T_n$ un estimateur de $F(\theta)$, alors on a que 

$$\mathbb{E}_\theta\left[\left(T_n(X_1,...,X_n)-F(\theta)\right)^2 \right] = V_\theta(T_n) + \left(\ \mathbb{E}_\theta[T_n]-F(\theta)\ \right)^2. $$


:::{prf:proof} 
 On obtient directement le résultat avec le théorème de Pythagore. Une preuve alternative est de dire que :

$$\mathbb{E}_\theta\left[\left({T_n(X_1,...,X_n)-F(\theta)}\right)^2 \right] = \mathbb{E}_\theta\left[\left({T_n(X_1,...,X_n)-\mathbb{E}_\theta[T_n] + \mathbb{E}_\theta[T_n]-F(\theta)}\right)^2 \right] $$

$$=\mathbb{E}_\theta\left[\left(T_n(X_1,...,X_n)-\mathbb{E}_\theta[T_n]\right)^2+2\left(T_n(X_1,...,X_n)-\mathbb{E}_\theta[T_n]\right)\left(\mathbb{E}_\theta[T_n]-F(\theta)\right)+ \left(\mathbb{E}_\theta[T_n]-F(\theta)\right)^2 \right] $$
$$= V_\theta(T_n) +0+ \left(\mathbb{E}_\theta[T_n]-F(\theta)\right)^2$$


:::

::::

:::{prf:definition} Intuition et vocabulaire
:class: dropdown
L'erreur quadratique est donc composée de deux termes d'erreur. On parle de décomposition en biais-variance. L'erreur quadratique est augmentée par la dispersion suivant la loi $\mathbb{P}_\theta$  de la statistique (terme de variance), et par l'importance de l'erreur en moyenne de la statistique (deuxième terme). On appelle le terme $\mathbb{E}[T_n]-F(\theta)$ le _biais_ de la statistique. Si ce terme est nul, l'on dira que la statistique est _sans biais_.

Une des questions essentielles que nous nous poserons sera la dépendance du risque quadratique vis-à-vis de la taille de l'échantillon. Elle revient à se demander à quelle vitesse nous pouvons approcher la bonne valeur, mais également comment obtenir une telle vitesse d'approche.
:::

### Biais d'un estimateur

:::{prf:definition} Biais et biais asymptotique

On dit qu'un estimateur $T_n$ d'un paramètre $f(\theta)$ est _sans biais_ si 

$$\mathbb{E}[T_n(X_1,...,X_n)] = f(\theta).$$

On dit qu'une suite d'estimateur $(T_n)$ est _asymptotiquement sans biais_ si la limite des espérances existe et 

$$ \lim \limits_{n\to +\infty}\mathbb{E}[T_n(X_1,...,X_n)] = f(\theta).$$

:::

::::{prf:example}
:class: dropdown
Prenons $(\mathbb{P}_\theta)_{\theta\in \R_+}$ la famille des lois uniformes $\mathcal{U}([0,\theta])$. Des exemples d'estimateurs de $\theta$ sont :

- deux fois la moyenne empirique est sans biais.

En effet, $\mathbb{E}(\frac{2}{n}\sum_{i=1}^n X_i) = \frac{2}{n}\sum_{i=1}^n \mathbb{E}(X_i) = \frac{2}{n}\sum_{i=1}^n \frac{\theta}{2} = \theta.$
    
- la suite d'estimateur qui prend le plus grand des résultats est biaisé, mais asymptotiquement sans biais.

En effet, pour $0\leq t\leq \theta$, on a que 
$\mathbb{P}_\theta(sup(X_i) \leq t)= \prod_{i=1}^n \mathbb{P}_\theta(X_i\leq t) = \left(\frac{t}{\theta}\right)^n.$

Ensuite, pour $Y$ une variable aléatoire, on peut montrer avec le théorème de Tonelli que

$$\mathbb{E}(Y)=\int_0^{+\infty} \mathbb{P}(Y> t) dt $$

Donc finalement, 

$$\mathbb{E}_\theta(\sup X_i)= \int_0^\theta \mathbb{P}_\theta (\sup X_i > t),$$
$$=\int_0^\theta(1-\left(\frac{t}{\theta}\right)^n) dt= \theta \int_0^1 (1- u^n)du= \theta \frac{n}{n+1}$$

Donc en particulier, l'estimateur est biaisé, mais asymptotiquement sans biais.
::::

::::{prf:property}
:class: dropdown
:label: Unicite_efficace
S'il existe un estimateur sans biais de variance minimale parmi tous les estimateurs sans biais, alors il est unique à vérifier cette propriété.


:::{prf:proof} 
Soit T et T' deux estimateurs vérifiant la propriété (en particulier, ils ont la même variance). Considérons alors l'estimateur $U=\frac{T+T'}{2}$.

Il est clair par linéarité de l'intégrale que $U$ est sans biais. Maintenant,

$$V(U)= \frac{1}{4}V(T)+\frac{1}{4}V(T') +2 Cov(\frac{T}{2}, \frac{T'}{2})\leq \frac{V(T)+V(T') +2\sqrt{V(T)V(T')}}{4} \text{ par l'inégalité de Cauchy-Schwarz}$$
$$= \frac{(\sqrt{V(T)}+\sqrt{V(T')})^2}{4}= V(T) \text{ par égalité des variances de T et T'}$$

En particulier, comme T est de variance minimale, il y a égalité dans l'inégalité précédente. Par le cas d'égalité dans l'inégalité de Cauchy-Schwarz, T et T' sont positivement affinement lié. Comme ils sont de même moyenne et variance, ils sont donc égaux.

:::

::::


:::{prf:definition} Estimateur plus efficace
:class: dropdown
On dit qu'un estimateur T sans biais est _plus efficace_ qu'un autre estimateur T' sans biais si sa variance est plus petite.


:::

### Convergence d'une suite d'estimateurs


    
:::{prf:definition} Estimateur convergent
On dit qu'une suite d'estimateur $T_n$ de $f(\theta)$ est _convergente_ (ou consistante, consistancy en anglais) si elle converge en probabilité vers ce $f(\theta)$, c'est-à-dire 

$$\forall \theta, \forall \epsilon >0, \mathbb{P}_\theta(|T_n(X_1,...,X_n)- f(\theta)|>\epsilon) \to 0$$

Comme la limite est une constante, on peut montrer que demander seulement la convergence en loi vers l'estimée n'affaiblie pas la condition. Il s'agit donc de la plus faible des notions de convergence possible pour des expériences statistiques.

(H.P.) On dira qu'une suite d'estimateur est _fortement consistante_ si la convergence est presque sûre :

$$ \forall \theta, \mathbb{P}_\theta\left(\lim\limits_{n\to+\infty}T_n(X_1,...,X_n)= f(\theta)\right)=1$$
:::


::::{prf:property} Convergence et continuité
:class: dropdown
:label: Convergence_continuite
 Soit $T_n$ une suite d'estimateur de $f(\theta)$ et $\phi$ une fonction continue en ce point.
 
Alors si $T_n$ est convergente, alors $\phi(T_n)$ est une suite d'estimateur convergents vers $\phi(f(\theta))$.

Si $T_n$ est fortement consistante, alors il en est de même pour $\phi(T_n)$

:::{prf:example}
On suppose que la famille de loi indépendante identiquement distribuée admet une espérance pour toute loi.

Si l'on peut écrire $\theta = f(\mathbb{E}(X))$ avec f une fonction continue défini au voisinage de $\Theta$, alors l'estimateur 

$$ f\left(\frac{1}{n}\sum_{i=1}^n X_i\right)$$

est convergent et fortement consistant.
:::

::::

::::{admonition} Méthode pour proposer certains bons estimateurs
:class: tip
On considère $(X_i)$ des variables aléatoires iid, et l'on note $m_j=\mathbb{E}[X^j]$ le moment d'ordre $j$.

On cherche à estimer $\theta=\theta(m_1,m_2...,m_k)$.

L'estimateur par la méthode des moments 

$$\hat{\theta}:= \theta(\hat{m_1},\hat{m_2},...,\hat{m_k}) \qquad \text{ avec } \hat{m_p}=\frac{1}{n}\sum_{j=1}^nX_j^p$$

est alors un bon candidat.

```{prf:example}
Soit $X_1,...,X_n$ v.a. i.i.d. de loi $\mathcal{N}(m,\sigma^2)$.

L'estimateur par la méthode des moments de $\sigma^2$ est alors :

$$\hat{\sigma^2}=\hat{m_2}-\hat{m_1}^2=\frac{1}{n}\sum_{j=1}^nX_j^2-\left(\frac{1}{n}\sum_{j=1}^nX_j\right)^2$$
```
::::


::::{prf:property} Critère utile de convergence
:class: dropdown
Une suite d'estimateurs $(T_n)$, asymptotiquement sans biais et telle que 

$$\lim\limits_{n\to +\infty} V(T_n) = 0,$$

est convergente.

:::{prf:proof}
En utilisant la décomposition biais-variance, l'on obtient que 

$$\mathbb{E}\left[ (T_n-f(\theta))^2\right] = V(T_n)+ \left(f(\theta)-\mathbb{E}(T_n)\right)^2 \underset{n\to +\infty}{\to} 0$$

Comme la convergence en moyenne quadratique implique la convergence en probabilité, la suite d'estimateur est bien convergente.
:::

::::


```{exercise} Estimateurs pour les lois de Poisson
:class: dropdown
:label: exer07
On considère l'expérience statistique issue de la répétition indépendante de n tirage $(X_1,...,X_n)$ de variable aléatoire suivant des lois de Poisson de paramètre $\lambda>0$.

a) Montrer que la moyenne empirique $\overline{X_n} = \frac{1}{n} \sum_{i=1}^n X_i$ est un estimateur sans biais de $\lambda$.

:::{admonition} Solution a)
:class: dropdown
Par linéarité de l'intégrale, 
            
$$\mathbb{E}_\lambda(\overline{X_n})= \mathbb{E}_\lambda({X_1})=\lambda$$

Donc l'estimateur est sans biais.
:::

b) Montrer que la moyenne empirique converge presque sûrement et en moyenne quadratique vers $\lambda$. En déduire le caractère convergent de l'estimateur.

:::{admonition} Solution b)
:class: dropdown
La convergence presque-sûre est la conséquence de la loi forte des grands nombres.

La convergence $L^2$ est directe. En effet, 

$$\mathbb{E}_\lambda\left[(\overline{X_n}-\lambda)^2\right] =V(\overline{X_n})=\frac{V_\lambda(X_1)}{n^2} \to 0$$

En particulier, l'estimateur moyenne empirique converge en probabilité, et est donc convergent.
     
:::

c) Montrer que la moyenne empirique est asymptotiquement normale, c'est-à-dire que $\sqrt{n}(\overline{X_n}- \lambda)$ converge en loi vers une loi normale, dont on précisera les paramètres.

:::{admonition} Solution c)
:class: dropdown
Il s'agit d'une application directe du théorème central limite
     
:::

d) Montrer que la variance empirique $S_n = \frac{1}{n-1}\sum_{i=1}^n (X_i-\overline{X_n})^2$ est un estimateur sans biais, et montrer que $\sqrt{n}\left( S_n-\lambda\right)$ converge en loi vers une loi normale dont on précisera les paramètres.s.

_On pourra utiliser que pour une loi de Poisson, le moment centré d'ordre 4 vérifie $\mathbb{E}[(X-\lambda)^4]=\lambda+3\lambda^2$, mais également le lemme de Slusky (voir {ref}`Slutsky`) qui permet de dire que si $Y_n$ converge en loi vers Y et que $X_n$ converge en probabilité vers $X$, alors $X_nY_n$ (respectivement la somme) converge en loi vers $XY$ (respectivement la somme des limites)._
:::{admonition} Solution d)
:class: dropdown
Nous avons déjà vu le calcul pour le biais de la variance empirique dans {prf:ref}`moy_var_empirique`.

Maintenant, par le théorème central limite, avec la première indication pour calculer la variance de l'estimateur, on trouve :

$$ \sqrt{n}\left(\frac{1}{n}\sum_{i=1}^n (X_i-\lambda)^2-\lambda \right) \overset{Loi}{\to} \mathcal{N}(0, \lambda+2\lambda^2) \qquad \sqrt{n}\left(\overline{X_n}-\lambda \right) \overset{Loi}{\to} \mathcal{N}(0, \lambda) $$

Alors,

$$\sqrt{n}\left(S_n-\lambda\right) = \sqrt{n}\left(\frac{1}{n-1}\sum_{i=1}^n (X_i-\overline{X_n})^2-\lambda\right)$$
 $$= \sqrt{n}\left(\frac{1}{n-1}[\sum_{i=1}^n (X_i-\lambda)^2 - n(\overline{X_n}-\lambda)^2]-\lambda \right)$$
$$= \frac{n}{n-1} \sqrt{n}\left( \frac{1}{n}\sum_{i=1}^n (X_i-\lambda)^2-\lambda \right) + \frac{n}{n-1} \sqrt{n}\left( \overline{X_n}-\lambda\right)^2 -\frac{\sqrt{n}}{n-1} \lambda$$


Maintenant, comme $\overline{X_n}-\lambda$ converge presque surement vers 0 (et donc en particulier converge en probabilité vers 0) et que $\sqrt{n}(\overline{X_n}-\lambda)$ converge en loi, $\frac{n}{n-1} \sqrt{n}\left( \overline{X_n}-\lambda\right)^2$ converge en loi vers 0. Comme la limite est constante, la convergence est même en probabilité.


Donc, comme d'après le lemme de Slusky $\frac{n}{n-1} \sqrt{n}\left( \frac{1}{n}\sum_{i=1}^n (X_i-\lambda)^2-\lambda \right) \overset{Loi}{\to} \mathcal{N}(0, \lambda+2\lambda^2) $, nous obtenons en appliquant encore une fois le lemme que

$$\sqrt{n}\left(S_n-\lambda\right) \overset{Loi}{\to} \mathcal{N}(0,\lambda+ 2\lambda ^2) $$     
:::

e) Quel estimateur privilégier pour avoir de meilleurs résultats asymptotiques ?

:::{admonition} Solution e)
:class: dropdown
Comme $S_n^2$ a une plus grande variance asymptotique, l'on privilégiera la moyenne empirique $\overline{X_n}$ afin de diminuer l'écart autour du paramètre d'intérêt.
     
:::
```

