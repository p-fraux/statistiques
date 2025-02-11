## Statistique de test du $\chi^2$

$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

On souhaite vérifier que la loi (donnée par sa fonction de répartition $F$) de $X$ est  égale à une certaine loi $F_0$ donnée (donc parfaitement connue). C'est-à-dire l'on souhaite tester 

$$H_0 : F=F_0 \qquad \text{ contre } \qquad H_1 : F\neq F_0.$$

Ce genre de test s’appellent des _test d’ajustement_.

Un des tests les plus utilisé en pratique est le test du $\chi^2$, dont nous allons décrire la loi de la statistique.

### Ajustement à une loi connue




Donnons-nous $l\in \N^*$ et une partition de $\R$ en classe $(C_1,...,C_l)$. L'on se donne $Z$ qui suit la loi $F_0$ et l'on pose 

$$p_k:=\mathbb{P}(Z \in C_k).$$

Posons également les variables aléatoires $U_i^{(k)} := {1}_{C_k}(X_i)$ et $W^{(k)} := \sum_{i=1}^n U_i^{(k)}$.

Enfin, posons la statistique de test 

$$ T_n= \sum_{k=1}^l \frac{(W^{(k)}-np_k)^2}{n p_k}$$

::::{prf:theorem} Loi asymptotique de $T_n$
:class: dropdown
```{prf:remark} Intuition derriere le théoreme
:class: dropdown
Sous $H_0$, $U_i^{(k)}$ suit une loi de Bernoulli de paramètre $p_k$ et $W^{(k)}$ suit une loi Binomiale de  paramètre $\mathcal{B}in(n,p_k)$ (elle représente le nombre de réalisations présente dans la classe $C_k$).

En particulier, l'on connait son espérance et sa variance : $\mathbb{E}(W^{(k)})=np_k$ et $V(W^{(k)})=np_k(1-p_k)$.


L'on sait alors avec le théorème central limite que 

$$\frac{W^{(k)}-np_k}{\sqrt{np_k(1-p_k)}} \overset{Loi}{\to} \mathcal{N}(0,1)$$
L'on peut donc raisonnablement supposer que la variable 

$$ T=\sum_{k=1}^l \frac{(W^{(k)}-np_k)^2}{n c_k} $$
soit, à des constantes $c_k$ près, une variable aléatoire suivant une loi du $\chi^2$. Comme chacune des variables ne sont pas indépendantes, il faut néanmoins faire attention (en particulier les constantes ne seront pas $\sqrt{p_k(1-p_k}$). 
```

Sous l'hypothèse $H_0$, la suite de variables aléatoire suivante converge en loi vers une loi du $\chi^2$ à $l-1$ degré de liberté :

$$ T_n= \sum_{k=1}^l \frac{(W^{(k)}-np_k)^2}{n p_k} \overset{Loi}{\to} \chi^2_{l-1}$$

```{prf:proof}
Nous allons utiliser une généralisation du théorème {ref}`loirapportvraissemblance` à la statistique de test du rapport de vraisemblance pour un paramètre dans $\R^n$, qui dit que dans ce cas, le logarithme du maximum du rapport de vraisemblance converge en loi vers une $\chi^2$ à n degré de liberté.


La vraisemblance d'un tirage sous la loi $F_0$ (avec $p_l=1-\sum_{k<l}p_k$ ) est alors 

$$ f_{p_1,...,p_l}(n_1,...,n_l) = C \prod_{k=1}^l p_k^{n_k}$$

On peut alors facilement montrer que l'estimateur de maximum de vraisemblance des valeurs $p_i$ est $\hat{p_i}=\frac{n_i}{n}$.

La statistique de rapport des maximums de vraisemblance est alors

$$-2\ln(\Lambda_n):=\frac{f_{p_1,...,p_l}(n_1,...,n_l)}{f_{\hat{p_1},...,\hat{p_{l-1}},}(n_1,...,n_l)}= n^n\prod_{k=1}^l \left(\frac{p_k}{n_k}\right)^{n_k} $$

D'où comme $-2\ln(\Lambda_n) = \sum_{k=1}^{l} 2 n_i \ln(\frac{n_k}{n p_k}) $, l'on aura avec nous $l-1$ degrés de liberté (puisque $\sum p_k=1$) que :

$$\sum_{k=1}^{l} 2 n_k \ln(\frac{n_k}{n p_k}) \overset{loi}{\to} \chi^2_{l-1}.$$

Mais le membre de gauche n'est pas exactement notre statistique. Posons $\Delta_i=\frac{n_i-np_i}{np_i}$ et réécrivons notre expression :
    
$$-2\ln(\Lambda_n)=2 \sum_{k=1}^{l}  n_k \ln(\frac{n_k}{n p_k}), $$
$$=2\sum_{k=1}^{l} (n_k - np_k + np_k) \ln(1+ \Delta_k),$$
$$=2\sum_{k=1}^{l} \left[(n_k - np_k) + np_k)\right] (\Delta_k- \frac{1}{2} \Delta_k^2 + O(\Delta^3),$$
$$=2\sum_{k=1}^{l} (n_k - np_k)\Delta_k + np_k \Delta_k - \frac{np_k}{2} \Delta_k^2 + O(n\Delta^3),$$

Or maintenant, comme $\sum_{k=1}^{l}np_k \Delta_k = \sum_{k=1}^{l} n_i - np_i = n-n=0  $ et comme $(n_k - np_k)=np_k \Delta_k$, l'on a que :

$$ -2\ln(\Lambda_n) = \sum_{k=1}^{l} np_k\Delta_k^2 +O(n\Delta^3) $$

Enfin, avec la loi forte des grands nombres, $\sqrt{n}\Delta_k$ converge en loi vers une loi normale, donc avec le lemme de Slusky et une composition avec une application continue, 

$$\frac{n}{\sqrt{n}^3}\cdot (\sqrt{n}\Delta_k)^3 =\frac{}{\sqrt{n}}\cdot (\sqrt{n}\Delta_k)^3   $$ 

converge en loi vers 0, donc en probabilité vers 0. L'on a bien alors que la statistique $ T_n$ à la même loi asymptotique que la statistique de rapport des maximums de vraisemblance.
    
```

