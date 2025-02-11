(inverse-generalise)=
##   Inverse généralisé de fonction de répartition
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

 Soit F une fonction de répartition, donc croissante et continue à droite. On cherche ici à inverser la fonction du mieux possible. Malheureusement, la fonction F n'est pas nécessairement injective. Pour certaines valeurs, nous aurons donc plusieurs choix d'inverses possibles. Mais tous ces choix ne se valent pas, et il y a un choix préférentiel : l'inverse généralisé.
Il s'agit de la fonction $F^{\leftarrow} : s \mapsto \inf \{x,\ F(x)\geq s\}$

:::{prf:proposition} 
$F^{\leftarrow}$ est croissante, continue à gauche et vérifie pour tout u que :

$$F(F^{\leftarrow}(y))\geq y $$

$$\{t, F(t)\geq u\} = \{t, t\geq F^{\leftarrow}(u)\}$$

```{prf:proof}
- Soit $u<v$, comme $ \{x,\ F(x)\geq v\}\subset \{x,\ F(x)\geq u\}$, on obtient directement que $F^{\leftarrow}$ est croissante.

- Soit $(s_n)$ une suite croissante et convergente vers $s\in \R$. La fonction $F^{\leftarrow} $ étant croissante, $F^{\leftarrow}(s_n)$ converge vers un $l$. Montrons que $l=F^{\leftarrow}(s)$.

Par croissance de $F^{\leftarrow}$, on a que $l\leq F^{\leftarrow}(s)$. Soit $m< F^{\leftarrow}(s)$, alors il existe $x_O\geq m$ tel que $F(x_0) <s$. Par convergence, il existe un rang n tel qu'à partir de ce rang, $s_n > F(x_0)$, et donc par croissance de F que $F^{\leftarrow}(s_n)\geq x_0\geq m$.

En particulier, à la limite, $l\geq m$. Puis en faisant tendre m vers $F^{\leftarrow}(s)$, l'on en déduit que $l \geq F^{\leftarrow}(s)$.

- Il existe une suite $(x_n)$ qui converge par valeur supérieure vers $F^\leftarrow(y)$ tels que $F(x_n)\geq y$. Comme F est continu à droite, on en déduit que $F(F^\leftarrow(y)) \geq y$

- Procédons par double inclusion : 

Soit t tel que $F(t)\geq u$. Alors par définition, \mbox{$ F^{\leftarrow}(u)= inf (x,\ F(x)\geq u)\geq t$.}

Soit maintenant t tel que $F(t)<u$. Comme F est continu à droite, il existe $t_0>t$ tel que $F(t_0)<u$, et donc nous en déduisons par croissance de F que $F^{\leftarrow}(u)\geq t_0>t$.

```
:::





Dans le cadre particulier des statistiques, on appelle également l'inverse généralisé d'une fonction de répartition la fonction quantile de la variable aléatoire.

:::{prf:example}
Pour $X$ une variable aléatoire, la médiane est la valeur t telle que la probabilité que $X$ lui soit inférieur est de $\frac{1}{2}$. C'est donc  $F^{\leftarrow}(\frac{1}{2})$.
:::

La fonction quantile n'a pas qu'un intérêt théorique. En effet, le lemme suivant nous dit qu'elle permet de simuler très facilement n'importe quelle variable aléatoire.


:::{prf:lemma} de transformation des quantiles
Soit $U : (\Omega, \mathcal{T}, \mathbb{P}) \to ([0, 1], \mathcal{B}[0, 1])$ une variable aléatoire de loi uniforme sur [0, 1]. Soit $F : \R \to[0, 1]$ une fonction de répartition. Alors la variable aléatoire $X:= F^{\leftarrow}\circ U :
(\Omega, \mathcal{T}, \mathbb{P})\to (\R, \mathcal{B}(\R))$ est une variable aléatoire de fonction de répartition F.

```{prf:proof} 
Soit $U$ et $F$ comme dans l'énoncé, et soit $t\in \R$, alors avec la proposition précédente, et comme nous connaissons la fonction de répartition d'une loi uniforme, 

$$\mathbb{P}(F^{\leftarrow}\circ U \leq t)=\mathbb{P}( U \leq F(t)) = F(t)$$

:::

    








