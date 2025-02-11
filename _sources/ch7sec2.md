

## Inégalités probabilistes
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

(Jensen)=
### Inégalité de Jensen pour les fonctions convexes

Cette propriété est essentielle si l'on cherche à majorer des espérances, mais aussi lorsque l'on cherche des inégalités de concentrations ou des majorations de probabilités pour des tests.
 

:::{prf:definition} Fonctions convexes
:class: dropdown
On appelle fonction convexe toute application
$f: I\subset\R \to \R$, où $I$ est un intervalle, vérifiant :

$$ \forall (x,y) \in V^2, \forall \lambda\in [0,1] : f\left[\lambda x+(1-\lambda)y\right] \leq \lambda f(x)+ (1-\lambda)f(y)$$
:::

:::{prf:proposition} Propriétées classiques des fonctions convexes
:class: dropdown
Soit $f$ une fonction convexe. On a que 

$$\forall a<b<c,\quad \frac{f(a)-f(b)}{a-b}\leq \frac{f(a)-f(c)}{a-c}\leq \frac{f(b)-f(c)}{b-c}  .$$
- f est continue.
- f est dérivable sauf en un nombre dénombrable de points.
- Si f est dérivable sur un intervalle, sa dérivée y est croissante.
- Si f est deux fois dérivable sur un intervalle, sa dérivée seconde y est positive.


:::


::::{prf:theorem}
Soit $(\Omega, \mathcal{T},\mathbb{P})$ un espace probabilisé.\newline
    Soit f une fonction convexe sur un intervalle réel $[a,b]$ et X une variable aléatoire à valeurs dans I, dont l'espérance $\mathbb{E}(f(X))$ existe, alors 

$$ f(\mathbb{E}(X))\leq \mathbb{E}(f(X))$$

```{prf:proof}

Soit $z\in [a,b]$. Comme f est une fonction convexe, pour z fixé, il existe $l \in \R$ tel que 

$$\forall x \in [a,b], f(x)\geq f(z) + (z-x) \times l$$

En effet, il suffit de prendre $l=\limsup\limits_{x\to z^-} \frac{f(z)-f(x)}{z-x}$ et la propriété découle directement de la croissance des taux d'accroissement (premier point de la propriété précédente).

\underline{Remarque :} si f est dérivable en z, il s'agit alors de prendre la dérivée de f en z, et d'utiliser qu'une fonction convexe est au-dessus de ses tangentes.

Donc pour la variable aléatoire X, l'on a l'inégalité : 

$$f(X)\geq f(z) + (z-X) \times l.$$

Par la croissance et linéarité de l'espérance, il en vient que 

$$ \mathbb{E}[f(X)] \geq f(z)+ (z-\mathbb{E}[X]) \times l.$$

Si l'on prend maintenant au début du raisonnement que $z=\mathbb{E}[X]$, on obtient bien que 
$$\mathbb{E}[f(X)] \geq  f(\mathbb{E}[X]).$$
```
::::


### Inégalité d'Hölder

Une autre application théorique des fonctions convexes est l'inégalité d'Hölder dans le cadre probabiliste :

::::{prf:proposition}
Soit $(\Omega, \mathcal{T},\mathbb{P})$ un espace probabilisé.

Soit $(p,q,r) \in ]0,+\infty]$ tels que$\frac{1}{p}+\frac{1}{q}=\frac{1}{r}$.

Alors pour toutes variables X et Y tels que $X^p$ et $Y^q$ soient intégrables, $|XY|^r$ admet une espérance finie, et de plus :

$$\mathbb{E}\left[|XY|^r\right]^\frac{1}{r}\leq \mathbb{E}\left[|X|^p\right]^\frac{1}{p} \times \mathbb{E}\left[|Y|^q\right]^\frac{1}{q}$$

```{prf:proof}
La fonction $-\ln$ est une fonction convexe, donc pour $u,v \in \R^+$, l'on a que 

$$-\ln(\frac{r}{p}u^\frac{p}{r} +\frac{r}{q}v^\frac{q}{r}) \leq -\frac{r}{p}\ln(u^\frac{p}{r}) - \frac{r}{q}\ln(v^\frac{q}{r}) = -\ln(u) - \ln(v).$$

C'est-à-dire que $ uv\leq \frac{r}{p}u^\frac{p}{r} +\frac{r}{q}v^\frac{q}{r}$.

Supposons tout d'abord que $\mathbb{E}\left[|X|^p\right]=\mathbb{E}\left[|Y|^q\right] =1 $

On applique alors l'inégalité précédente à $|X|^r$ et $|Y|^r$ pour obtenir que 

$$|XY|^r \leq \frac{r}{p}|X|^p +\frac{r}{q}|Y|^q.$$

Mais alors en intégrant, l'on obtient bien que 

$$\mathbb{E}(|XY|^r ) \leq  \frac{r}{p} \mathbb{E}(|X|^p) +\frac{r}{q}\mathbb{E}(|Y|^q) =\frac{r}{p}+\frac{r}{q} =1 =  \mathbb{E}\left[|X|^p\right]\times \mathbb{E}\left[|Y|^q\right]$$

Maintenant, pour le cadre général, il suffit de se rendre compte que si $X\neq 0$ et $Y\neq 0$, 

$$\mathbb{E}\left[\left|\frac{X}{\mathbb{E}\left[|X|^p\right]^{\frac{1}{p}}}\right|^p\right]=1 = \mathbb{E}\left[\left|\frac{Y}{\mathbb{E}\left[|Y|^q\right]^{\frac{1}{q}}}\right|^q\right].$$

```

::::