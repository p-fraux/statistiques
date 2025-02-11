$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

## Convergence supplémentaire

(Slutsky)=
### Lemme de Slutsky et Scheffé

:::{prf:lemma} Slutsky et Scheffé
Soit $ X_n \overset{\mathbb{P}}{\to} c \in \R$ et $Y_n\overset{\mathcal{L}oi}{\to} Y$ deux suites de variable aléatoire, l'une convergente en loi vers une constante et l'autre convergente en loi.

Alors le couple $(X_n,Y_n)$ converge en loi vers $(X,Y)$ et en particulier le produit des deux suites converge en loi vers le produit des limites :

$$X_nY_n\overset{\mathcal{L}oi}{\to}cY$$

```{prf:proof}
Quitte à remplacer $X_n$ par $X_n-c$, on peut supposer que $X_n$ converge en probabilité (et donc en loi comme la limite est constante) vers 0. Montrons alors la convergence en loi du couple $(X_n, Y_n) $ vers $(0,Y)$ en utilisant la caractérisation de Paul Lévy par les fonctions caractéristiques :

$$|\varphi_{(X_n,Y_n)}(s,t)-\varphi_{(0,Y)}(s,t)|\leq |\varphi_{(X_n,Y_n)}(s,t)-\varphi_{(0,Y_n)}(s,t)|+|\varphi_{(0,Y_n)}(s,t)-\varphi_{(0,Y)}(s,t)| $$

Par convergence en loi, $|\varphi_{(0,Y_n)}(s,t)-\varphi_{(0,Y)}(s,t)|=|\varphi_{Y_n}(t)-\varphi_{Y}(t)| \underset{t\to 0}{\to}0$.

Maintenant, $|\varphi_{(X_n,Y_n)}(s,t)-\varphi_{(0,Y_n)}(s,t)|= |\mathbb{E}(e^{isX_n+itY_n}-e^{itY_n})| \leq \mathbb{E}(|e^{isX_n}-1|)$,

Comme l'exponentielle est continue en 0, pour $\epsilon>0$, il existe $\delta>0$ tel que si $|x|\leq \delta$, alors $|e^{itx}-1|\leq \epsilon$. Donc 

$$\mathbb{E}(|e^{isX_n}-1|) = \mathbb{E}(|e^{isX_n}-1|{1}_{|X_n|\leq \delta})+ \mathbb{E}(|e^{isX_n}-1|{1}_{|X_n|> \delta})$$
$$\leq \epsilon +2 \mathbb{P}(|X_n|> \delta)$$

Et comme la convergence en loi implique la convergence en probabilité, on en déduit la convergence simple des fonctions caractéristiques, et donc la convergence en loi du couple. Enfin, le produit est une fonction continue, donc on a bien la convergence en loi annoncée.
```

:::

    
