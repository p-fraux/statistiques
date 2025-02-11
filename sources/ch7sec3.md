(Chol)=
## Compléments d'algèbre linéaire
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\C}{\mathbb{C}}$
$\newcommand{\N}{\mathbb{N}}$
$\newcommand{\K}{\mathbb{K}}$

:::{prf:theorem} Factorisation de Cholesky

Soit $K\in S_n^{+}$ une matrice symétrique semi-définie positive.

Alors il existe une matrice de permutation $P \in M_{n,n}$ et une matrice triangulaire inférieur $L\in T_n$ à coefficients diagonaux positifs tels que :

$$PKP^t=L\times L^t$$

Si K est défini positive, alors on peut prendre $P=I_n$ et alors L est unique.

:::

Nous ne traiterons que le cas  défini positif, le cas général pouvant s'en déduire en utilisant que pour une matrice symétrique, $Ker(A)=Im(A)^\bot$ pour le produit scalaire (hermitien) canonique de $\R^n$ ($\C^n$). Nous ne montrerons pas l'unicité de la décomposition, qui sera laissé au lecteur.

Nous allons faire une démonstration en construisant un algorithme, et nous aurons pour cela besoin de la proposition matricielle suivante :

::::{prf:proposition}
:class: dropdown
Soit  $K\in S_n^{++}$ une matrice symétrique définie positive écrite par bloc de la forme :

$$ K := \begin{pmatrix}A&B^t\\B&W\end{pmatrix}$$

Alors A est définie positive, donc inversible, et le complément de Schur de A dans la matrice K définie comme la matrice 

$$W-BA^{-1}B^t$$

est défini positif.

```{prf:proof}
Le caractère défini positif de A est immédiat avec la caractérisation 
    
$$A \text{ est défini positif} \iff \forall X\in \K^n, \vec{X}^tA\vec{X}\geq 0$$ 

Maintenant, supposons par l'absurde que le complément de Schur de A dans K n'est pas défini positif, il existe donc $\vec{u}$ non nul tel que 

$$\vec{u}^t(W-BA^{-1}B^t)\vec{u}\leq 0$$

On pose alors le vecteur non nul 

$$\vec{v}=\begin{pmatrix}
        -A^{-1}B^t \vec{u}\\\vec{u}
    \end{pmatrix}$$

qui vérifie bien 

$$ \vec{v}^tW\vec{v}=\vec{u}^t(W-BA^{-1}B^t)\vec{u} \leq 0$$

Ce qui contredit le fait que K est défini positif.

```
::::

::::{prf:algorithm} Décomposition de Cholesky (version recursive)
:label: décomposition_Cholesky

**Entrée** $K\in S_n^{++}$ une matrice symétrique définie positive

**Sortie** Une matrice de permutation $P \in M_{n,n}$ et une matrice triangulaire inférieur $L\in T_n$ à coefficients diagonaux positifs tels que :

$$PKP^t=L\times L^t$$


1. **Cas de base** $n=1$, l'existence d'une telle décomposition est immédiate.
2. **Cas récursif** Choisir $1\leq k\leq n$. 

	Ecrire K de la forme
    
    $$K=\begin{pmatrix}A&B^t\\B&W\end{pmatrix}$$
    avec $A\in M_{k,k}$

	1. Trouver $(L_1, L_2)\in T_n^2$ deux matrices triangulaires inférieures à coefficients diagonaux positifs tels que $A=L_1L_1^t$ et $W-BA^{-1}B^t=L_2L_2^t $
	2. Renvoyer la matrice 
    
    $$L=\begin{pmatrix}L_1&0\\B(L_1^t)^{-1}&L_2\end{pmatrix}$$

::::


:::{prf:remark}

Si l'on suit l'algorithme, la décomposition de Cholesky est facile à calculer. On peut montrer que la complexité de l'algorithme est de l'ordre de $n^3$.
:::



On préfère parfois trouver une racine carrée de la matrice K, c'est-à-dire une matrice A, qui commute avec K, telle que 

$$K=A^2.$$

De plus, l'on veut parfois trouver une matrice de plus petite dimension "proche" de la matrice originelle pour accélérer les calculs en statistique de grande dimension. Pour le lecteur intéressé, nous renvoyons alors à la décomposition spectrale et la décomposition en valeur singulière. L'on pourra par exemple lire :

```{admonition} Analyse matricielle (Partie théorique)
:class: hint, dropdown
Pour tous les résultats théoriques de l'analyse matricielle, {cite:ps}`MatrixAnalysis`.
```

```{admonition} Regression linéaire (Applications au statistiques)
:class: hint, dropdown
Pour des méthodes algorithmiques de régression le long des valeurs principale, pour des régressions mal posées.

```
