(EMV_section)=
## Estimateur de Maximum de Vraisemblance
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

Cette page présente un premier estimateur à considérer lors d'une recherche d'approximation : l'estimateur du maximum de vraisemblance. Il s'agit de chercher le paramètre $\theta$ pour lequel la probabilité $\mathbb{P}_\theta$ met le plus grand poids sur le résultat obtenu.

### Définition et méthode de calcul pour les modèles réguliers

:::{prf:definition} EMV
:class: dropdown
On considère un modèle régulier de vraisemblance $f(\mathbf{x}, \theta)$. On appelle estimateur du maximum de vraisemblance (EMV) une statistique $\hat{\theta}$ qui renvoie un des paramètres $\theta$ pour lequel la vraisemblance de la réalisation est maximale. 

$$f(\mathbf{x}, \hat{\theta}) = \max_{\theta \in \Theta}f(\mathbf{x}, {\theta}) $$

::::{prf:remark}
Pour pouvoir calculer l’Estimateur du Maximum de Vraisemblance (E.M.V., ou MLE en anglais), il faut que le modèle soit spécifié (gaussien, exponentiel, etc.)

Attention cependant, il n’y a pas forcément unicité de la solution de l’équation de vraisemblance, et donc de l'estimateur.

::::

:::


:::{admonition} Méthode dans un modèle régulier :
:class: tip
- Calculer la vraisemblance, et en déduire la Log-vraisemblance
- Calculer et chercher les points d'annulations de la fonction score :

$$\partial_\theta \ln\left(f(\mathbf{x},\theta) \right)$$

- Chercher le maximum de la Log-vraisemblance parmi les points d'annulation de la fonction score et le bord de $\Theta$ si l'hypothèse H2 n'est pas vérifiée. 

Pour vérifier qu'un point est bien un maximum, l'on pourra sur un intervalle utiliser un argument de convexité (_i.e._ calculer la dérivée seconde et étudier son signe), ou encore tracer un tableau de variation pour éliminer les optimums locaux des candidats possibles.
:::


```{exercise} EMV et lois exponentielles
:class: dropdown
:label: exer08
On considère l'expérience statistique issue de la répétition indépendante de n tirage $(X_1,...,X_n)$ de variable aléatoire suivant des lois exponentielles de paramètre $\lambda>0$.

a) Calculer l'estimateur du maximum de vraisemblance.

:::{admonition} Solution a)
:class: dropdown
 La Log-vraisemblance est la fonction

$$\ln(f) : (x_1,...,x_n) \mapsto \sum_{i=1}^n \ln(\lambda) - \lambda x_i = n\ln(\lambda)- \lambda \sum_{i=1}^n x_i$$

Cette application est bien dérivable en $\lambda$, de dérivé 

$$\partial_\theta\ln\circ f (\mathbf{X}, \theta) = \frac{n}{\lambda} - \sum_{i=1}^nx_i.$$

Comme celle-ci s'annule pour $\theta = \frac{n}{\sum_{i=1}^nx_i} = \frac{1}{\overline{X_n}}$, et que la Log-vraisemblance est concave (sa dérivée seconde existe et est négative), l'on a bien que l'estimateur du maximum de vraisemblance est 

$$\frac{1}{\overline{X_n}}.$$
:::


b) Montrer que la moyenne empirique converge presque sûrement et en moyenne quadratique vers $\lambda$. En déduire le caractère convergent de l'estimateur du maximum de vraisemblance.

:::{admonition} Solution b)
:class: dropdown
Par la loi forte des grands nombres, la moyenne empirique converge presque surement et dans $L^2$ vers l'espérance, qui vaut $\frac{1}{\lambda}$.

L'EMV converge presque surement (par les opérations sur les limites réelles) vers $\lambda$ donc converge en probabilité.
:::

```