```{prf:remark} Preuve alternative
:class: dropdown
L'on peut remarquer que $T_n$ est en fait la norme du vecteur $(\frac{n_k-np_k}{\sqrt{np_k}})_{k \in \{1,...,l\}}$. Or l'on peut montrer que ce vecteur est de matrice de covariance :

$$ Cov(\frac{n_k-np_k}{\sqrt{np_k}}) = Id_{l}-
\begin{pmatrix}
    \sqrt{p_1}\\\vdots\\ \sqrt{p_l}
\end{pmatrix}\times \begin{pmatrix}
    \sqrt{p_1}&\cdots& \sqrt{p_l}
\end{pmatrix}:= \Gamma(F_0)$$

Qui est la matrice de projection sur l'orthogonal de l'espace engendré par $\begin{pmatrix}
    \sqrt{p_1}\\\vdots\\ \sqrt{p_l}
\end{pmatrix}$.

Comme avec le théorème central limite, nous avons la convergence en loi vectorielle

$$\frac{n_k-np_k}{\sqrt{np_k}} \to \mathcal{N}(0,\Gamma(F_0))$$

le théorème de Cochran permet de conclure sur la loi asymptotique de $T_n$.
```

::::



Cette loi asymptotique permet encore une fois de créer un test, portant sur notre hypothèse $H_0$.

::::{prf:definition}
Soit $F_0$ une loi, $(C_i)$ une partition de $\R$ en classes, et $T $ défini comme ci-dessus.

Si l'on se donne $\alpha$ un risque de première espèce, et $s_\alpha$ le quantile d'ordre $1-\alpha$ d'une loi du $\chi^2_{l-1}$, 

Alors le test 

$$\text{On rejette }H_0 \text{ si }\ T>s_\alpha \qquad  \text{On ne rejette pas }H_0 \text{ si }\ T\leq s_\alpha$$

est un test de niveau asymptotique $\alpha$.
::::

```{figure} test_chi_2.png
---
height: 400px
name: fig:testchi2
---
Illustration du test du $\chi^2$ avec l = 50 classes
```



```{prf:remark}
:class: dropdown
 La densité d'une loi du $\chi^2_{l-1}$ à $l-1$ degré de liberté a pour densité 
 
 $$ f_{\chi^2_{l-1}}(x)=x\mapsto \frac{x^{\frac{1}{2}(k-2)}e^{-\frac{x}{2}}}{2^{\frac{k}{2}}\Gamma(\frac{k}{2})}{1}_{\R^+}(x).$$
 

Lors de calculs explicite, l'on préfèrera se rapporter à une table des valeurs de la fonction de répartition plutôt qu'un calcul d'intégral numérique pour trouver le quantile d'ordre $1-\alpha$. 
```


### Comment choisir les classes $C_1, ... ,C_l$ ?

Il est d'usage de demander que le nombre moyen
d’observations par classe $np_k$ soit supérieur à 5 pour toutes les classes, _i.e._

$$ \min\limits_{k\in \{1,...,l\}}np_k > 5.$$

Pour faciliter cela, on détermine des classes $C_k$ de manière à avoir 

$$p_k\approx\frac{1}{l}.$$

Pour des raisons de simplicité, lorsque le test est effectué à la main, on choisit un nombre de classes faible : $l=3, 4$ ou $5$. Dans le cas d’une loi $F_0$ ayant une symétrique par rapport à sa moyenne, on pourra profiter de la symétrie pour avoir l’équiprobabilité en prenant $l$ pair (par exemple l=4).

### Que faire si les paramètres définissant $F_0$ ne sont pas connus ?

Il arrive bien souvent que seule la forme de la loi $F_0$ soit connue via la modélisation (loi de Poisson, normale…), mais que l'on ignore certains paramètres. L'on pourra alors estimer à l’aide de l'échantillon ces paramètres. 

::::{prf:theorem} Loi de la statistique avec estimation de paramètres
Soit $m \in \N^*$ un entier et $F_0(\theta_1, \cdots, \theta_m)$ une famille de loi. Si l'on note $(\hat{\theta_i})$  l’estimateur de maximum de vraisemblance des paramètres de la loi, $\hat{p_k} = \mathbb{P}_{F_0(\hat{\theta_1}, \cdots, \hat{\theta_m})}(X\in C_k)$ et $n_k$ le nombre de résultats présent dans la classe $C_k$, alors
    
$$T_n := \sum_{k=1}^l \frac{(n_k-n\hat{p_k})^2}{n \hat{p_k}} \overset{Loi}{\to} \chi^2_{l-m-1}$$

```{prf:proof} 
Voir {cite}`advanced-stats` points 30.11 à 30.19.

Une autre preuve possible est d'estimer plus finement le maximum de vraisemblance avec l'information de Fisher et le gradient de la Log-vraisemblance, avant d'étudier le comportement asymptotique de couple $(T_n,\hat{\theta})$ puis de conclure avec le théorème de Cochran.
```

::::

Ainsi, on réduira le nombre de degrés de liberté de la loi du $\chi^2$ utilisée pour le test d’ajustement selon le
nombre de paramètres estimés $m$.