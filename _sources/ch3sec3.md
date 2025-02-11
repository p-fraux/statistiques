## Test paramétrique simple
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

Rappellons que nous somme dans le cadre d'un modèle dominé (voir {ref}`dominee`}).

Il existe donc une mesure $\nu$ et une fonction $L : \Omega\times \Theta \to \R_+$ telle que toute loi $\mathbb{P}_\theta$ soit absolument continue par rapport à $\nu$ et de densité $L(\cdot,\theta)$.

Sur cette page, nous allons tester une hypothèse nulle simple contre une hypothèse alternative simple :

$$ H_0 : \theta=\theta_0 \qquad \text{ contre } \qquad H_1 : \theta= \theta_1.$$


:::{prf:theorem} Test de Neyman-Pearson
:class: dropdown
Pour $\alpha$ fixé, il existe un test de la statistique "rapport de vraisemblance", éventuellement randomisé de niveau exactement $\alpha$. Il consiste à comparer le rapport de vraisemblance à un seuil $\tau_\alpha$ (que l'on calcule sans regarder les données pour assurer le niveau) :



- Si $\frac{L(\mathbf{X},\theta_1)}{L(\mathbf{X},\theta_0)}>\tau_\alpha$, alors on rejette $H_0$   
- Si $\frac{L(\mathbf{X},\theta_1)}{L(\mathbf{X},\theta_0)}<\tau_\alpha$, alors on ne rejette pas $H_0$   
- Enfin, si $\frac{L(\mathbf{X},\theta_1)}{L(\mathbf{X},\theta_0)}=\tau_\alpha$, on choisit de rejeter ou de ne pas rejeter suivant le résultat d'un tirage d'une loi uniforme.



De plus, ce test est le plus puissant sous l'hypothèse alternative parmi tous les tests de niveau inférieur ou égal à $\alpha$.

On appelle ce test  _le test de Neyman-Pearson_, ou _test du rapport des vraisemblances_.

::::{prf:proof}
On note $G$ la fonction de répartition du rapport de vraisemblance sous $\mathbb{P}_{\theta_0}$, c'est-à-dire

$$G: t\mapsto \mathbb{P}_{\theta_0}\left(\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}\leq t\right) $$

Et on note $G^{\leftarrow}$ la fonction quantile associé (voir {ref}`inverse-generalise`) :

$$ G^{\leftarrow}(p) = \inf\{x : G(x)\geq p\}.$$

Posons alors comme seuil $\tau_\alpha := G^\leftarrow(1-\alpha)$.

On a alors 

$$\mathbb{P}_{\theta_0}\left(\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}> \tau_\alpha\right)= 1-G(\tau_\alpha) \leq \alpha $$

Car l'inverse généralisé vérifie $G(G^\leftarrow(1-\alpha))\geq 1-\alpha$.

Maintenant, si $G(\tau_\alpha)>1-\alpha$, on sait que 

$$\mathbb{P}_{\theta_0}\left(\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}= \tau_\alpha\right)= G(\tau_\alpha)-G(\tau_\alpha^-)$$

On considère alors $U$ une variable aléatoire uniforme sur[0,1] indépendante des mesures.

Si l'on prend alors le test qui rejette $H_0$ si $\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}>\tau_\alpha$ ou si $U \leq \frac{G(\tau_\alpha)-(1-\alpha)}{G(\tau_\alpha)-G(\tau_\alpha^-)}$ alors ce test (randomisé) est de niveau exactement $\alpha$. On le note T pour la suite.

Montrons à présent que ce test est le plus puissant parmi les tests de niveau inférieur à $alpha$. Prenons la convention qu'un test est une application qui vaut 1 si l'on rejette $H_0$ et 0 sinon, et considérons $T'$ au autre test de niveau inférieur à $\alpha$. Alors, avec $\nu$ la mesure dominante, l'on a 