```{exercise} EMV et lois discrètes
:class: dropdown
:label: exer09
 On considère l'expérience statistique issue de la répétition indépendante de n tirage $(X_1,...,X_n)$ de variable aléatoire suivant des lois de Bernoulli de paramètre $0< p < 1$.

a) Calculer l'estimateur du maximum de vraisemblance de $p$.

:::{admonition} Solution a)
:class: dropdown
  La Log-vraisemblance est la fonction

$$\ln(f) : (x_1,...,x_n) \mapsto \ln(\mathbb{P}_p(\forall i, \quad X_i=x_i)) = \ln(p^{\sum x_i}(1-p)^{n-\sum x_i}) $$

Cette application est bien dérivable en $p$, de dérivé 

$$\partial_\theta\ln\circ f (\mathbf{X}, p) = \frac{1}{p}\sum x_i  -\frac{1}{1-p}(n-\sum_{i=1}^nx_i).$$

Cette expression s'annule uniquement pour $p=\overline{X}$. 

Comme la dérivée seconde de la log-vraisemblance est 

$$-\frac{1}{p^2}\sum x_i  -\frac{1}{(1-p)^2}(n-\sum_{i=1}^nx_i)<0, $$

on a bien trouvé un maximum de la Log-vraisemblance.
:::


b) L'estimateur est-il sans biais ? convergent ? efficace ?

:::{admonition} Solution b)
:class: dropdown
Il est sans biais car $\mathbb{E}_p(\overline{X})=p$.

Il est convergent grâce à la loi des grands nombres.

Pour montrer qu'il est efficace, commençons par calculer l'information de Fisher :

$$I(p)=-\mathbb{E}_p(\partial_\theta^2\ln\circ f (\mathbf{X}, p)) = -\mathbb{E}_p\left[-\frac{1}{p^2}\sum x_i  -\frac{1}{(1-p)^2}(n-\sum_{i=1}^nx_i)\right]=\frac{np}{p^2}+\frac{n(1-p)}{1-p}$$

Donc $I(p)=\frac{n}{p(1-p)}$. En particulier, la borne de Cramer-Rao pour un estimateur de p est $\frac{p(1-p)}{n}$. Comme $V(\overline{\mathbf{X}})=p(1-p)\frac{n}{n^2}$, l'estimateur est donc efficace.

:::

```

