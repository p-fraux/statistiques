## Test paramétrique composite
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

On veut à présent tester des hypothèses plus complexes. En effet,  il faut bien souvent envisager plus que deux lois potentielles. On pourra par exemple se rappeler l'exemple décrit dans la section précédente des durées de vie des moteurs, qui correspond à :

_Une hypothèse simple contre une hypothèse composite_ : 

$$\left\{ \begin{matrix}
    H_0 : \theta=\theta_0\\ \text{contre} \\ H_1 : \theta >\theta_0
\end{matrix}\right. .$$

 Plus généralement, on voudrait considérer les tests paramétriques les plus complexes possibles :


_Une hypothèse composite contre une hypothèse composite_ : 

$$\left\{ \begin{matrix}
    H_0 : \theta\in \Theta_0\\ \text{contre} \\ H_1 : \theta \in\Theta_1
\end{matrix}\right. , \qquad \text{avec } \Theta_0\cap \Theta_1=\emptyset.$$

En voyant l'efficacité du test de Neyman-Pearson, il est naturel de chercher à le généraliser. Une première idée serait de prendre comme statistique de test le rapport 

$$\frac{\sup\limits_{\theta \in \Theta_0} f(\mathbf{X},\theta)}{\sup\limits_{\theta \in \Theta_1} f(\mathbf{X},\theta)}.$$

Comme on peut rencontrer des valeurs trop petites au dénominateur, on peut alors modifier légèrement cette statistique. 

:::{prf:definition}
On pose $\Theta= \Theta_0\cup \Theta_1 $. On appelle test du rapport des maximums de vraisemblance le test basé sur la statistique de test :

 $$\Lambda_n=\frac{\sup\limits_{\theta \in \Theta_0} f(\mathbf{X},\theta)}{\sup\limits_{\theta \in \Theta} f(\mathbf{X},\theta)}.$$
 
On prendra alors une zone de rejet de la forme $\Lambda_n <\lambda_\alpha$
::::{prf:remark}
La statistique $\Lambda_n$ vérifie $0\leq \Lambda_n\leq 1$.
::::
:::

Comme nous avons généralisé les hypothèses, le résultat précédent est perdu. En revanche, on peut prouver le résultat suivant dans le cas d'une hypothèse simple contre une hypothèse composite :

:::{prf:theorem}
:class: dropdown
:label: loirapportvraissemblance
On considère un modèle identifiable, régulier (voir {ref}`dominee`), paramétrisé par $\R$, d'information de Fisher strictement positive ($I_n(f)(\theta) >0$) et de dérivée seconde de la Log-vraisemblance uniformément continue en $\theta$. 
On suppose aussi que le modèle est issu du tirage de variables aléatoire indépendante et de même loi.

On souhaite tester $H_0: \theta=\theta_0$ contre $H_1 : \theta \neq \theta_0$.


Si l'on considère la statistique du test du rapport des maximums de vraisemblance (avec l'EMV l'estimateur de maximum de vraisemblance) : 

$$\Lambda_n := \left\{ \begin{matrix}\frac{f(\mathbf{X},\theta_0)}{f(\mathbf{X},\hat{\theta})}\\
    \text{ où }\\ 
    \hat{\theta_n} \text{est l'EMV,}\end{matrix}\right.
$$
    
alors on a convergence en loi du logarithme de la statistique de test vers une loi du $\chi^2$ à un degré de liberté :
    
$$ -2\log(\Lambda_n) \overset{Loi}{\to} \chi^2_1.$$

::::{prf:proof}
 Notons $(X_i)$ la suite des réalisations et $\hat{\theta}_n$ l'estimateur du maximum de vraisemblance des $n$ premières réalisations.
 
 D'après le théorème de Taylor Lagrange appliqué à la log-vraisemblance en $\theta_0$, il existe des variables aléatoires $\theta^*_{i,n}$ telles que

$$\forall n\in \N,\forall i\leq n, \qquad \log\left( f(X_i,\theta_0)\right) = \log\left( f(X_i,\hat{\theta}_n(\mathbf{X}))\right) + (\theta_0-\hat{\theta}_n)\left(\partial_\theta \log f\right)(X_i,\hat{\theta}_n(\mathbf{X}))+ \frac{1}{2} (\theta_0-\hat{\theta}_n)^2\left(\partial_\theta^2 \log f\right)(X_i,{\theta}_{i,n}^*)$$

De plus, par uniforme continuité de $\partial_\theta^2 \log f$ en $\theta_0$, il existe une fonction $c : \R_+ \to \R_+$ croissante, indépendante de x, et de limite nulle en 0 telle que

$$ \forall x, |\partial_\theta^2 \log f(x,\theta)- \partial_\theta^2 \log f(x,\theta_0) | \leq c(|\theta-\theta_0|)$$

Avec ces deux résultats, nous pouvons calculer :

$$-2\log(\Lambda_n) = -2 \sum_{i=1}^n \left[\log f(X_i, \theta_0)-\log f(X_i, \hat{\theta}_n)\right]
$$= -2 \sum_{i=1}^n  (\theta_0-\hat{\theta}_n)\left(\partial_\theta \log f\right)(X_i,\hat{\theta}_n(\mathbf{X}))  - \sum_{i=1}^n (\theta_0-\hat{\theta}_n)^2\left(\partial_\theta^2 \log f\right)(X_i,{\theta}_{i,n}^*) $$
$$= 0 - \sum_{i=1}^n (\theta_0-\hat{\theta}_n)^2\left(\partial_\theta^2 \log f\right)(X_i,{\theta}_{i,n}^*)\ \text{ car }\ \hat{\theta}_n \text{ est l'EMV.}$$
$$=\frac{1}{I(\theta_0)}\left[\sqrt{I(\theta_0)}(\theta_0-\hat{\theta}_n)\sqrt{n}\right]^2 \left[\frac{1}{n}\sum_{i=1}^n \left(\partial_\theta^2 \log f\right)(X_i,{\theta}_{i,n}^*) \right]$$

Et en faisant artificiellement apparaitre les termes manquants

$$-2\log(\Lambda_n)=\left[\sqrt{I(\theta_0)}(\theta_0-\hat{\theta}_n)\sqrt{n}\right]^2 \frac{1}{I(\theta_0)}\left[\frac{1}{n}\sum_{i=1}^n \left(\partial_\theta^2 \log f\right)(X_i,{\theta}_0) +c(|\theta_0-{\theta}_{i,n}^*|) \right]$$

Or par croissance de c, $c(|\theta_0-{\theta}_{i,n}^*|)\leq c(|\theta_0-\hat{\theta}_{n}|)$. Comme $\hat{\theta}_{n}$ converge presque sûrement vers $\theta_0$ sous l'hypothèse $H_0$ (voir {ref}`EMV-prop-asymptotique`), $c(|\theta_0-\hat{\theta}_{n}|)$ converge presque surement vers 0.

De plus, d'après la loi des grands nombres, encore sous $H_0$,

$$\frac{1}{n}\sum_{i=1}^n \left(\partial_\theta^2 \log f\right)(X_i,{\theta}_0) \overset{p.s.}{\to} \mathbb{E}_{\theta_0} \left[\left(\partial_\theta^2 \log f\right)(X,{\theta}_0)\right] = I(\theta_0)$$

Encore une fois, avec les résultats de la section {ref}`EMV-prop-asymptotique`, 

$$\sqrt{I(\theta_0)}(\theta_0-\hat{\theta}_n)\sqrt{n} \overset{Loi}{\to} \mathcal{N}(0,1)$$

Par composition avec une fonction continue, $\left[\sqrt{I(\theta_0)}(\theta_0-\hat{\theta}_n)\sqrt{n}\right]^2$ converge alors en loi vers une $\chi^2$ à un degré de liberté.

Nous obtenons donc le produit d'une variable aléatoire qui converge presque surement vers 1 et d'une variable aléatoire qui converge en loi vers une $\chi^2$ à un degré de liberté. Nous pouvons alors conclure avec le lemme de Scheffé-Slutsky {ref}`Slutsky`.

::::
:::

:::{prf:remark}
L'on pourra donc avec le rapport des vraisemblances et la fonction quantile d'un $\chi^2$ développer un test asymptotique.
:::