$$\mathbb{P}_{\theta_1}(T=1)-\mathbb{P}_{\theta_1}(T=1)= \mathbb{E}_{\theta_1}(T-T')$$
$$=\int (T-T') f(x,\theta_1)d\nu(x)= \int (T-T')\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)} f(x,\theta_0)d\nu(x) +\int (T-T')1_{f(x,\theta_0)=0} f(x,\theta_1)d\nu(x)$$

Or sur l'événement $f(x,\theta_0)=0$, le rapport de vraisemblance est infini, et donc $T=1$ et donc $T-T'\geq 0$. Ceci donne

$$ \mathbb{P}_{\theta_1}(T=1)-\mathbb{P}_{\theta_1}(T=1)\geq \mathbb{E}_{\theta_1}\left[(T-T')\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}\right]$$
$$ \geq \mathbb{E}_{\theta_0}\left[(T-T')\left(\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}-\tau_\alpha\right)\right] + \tau_\alpha\mathbb{E}_{\theta_0}\left[(T-T')\right]$$
$$\geq \mathbb{E}_{\theta_0}\left[(T-T')\left(\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}-\tau_\alpha\right)\right] $$

Car $\mathbb{E}_{\theta_0}\left[(T_i)\right] = \mathbb{P}_{\theta_0}(T=1)$  est le niveau du test i, qui vaut $\alpha$.

Donc $\mathbb{P}_{\theta_1}(T=1)-\mathbb{P}_{\theta_1}(T=1)\geq 0 $ car $(T-T')\left(\frac{f(\mathbf{X},\theta_1)}{f(\mathbf{X},\theta_0)}-\tau_\alpha\right)\geq 0$.

Qui nous donne bien que la puissance sous l'alternative est maximale.
::::

:::


:::{admonition} Méthodologie :
:class: tip
Ce résultat théorique permet de construire concrètement un test uniformément le plus puissant parmi les tests de niveau donné. Pour cela, on part de l’inégalité du théorème puis, par équivalences successives, on aboutit à une statistique de test et à la règle de décision correspondante. En général, il n'y a pas besoin de connaître la valeur de $\tau_\alpha$, on préférera la calculer lorsqu'il faut donner la règle de décision (après transformation par équivalence pour simplifier la statistique).
:::


```{exercise}
:label: exer13
Nous considérons des variables aléatoires indépendantes $X_1,...,X_n$ de même loi $\mathcal{N}(0,\frac{1}{\lambda^2})$.

Nous voulons choisir entre deux hypothèse :

$$H_0  : \lambda=1 \qquad \text{ contre } \quad H_1 : \lambda=\lambda_1<1.$$

a) Construire le test de Neyman-Pearson.
:::{admonition} Solution a)
:class: dropdown
Raisonnons par équivalence (sur la partie du test non randomisé) pour trouver une statistique de test à partir du rapport des vraisemblances :

$$\frac{f(x_1,...,x_n,1)}{f(x_1,...,x_n,\lambda_1)}>C_\alpha \iff \frac{1}{\lambda_1^n}e^{-\frac{((1-\lambda_1^2)}{2}\sum_{i=1}^n x_i^2}>C_\alpha $$

En prenant le logarithme, qui est une fonction croissante, on a :

$$\frac{f(x_1,...,x_n,1)}{f(x_1,...,x_n,\lambda_1)}>C_\alpha\iff -n\ln(\lambda_1) - \frac{(1-\lambda_1^2)}{2}\sum_{i=1}^n x_i^2  > \ln(C_\alpha)$$

Et comme $- \frac{(1-\lambda_1^2)}{2}<0$),

$$\frac{f(x_1,...,x_n,1)}{f(x_1,...,x_n,\lambda_1)}>C_\alpha\iff \sum_{i=1}^n x_i^2 < \frac{2}{1-\lambda_1^2}(-n\ln(\lambda_1)-\ln(C_\alpha))$$

Nous prenons alors comme statistique 
        
$$Y=\sum_{i=1}^n x_i^2 $$

Et comme le test de Neyman-Pearson rejette $H_0$ lorsque le rapport des vraisemblances est supérieur à $C_\alpha$, nous rejetterons lorsque $Y<\mu_{\alpha}$.
        
$$\left\{ \begin{matrix}
            si & Y<\mu_{\alpha} & \text{ on rejette }H_0\\
            si &Y>\mu_{\alpha} & \text{ on ne peut pas rejetter }H_0
        \end{matrix}\right.$$

où $\mu_{\alpha}$ est le quantile d'ordre $\alpha$ d'une loi $\chi^2_n$
:::

b) On désire calculer l'erreur de seconde espèce pour le test de niveau $\alpha=5\%$ issus de $n=30$ réalisation, et une alternative $\lambda_1=0.9$. Donner la formule générale de cette erreur et sa valeur numérique.

:::{admonition} Solution b)
:class: dropdown
Pour $n=30$ et $\alpha=5\%$, on trouve avec la table {ref}`fig:Chi-Square-table` $\mu_\alpha = 18.493$.

Or, sous $H_1$, $Y\times \lambda_1^2= \sum_{i=1}^n \frac{x_i^2}{1/\lambda_1^2} \sim \chi^2_n$.

Donc 

$$\mathbb{P}(\text{Accepter }H_0 | H_1 \text{ vrai})=\mathbb{P}(Y > \mu_\alpha| H_1 \text{ vrai}) = \mathbb{P}(Y\lambda_1^2 > \mu_\alpha\lambda_1^2| H_1 \text{ vrai}) $$

De nouveau avec la table, l'on trouve que pour $Z\sim \chi^2_{30}$ 

$$\mathbb{P}(Z>\mu_\alpha\times \lambda_1^2) =\mathbb{P}(Z>14.979)=0.01$$

Donc nous aurons une erreur de seconde espèce de 1\%.
:::
```



```{exercise}
:label: exer14
Soit $a\geq0$ connu, et soient $X_1,...,X_n$ des variables aléatoires indépendantes. La loi de $X_j$ est $\mathcal{N}(m,j^{2a})$.

On souhaite choisir entre $H_0 : m=0$ et $H_1 : m=2$ à partir des observations des $X_j$.

Construire le test de Neymann-Pearson associé pour un risque $\alpha=0.05$.

Que dire de la zone de rejet pour $a>\frac{1}{2}$ et n grand ?

:::{admonition} Solution 
:class: dropdown
La zone de rejet est de la forme 

$$\tau_\alpha <\frac{f (\mathbf{X},m=0)}{f (\mathbf{X},m=2)}.$$

Nous pouvons réécrire cela comme :

$$\tau_\alpha <\frac{f (\mathbf{X},m=0)}{f (\mathbf{X},m=2)}\iff \tau_\alpha <\prod_{j=1}^n e^{-\frac{x_j^2}{2 j^{2a}}+\frac{(x_j-2)^2}{2 j^{2a}} }$$
$$\iff \ln(\tau_\alpha)< \sum_{j=1}^n -\frac{x_j^2}{2 j^{2a}}+\frac{(x_j-2)^2}{2 j^{2a}}$$
$$\iff \ln(\tau_\alpha)< \sum_{j=1}^n \frac{-4x_j+4}{2j^{2a}}$$
 $$\iff C_\alpha >\sum_{j=1}^n\frac{x_j}{j^{2a}}$$
 
Or la variable 

$$\sum_{j=1}^n\frac{x_j}{j^{2a}}\sim \mathcal{N}(m\sum_{j=1}^n \frac{1}{j^{2a}} ; \sum_{j=1}^n \frac{1}{j^{2a}}).$$

Donc $C_\alpha = 1.65\times \frac{1}{\sqrt{\sum_{j=1}^n \frac{1}{j^{2a}}}}$.

En particulier, pour $a>\frac{1}{2}$, nous avons
$C_\alpha \underset{n \to +\infty}{\to} \frac{1.65}{\sqrt{\zeta(2a)}}.$ et donc la zone de rejet "converge" vers une zone limite.
:::
```