```{exercise} Examen 2024 - Loi Log-Normal
:label: exer10
:class: dropdown
On considère l'expérience statistique issue de la répétition indépendante de n tirage $(X_1,...,X_n)$ de variable aléatoire suivant la même loi de densité de paramètre $\theta>0$ et $\mu \in \R$ :

$$\forall x>0, \qquad f(x)=\frac{1}{\theta x\sqrt{2\pi}}e^{-\frac{\left(\ln(x)-\mu\right)^2}{2\theta^2}}$$

On peut vérifier que $Y_i=\ln(X_i)$ suivent des lois normales $\mathcal{N}(\mu,\theta^2)$ et l'on rappelle que la fonction génératrice des moments d'une loi normale vérifie

$$M_{Y}(t)=\mathbb{E}(e^{tY})=e^{\mu t +\frac{\theta^2t^2}{2}}$$

a) Montrer que l'espérance et la variance de X s'écrivent 

$$\mathbb{E}(X)=e^{\mu +\frac{\theta^2}{2}} \qquad \text{et} \qquad V(X)= e^{2\mu+\theta^2}\left(e^{\theta^2}-1\right).$$

:::{admonition} Solution a)
:class: dropdown
L'on vérifie que 
 
$$\mathbb{E}(X)=\mathbb{E}(e^{ln(X)})= e^{\mu *1 +\frac{\theta^2*1^2}{2}}$$

et que 

$$V(X)=\mathbb{E}(X^2)-\mathbb{E}(X)^2=e^{2\mu+\theta^2}\left(e^{\theta^2}-1\right) $$
:::


b) Déterminer, en supposant $\theta$ connu, l'estimateur du maximum de vraisemblance de $\mu$ , noté $\hat{\mu}_{MV}$, construit à partir d'observation de $X_1,...,X_n$. L'on prendra le soin d'établir un tableau de variation associé à la fonction à maximiser

:::{admonition} Solution b)
:class: dropdown
La Log-vraisemblance de l'échantillon s'écrit 

$$\ln f(x_1,...,x_n,\mu,\theta) = -n( \ln(\theta) -\ln(\sqrt{2\pi}))-\sum_{i=1}^n ln(x_i) - \sum_{i=1}^n \frac{(ln(x_i)-\mu)^2}{2\theta^2}$$

Sa dérivée suivant $\mu$ s'écrit

$$ \partial_\mu\ln f(x_1,...,x_n,\mu,\theta) =  \sum_{i=1}^n \frac{ln(x_i)-\mu}{\theta^2}$$

Qui est bien décroissante en $\mu$ et s'annule pour $\mu = \frac{1}{n} \sum_{i=1}^n\ln(x_i).$

En particulier, la log-vraisemblance est concave et admet pour maximum $\hat{\mu}_{MV}=\frac{1}{n} \sum_{i=1}^n\ln(x_i)$
:::

c) Montrer que $\hat{\mu}_{MV}$ est un estimateur sans biais, convergent de $\mu$.

:::{admonition} Solution c)
:class: dropdown
Avec le rappel, $\mathbb{E}(\ln(X))=\mathbb{E}(Y)=\mu$ donc l'estimateur n'a pas de biais.

Avec la loi des grands nombres appliquée aux lois normales, l'estimateur converge presque surement vers $\mu$ et en particulier converge en probabilité.
:::

d)  Montrer que $\hat{\mu}_{MV}$ est un estimateur efficace de $\mu$.

:::{admonition} Solution d)
:class: dropdown
Commençons par calculer la borne de Cramer-Rao.

La dérivée seconde de la log-vraisemblance est

$$\partial_\mu^2\ln(f(x_1,...,x_n,\mu,\theta) =  -\sum_{i=1}^n \frac{\mu)}{\theta^2} = -\frac{n}{\theta^2}$$ 

En particulier, l'information de Fisher est $$I(\mu)= \mathbb{E}(-\partial_\mu^2\ln(f(x_1,...,x_n,\mu,\theta)))= \frac{n}{\theta^2}$$

Comme la variance de $\hat{\mu}_{MV}$ est celle d'une somme de loi normale, elle vaut $V(\hat{\mu}_{MV})=\frac{V(\ln(X_i))}{n}=\frac{\theta^2}{n}=\frac{1}{I(\mu)}$.

L'estimateur est donc efficace
:::

e)  Nous ne supposons plus $\theta$ connu. À l'aide des valeurs de l'espérance et de la variance de X, proposer un estimateur de $(\mu,\theta)$ qui ne dépend que de 

$$\overline{X}=\frac{1}{n}\sum_{i=1}^n X_i \quad \text{ et } \quad \overline{X^2}=\frac{1}{n}\sum_{i=1}^n X_i^2$$ 
:::{admonition} Solution d)
:class: dropdown
Notons $m_1=\mathbb{E}(X)$ et $m_2=\mathbb{E}(X^2)$.

Alors avec la première question, nous avons le système

$$ \left\{\begin{matrix}
       \mu+\frac{\theta^2}{2} & =& \ln(m_1),\\ 2\mu +2\theta^2&=& \ln(m_2),
   \end{matrix} \right. \iff \left\{\begin{matrix}
       \theta^2 & =& \ln(m_2)-2\ln(m_1),\\ \mu &= &2\ln(m_1)-\frac{1}{2}\ln(m_2).
   \end{matrix} \right.$$

Nous pouvons alors poser comme estimateur 

$$\left\{\begin{matrix}
         \hat{\mu} &= &2\ln(\overline{X^1})-\frac{1}{2}\ln(\overline{X^2}),\\
       \hat{\theta^2} & =& \ln(\overline{X^2})-2\ln(\overline{X}).
   \end{matrix} \right. $$
:::

```

```{exercise} EMV et lois discrètes 2
:label: exer11
:class: dropdown
On considère l'expérience statistique issue de la répétition indépendante de n tirage de variable aléatoire, avec $\Theta= ]-1,1[$ et de loi $\mathbb{P}_\theta$ la loi sur $\{0,1,−1\}$ avec des probabilités respectives $1-\theta$, $\frac{\theta}{2}$ et $\frac{\theta}{2}$.

Calculer l’estimateur du maximum de vraisemblance en fonction du nombre de résultats nuls $n_1$.

:::{admonition} Solution 
:class: dropdown
La statistique est dominée par la mesure de comptage sur $\{0,1,-1\}$.

La vraisemblance est l'application     

$$({\bf x},\theta) \mapsto \prod_{x_i =0} (1-\theta) \times \prod_{x_i=1}\frac{\theta}{2} \times \prod_{x_i=-1}\frac{\theta}{2}  $$ 

La Log-vraisemblance est alors    

$$({\bf x},\theta) \mapsto \sum_{x_i =0} \log(1-\theta) +\sum_{x_i\neq 0}\log(\frac{\theta}{2}) $$

dont la dérivée s'annule en $\hat{\theta}$ tel que 

$$(n-n_1)\frac{2}{\hat{\theta}}- \frac{n_1}{1-\hat{\theta}}=0$$

 C'est à dire pour $\hat{\theta}=\frac{2(n-n_1)}{2n-n_1}$.
:::


```

    

