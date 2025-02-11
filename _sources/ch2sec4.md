## Amélioration théorique d'estimateurs (HP)
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

### Statistique exhaustive
:::{prf:definition} Statistique exhaustive

Considérons un modèle paramétré. Nous dirons qu'une statistique $S$ est _exhaustive_ si la loi conditionnelle de l'échantillon sachant la statistique est libre du paramètre :

$$\mathbb{P}_\theta(X\in A| S,\theta) =\mathbb{P}(X\in A| S)$$

::::{prf:remark}
D'un point de vue purement pratique, si S est une statistique exhaustive, le rapport des vraisemblances peut s'écrire comme une fonction uniquement de S.

::::

Si le modèle est dominé et paramétré, et nous notons $f_\theta$ la densité de la loi $\mathbb{P}_\theta$, alors S est une statistique exhaustive si et seulement si il existe h et g deux applications mesurables telles que 

$$\forall (x,\theta) \in \mathcal{X}\times \Theta, f_\theta(x)= h(x)g(S(x),\theta).$$

:::

::::{prf:example}
Considérons $(X_i)$ la répétition de loi de Poisson $\mathcal{P}(\lambda)$ indépendantes. Alors, nous pouvons réécrire la vraisemblance comme :

$$f(k_1,...,k_n,\lambda)=\mathbb{P}_\lambda (X_1=k_1,...,X_n=k_n) = \prod_{i=1}^n e^{-\lambda}\frac{\lambda^{k_i}}{k_i !} = e^{-n\lambda} \lambda^{\sum_{i=1}^nk_i} \cdot \prod_{i=1}^n\frac{1}{k_i!}. $$

En particulier, $S=\sum_{i=1}^n k_i$ est une statistique exhaustive

::::

::::{prf:theorem} Rao-Blackwell
Soit un modèle paramétrique et S une statistique exhaustive. Alors, pour tout estimateur T sans biais, l'estimateur

$$E=\mathbb{E}(T|S)$$

est (sans biais et) de variance inférieure à T.

::::

::::{prf:example}
Considérons la répétition de lois de Poisson $\mathcal{P}(\lambda)$ indépendantes, et la statistique exhaustive $S=\sum_{i=1}^n X_i$.

Prenons comme estimateur de $e^{-\lambda}$ la statistique (douteuse) $T_1=\delta_{0=X_1}$ à valeur dans $\{0,1\}$, et appliquons-lui le théorème.

D'abord, $T_1$ est bien sans biais car $\mathbb{E}(T_1)=\mathbb{P}(X_1=0)=e^{-\lambda}$. L'estimateur suivant est donc plus efficace

$$T_2:=\mathbb{E}(T_1|S).$$

Calculons le :

$$T_2(k_1,...,k_n)=\mathbb{E}(T_1|S)(k_1,...,k_n)$$
$$=1\times\mathbb{P}\left(X_1=0|\sum_{i=1}^n X_i =\sum_{i=1}^n k_i\right) + 0\times\mathbb{P}\left(X_1\neq 0|\sum_{i=1}^n X_i =\sum_{i=1}^n k_i\right) $$
$$= \frac{\mathbb{P}(X_1=0,\sum_{i=1}^n X_i =\sum_{i=1}^n k_i)}{\mathbb{P}(\sum_{i=1}^n X_i =\sum_{i=1}^n k_i)}$$
$$=\frac{\mathbb{P}(X_1=0)\mathbb{P}(\sum_{i=2}^n X_i =\sum_{i=1}^n k_i)}{\mathbb{P}(\sum_{i=1}^n X_i =\sum_{i=1}^n k_i)}$$

Or, comme une somme de loi de Poisson suit une loi de poisson de paramètre, la somme des paramètres, nous pouvons directement dire (en notant $S:=\sum_{i=1}^n k_i$) :

$$T_2(k_1,...,k_n) =e^{-\lambda}\frac{e^{-(n-1)\lambda}\left((n-1)\lambda\right)^S}{S!}\times \left(\frac{e^{-n\lambda}(n\lambda)^S}{S!}\right)^{-1}$$
$$=(n-1)^S\frac{1}{n^S} = (1-\frac{1}{n})^S$$

Nous pourrions alors vérifier que la variance a effectivement diminué, mais nous nous contenterons de remarquer que cet estimateur est devenu convergent (à l'aide de la convergence presque sûre de $\frac{S}{n}$ vers $\lambda$). 

::::

### Statistique complète

La question qui suit est alors, comme toujours, celle de l'optimalité du résultat précédent. Pourrions-nous trouver un estimateur plus efficace que celui-ci ? La réponse est positive, si l'on est plus attentif dans le choix de notre statistique exhaustive. 

:::{prf:definition} Statistique complète
On dit qu’une statistique $S$ à valeurs dans $\R^q$ est _complète_ si, pour toute fonction mesurable $g$ telle que $g\circ S$ soit intégrable, alors

$$ \left(\forall\theta\in \Theta, \mathbb{E}_\theta[g(S(X))]=0\right) \Rightarrow \left(\forall\theta\in \Theta, g(S(X))=0 \text{ presque surement pour }\mathbb{P}_\theta\right)$$
::::{prf:theorem} Lehmann-Scheffé
Soit un modèle paramétrique et S une statistique exhaustive **complète**. Alors, pour tout estimateur T sans biais, l'estimateur

$$E=\mathbb{E}(T|S)$$

est (sans biais et) de variance inférieure à tout estimateur sans biais.

::::
:::




::::{prf:example}

Toujours avec le modèle de loi de Poisson indépendantes, vérifions que la statistique $S= \sum X_i$ est complète. Pour $\lambda>0$ et $g$ telle que $g\circ S \in L^1$, calculons :

$$\mathbb{E}\left[g\left(\frac{1}{n} \sum X_i\right)\right]= \sum_{k_1,...,k_n}g\left(\frac{1}{n} \sum k_i\right) e^{-n\lambda} \frac{\lambda^{\sum k_i}}{k_1!...k_n!}$$
$$=\sum_{k=0}^{+\infty} \sum_{\underset{\sum{k_i=k}}{k_1,...,k_n}}g\left(\frac{1}{n} \sum k_i\right) e^{-n\lambda} \frac{\lambda^{\sum k_i}}{k_1!...k_n!}$$
$$=e^{-n\lambda}\sum_{k=0}^{+\infty} g\left(\frac{k}{n}\right)\lambda^{k}\sum_{\underset{\sum{k_i=k}}{k_1,...,k_n}}  \frac{1}{k_1!...k_n!}$$


Donc si cette quantité est nulle pour tout $\lambda$, la série entière suivante est nulle

$$ \sum_{k=0}^{+\infty}\left( g\left(\frac{k}{n}\right)\sum_{\underset{\sum{k_i=k}}{k_1,...,k_n}}  \frac{1}{k_1!...k_n!}\right)\lambda^{k}=0$$

Donc $\forall k\in \N,  g\left(\frac{k}{n}\right)=0$.

En particulier, $g\circ S=0$, et la statistique est bien complète. Ainsi, la statistique $(1-\frac{1}{n})^S$ est optimale.
::::