(EMV-prop-asymptotique)=
### Propriétés asymptotiques

Une hypothèse essentielle à une étude plus fine est l'identifiabilité, c'est-à-dire que la connaissance de la loi permette de retrouver le paramètre.

:::{prf:definition} Identifiabilité
On dit qu'un modèle est _identifiable_ si l'on a que :

$$ \theta_1\neq \theta_2 \iff \mathbb{P}_{\theta_1}\neq \mathbb{P}_{\theta_2}$$

:::


::::{prf:property} Convergence de l'EMV
:class: dropdown
On considère un modèle identifiable d'une suite de variable aléatoire indépendante de même loi, avec l'expérience statistique qui est dominée, vérifie H1 et H2, et que la Log-vraisemblance est continue. On suppose de plus que l'adhérence de $\Theta$ est compacte, et on rappelle que {le vrai paramètre recherché $\theta_0$ est} dans ${\Theta}$ un ouvert.

On suppose de plus qu'il existe une suite de statistique $\hat{\theta}_n$ qui calcule un maximum de vraisemblance avec probabilité 1 sous la loi $ \mathbb{P}_{\theta_0}$, c'est-à-dire que :

$$\mathbb{P}_{\theta_0}\left( \forall \theta, f(X_1,...X_n, \hat{\theta}_n(X_1,...X_n)) \geq   f(X_1,...X_n, \theta) \right)=1.$$

Enfin, on suppose que pour ce $\theta_0$, les variables aléatoires $\left(\ln(f(X_1,\theta))\right)_{\theta}$ sont toutes intégrables.

Alors sous la loi $\mathbb{P}_{\theta_0} $, $\hat{\theta}_n$ converge presque sûrement vers $\theta_0$ :

$$\mathbb{P}_{\theta_0}\left(\lim\limits_{n\to +\infty}\hat{\theta}_n = \theta_0\right)=1$$

:::::{prf:proof} _(inspiré de {cite}`advanced-stats`)_
On peut commencer par remarquer que grâce à l'inégalité de Jensen (voir {ref}`Jensen`), l'on a l'inégalité suivante pour tout $\theta \in \Theta$ :

$$ \mathbb{E}_{\theta_0}\left[ \ln\left(\frac{f(\mathbf{X},\theta)}{f(\mathbf{X},\theta_0)}\right)\right] \leq  \ln\left(\mathbb{E}_{\theta_0}\left[ \frac{f(\mathbf{X},\theta)}{f(\mathbf{X},\theta_0)}\right]\right)$$

Or, le membre de droite se calcule sans peine. En effet, 

$$\mathbb{E}_{\theta_0}\left[ \frac{f(\mathbf{X},\theta)}{f(\mathbf{X},\theta_0)}\right]= \int \left( \frac{f(\mathbf{x},\theta)}{f(\mathbf{x
    },\theta_0)}\right) f(\mathbf{x},\theta_0 ) d\nu(\mathbf(x)=\int f(\mathbf{x},\theta)d\nu(\mathbf(x) =1  $$
    
Donc l'on a 

$$\mathbb{E}_{\theta_0}\left[ \ln\left(\frac{f(\mathbf{X},\theta)}{f(\mathbf{X},\theta_0)}\right)\right] \leq 0 $$

Ce qui se réécrit 

$$ \mathbb{E}_{\theta_0}\left[ \ln\left(f(\mathbf{X},\theta)\right)\right] \leq \mathbb{E}_{\theta_0}\left[ \ln\left(f(\mathbf{X},\theta_0)\right)\right]$$

Maintenant, par l'hypothèse d'un modèle issu d’une suite de variable aléatoire indépendante, la Log-vraisemblance vérifie que pour tout paramètre $\theta$, 

$$ \frac{1}{n}\ln\left(f(\mathbf{X},\theta)\right)=\frac{1}{n}\sum_{i=1}^n\ln\left(f({X_i},\theta)\right).$$

L'on utilise encore une fois le fait que $\left(\ln\left(f({X_i},\theta)\right)\right)_{i\in \N}$ est une suite de variable indépendante (par transfert de l'indépendance), intégrable et de même loi. En effet, d'après la loi des grands nombres, l'on obtiendra pour tous $\theta$ la convergence presque sûre sous $\mathbb{P}_{\theta_0}$ que 

$$\frac{1}{n}\sum_{i=1}^n\ln\left(f({X_i},\theta)\right) \overset{p.s. \mathbb{P}_{\theta_0}}{\to} \mathbb{E}_{\theta_0}\left[ \ln\left(f(X_1,\theta)\right)\right].$$

En particulier, l'on obtiendra  que 

$$\mathbb{P}_{\theta_0}\left( \lim\limits_{n\to +\infty}\frac{1}{n}\ln\left(f(\mathbf{X},\theta)\right)\leq \lim\limits_{n\to +\infty}\frac{1}{n}\ln\left(f(\mathbf{X},\theta_0)\right) \right) =1 $$

De plus, comme $\hat{\theta}_n$ est un maximum de vraisemblance, l'on a que 

$$\mathbb{P}_{\theta_0}\left( \liminf\limits_{n\to +\infty}\frac{1}{n}\ln\left(f(\mathbf{X},\hat{\theta}_n)\right)\geq \lim\limits_{n\to +\infty}\frac{1}{n}\ln\left(f(\mathbf{X},\theta_0)\right) \right) =1$$

En particulier, si pour chaque événement l'on considère une valeur d'adhérence, 
    $$ \mathbb{P}_{\theta_0}\left( \forall \theta^*, (\exists \phi \text{ extractrice}, \lim\limits_n\hat{\theta}_{\phi(n)} = \theta^*) \Rightarrow \liminf\limits_{n\to +\infty}\frac{1}{n}\ln\left(f(\mathbf{X},\hat{\theta}_{\phi(n)})\right)= \lim\limits_{n\to +\infty}\frac{1}{n}\ln\left(f(\mathbf{X},\theta_0)\right) \right)=1$$

ou encore en utilisant l'indépendance

$$ \mathbb{P}_{\theta_0}\left( \forall \theta^*, (\exists \phi \text{ extractrice}, \lim\limits_n\hat{\theta}_{\phi(n)} = \theta^*) \Rightarrow \liminf\limits_{n\to +\infty}\ln\left(f(X_1,\hat{\theta}_{\phi(n)})\right)= \ln\left(f(X_1,\theta_0)\right) \right)=1$$

Ce qui par continuité de la log-vraisemblance donne :

$$ \mathbb{P}_{\theta_0}\left( \forall \theta^*, (\exists \phi \text{ extractrice}, \lim\limits_n\hat{\theta}_{\phi(n)} = \theta^*) \Rightarrow \ln\left(f(X_1,\theta^*)\right)= \ln\left(f(X_1,\theta_0)\right) \right)=1$$

Ce qui donne par identifiabilité que 

$$ \mathbb{P}_{\theta_0}\left( \forall \theta^*, (\exists \phi \text{ extractrice}, \lim\limits_n\hat{\theta}_{\phi(n)} = \theta^*) \Rightarrow \theta^*=\theta_0 \right)=1$$

Ce qui donne par compacité de $\Theta$ que 

$$ \mathbb{P}_{\theta_0}\left( \lim\limits_{n\to +\infty} \hat{\theta}_n = \theta_0 \right)=1$$
:::::

L'hypothèse de compacité, tout comme celle sur l'existence d'une suite $\hat{\theta}_n$ d'estimateur de maximum de vraisemblance, peut être
supprimée, quitte à affaiblir la conclusion (voir ainsi le `Théorème 3.7, page 447` de {cite:ps}`lehmann1998theory`).
::::

