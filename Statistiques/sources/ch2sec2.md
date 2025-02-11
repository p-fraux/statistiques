
## Efficacité d'un estimateur
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

Afin de faciliter nos calculs et obtenir des résultats plus fins, nous allons faire une série d'hypothèses simplificatrice sur la famille des lois. On parle alors d'hypothèse de régularité.

(dominee)=
### Régularité d'une expérience

:::{prf:definition} Vraisemblance
:class: dropdown
On dit qu'une famille de loi est dominée par une mesure $\nu$ si toutes les lois sont absolument continues par rapport à cette mesure. En particulier, il existe une fonction $(x,\theta) \mapsto L(x,\theta)$ intégrable en la première variable telle que pour toutes fonctions g mesurable bornée, 

$$\mathbb{E}_\theta(g(X))=\int_R g(x) L(x,\theta) d\nu(x).$$

On appelle alors le choix d'une telle fonction dans la classe d'équivalence d'égalité presque partout une vraisemblance (_Likelihood_) des lois.

::::{prf:remark}
En particulier, la connaissance de la vraisemblance permet de calculer la probabilité sous $\mathbb{P}_\theta$ de n'importe quel événement en prenant pour g l'indicatrice d'un événement.

::::

:::

::::{prf:example}

- Si $X=(X_1,\cdots,X_n)$ est un vecteur aléatoire discret, alors en prenant la mesure de comptage comme mesure  dominante, on trouve que la vraisemblance L est égale

$$L(k_1,\cdots,k_n, \theta)=\mathbb{P}_\theta(X_1=k_1,\cdots,X_n=k_n)$$

- Si $X=(X_1,\cdots,X_n)$ est un vecteur aléatoire absolument continu, alors en prenant la mesure de Lebesgue comme mesure  dominante, on trouve avec $f_\theta$ la densitée de probabilité de $\mathbb{P}_\theta$ que la vraisemblance L est égale

$$L(x_1,\cdots,x_n,\theta)=f_\theta(x_1,\cdots,x_n)$$

Ainsi, avec $X_i \sim \mathcal{E}(\lambda_i)$, la vraisemblance du vecteur $(X_1, ..., X_n)$ est :
$$ L : (x_1,...,x_n, \lambda_1, ...,\lambda_n) \mapsto \prod_{i=1}^n\lambda_i e^{-\lambda_i x_i}{1}_{\R_+}(x_i)$$
::::


:::{prf:remark}
Dans le cas d'une suite de variables indépendante identiquement distribué, on peut choisir comme mesure dominante une mesure produit. Dans ce cas, la vraisemblance d'un vecteur aléatoire s'écrira comme un produit.

:::

:::{prf:definition} Modèle régulier.
:class: dropdown
Soit une expérience statistique dominée par une mesure $\mu$, et $f(x,\theta)$ une vraisemblance associée.

On considère la suite de propriétés suivante par rapport à la mesure $\mu$ :

$$
    \{x \in \R, L(x,\theta)>0\} \text{ est indépendant de }\theta. \tag{H1}\label{H1}
$$

$$
    \Theta \text{ est un interval ouvert.} \tag{H2}\label{H2}
$$


$$
    \partial_\theta L(x,\theta) \text{ et }\partial_\theta^2 L(x,\theta) \text{ existent et sont intégrables par rapport à la loi }\mathbb{P}_\theta. \tag{H3}\label{H3}
$$
$$
    \text{Il est possible de deriver deux fois la vraisemblance sous le signe intégrale - hypothèses de dominations.} \tag{H4}\label{H4}
$$
$$
    \text{La fonction } Sc_\theta(x) \mapsto \partial_\theta \ln L(x,\theta) \text{ (pour score) est de carré intégrable.} \tag{H5}\label{H5}
$$
Lorsque les cinq propriétés _H1-5_ sont vérifiées, on dit que le modèle est régulier.



::::{prf:remark}
- La première hypothèse correspond à pouvoir, quitte à modifier le support de la mesure $\mu$, mettre la densité sous la forme d'une exponentielle. On retrouve alors parmi les modèles vérifiant cette hypothèse tous les modèles exponentiels (dont on trouvera une introduction dans {cite:ps}`Mathematical-statistics`).

- La deuxième hypothèse assure un espace de paramètre satisfaisant pour une analyse fonctionnelle.

- La troisième et quatrième hypothèse permettent de  calculer facilement les variations des quantités d'intérêts statistiques par rapport au paramètre. En particulier, elles simplifieront la recherche d'optimum

- La dernière hypothèse est là pour permettre l'étude qui va suivre de l'information de Fisher.
::::


:::

::::{prf:example}
- La famille des lois normales avec comme paramètres moyenne et variance.

- La famille des lois Gamma.

- La famille des lois de Poissons.

::::

### Borne de Cramer-Rao et efficacité d'un estimateur

Un des résultats principal des modèles réguliers est une minoration du risque quadratique, minoration qui décrit l'impossibilité d'avoir une statistique parfaite.

L'idée de cette minoration est de définir une notion de quantité d'information que l'on peut extraire d'une loi.

Cette quantité d'information sera directement reliée à la variation du score d'une probabilité (qui mesure la variation de la densité au voisinage d'une loi). 

:::{prf:definition} Score
:class: dropdown
L'on considère un modèle régulier, et l'on note $(x,\theta) \mapsto L(x,\theta)$ la vraisemblance.

On note $\mathcal{X}$ l'ensemble $\{x\in \R | L(x,\theta)>0\}$ (cet ensemble est bien défini grâce à l'hypothèse \eqref{H1}, et on l'appelle _support_ du modèle).

On appelle fonction score du modèle l'application :

$$ Sc : \left\{\begin{matrix}\mathcal{X}\times \Theta &\to& \R\\(x,\theta) &\mapsto &\partial_\theta \ln(f(x,\theta)),\end{matrix}\right.
$$

qui est bien défini grâce à l'hypothèse \eqref{H3}.

::::{prf:remark}
La présence du logarithme dans la définition du score permet, dans le cas indépendant, d'écrire la fonction score d'un vecteur comme somme de score de chacune des composantes.

Dans le cas d'un vecteur, l'on notera de même $Sc_n(\mathbf{x},\theta) =\partial_\theta \ln(f(\mathbf{x},\theta)) $ la fonction score correspondante.

Dans le cas particulier de variables indépendantes, on pourra vérifier que si l'on note $Sc$ le score de la première composante, l'on a que $ Sc_n(\mathbf{x},\theta) = \sum_{i=1}^n Sc(x_i,\theta)$.

::::

:::



:::{prf:definition} Information de Fisher

Pour une expérience statistique dans un modèle régulier de vraisemblance $L(x,\theta)$, on définit _l'information de Fisher_ de la variable aléatoire réelle X (sous-entendu sous la loi  $\mathbb{P}_\theta$) comme la quantité :

$$ 
\mathcal{I}_X(\theta):= -\mathbb{E}_\theta\left[\frac{\partial^2}{\partial \theta^2} \ln L(X,\theta)\right].
$$

De même, on définit _l'information de Fisher_ du vecteur aléatoire réel $\mathbf{X}$ comme la quantité :

$$ 
\mathcal{I}_{\mathbf{X}}(\theta):= -\mathbb{E}_\theta\left[\frac{\partial^2}{\partial \theta^2} \ln(f(\mathbf{X},\theta))\right].
$$


Dans le cas où les composantes d'un vecteur aléatoire $\mathbf{X}=(X_i)_{i\in [\![1,n]\!]}$ sont indépendantes dans leur ensemble et de même loi, on aura la relation sur l'information de Fisher :

$$\mathcal{I}_{\mathbf{X}}(\theta) =n \mathcal{I}_{X_1}(\theta) .$$

::::{prf:property} Réecriture utile
:class: dropdown
Pour une expérience statistique avec un modèle régulier,
    
$$ I_X(\theta) = \mathbb{E}_\theta\left[Sc(x,\theta)^2\right].$$

:::::{prf:proof} 
Commençons d'abord par remarque que grâce à \eqref{H4}, l'on a que :

$$\int \frac{\partial^2}{\partial \theta^2}\left(f(x,\theta) \right)d\nu(x) = \frac{\partial^2}{\partial \theta^2}\left( \int f(x,\theta) d\nu(x)\right) = \frac{\partial^2}{\partial \theta^2} 1 =0.$$

Maintenant, grâce au théorème de transfert pour les mesures à densité, l'on peut calculer :

$$ \mathbb{E}_\theta\left[\frac{\partial^2}{\partial \theta^2} \ln(f(X,\theta))\right] = \int \frac{\partial^2}{\partial \theta^2} \ln(f(X,\theta)) \ f(x,\theta ) d\nu(x)$$
$$= \int \frac{\partial}{\partial \theta}\frac{\partial_\theta f}{f}(x,\theta) \ f(x,\theta ) d\nu(x),$$
$$= \int \left(\frac{\partial^2}{\partial \theta^2}f(x,\theta) - \frac{\partial_\theta f \times \partial_\theta f}{f^2}(x,\theta) \ f(x,\theta ) \right)d\nu(x)$$

Enfin, comme la fonction score est de carré intégrable, on peut utiliser la linéarité de l'intégrale et trouver que 

$$ \mathbb{E}_\theta\left[\frac{\partial^2}{\partial \theta^2} \ln(f(X,\theta))\right] =  \int \frac{\partial^2}{\partial \theta^2}f(x,\theta)d\nu(x) - \int Sc(x,\theta)^2 \ f(x,\theta ) d\nu(x) = 0- \mathbb{E}_\theta\left[Sc^2\right]$$

qui est bien le résultat voulu.
:::::
::::



::::::{prf:remark}
L'information de Fisher donne une estimation moyenne de la courbure de la Log-vraisemblance. Si l'information est grande, la Log-vraisemblance varie beaucoup. L'estimation du maximum de vraisemblance (voir [l'Estimateur de maximum de vraisemblance](EMV_section)), obtenue en prenant le paramètre pour lequel la chance d'obtenir le résultat tirée est maximale, est meilleur : elle est plus sensible à un petit déplacement de paramètre ; on pourra donc obtenir plus d'information sur le vrai paramètre à partir  de l'échantillon.
::::::

:::

 



:::{prf:definition} Efficacité

On dit qu'une statistique $T_n$ est _efficace_ en $\theta$ si elle est sans biais et atteint la borne de Cramer-Rao en $\theta$ (définie ci-dessous) 
    
$$\mathbb{E}_\theta(T_n)= h(\theta) \qquad \text{ et } \qquad V_\theta(T_n)= \frac{{(h'(\theta)^2}}{I_X(\theta)}$$

:::



:::{prf:theorem} Borne de Cramer-Rao
On considère un modèle régulier (hypothèse \eqref{H1} à \eqref{H5}).

Soit $h$ une fonction dérivable sur $\Theta$, et soit une statistique bornée $T_n$ qui est un estimateur sans biais de $h(\theta)$. 

Si $I_\mathbf{X}(\theta)>0$, on a la minoration de la variance suivante :

$$V_\theta(T_n) \geq \frac{(h'(\theta))^2}{I_\mathbf{X}(\theta)}.$$

En particulier, pour un estimateur de $\theta$ sans biais, 

$$V_\theta(T_n) \geq \frac{1}{I_\mathbf{X}(\theta)}.$$

::::{prf:proof} 
On se donne une statistique $T_n$ qui est un estimateur borné sans biais de $h(\theta)$.

Alors 
    
$$|h'(\theta)|= \left|\frac{\partial}{\partial \theta} \mathbb{E}_\theta\left[T_n(\mathbf{X})\right]\right|,$$
$$=\left| \frac{\partial}{\partial \theta} \int T_n(\mathbf{x}) f(\mathbf{x},\theta) d\nu(x)\right|,$$

Et par dérivation sous l'intégrale,

$$|h'(\theta)|=\left| \int T_n(\mathbf{x}) \frac{\partial}{\partial \theta} \left(f(\mathbf{x},\theta)\right) d\nu(x)\right| $$
$$=\left| \int T_n(\mathbf{x}) f(\mathbf{x},\theta) \times  \frac{\partial f(\mathbf{x},\theta)}{f(\mathbf{x},\theta) } d\nu(x)\right|,$$

Et comme 

$$\int\mathbb{E}_\theta(T_n)\partial_\theta f(\mathbf{x},\theta)d\nu(x)=\mathbb{E}_\theta(T_n)\partial_\theta\int f(\mathbf{x},\theta)d\nu(x)=\mathbb{E}_\theta(T_n)\partial_\theta(1)=0,$$

on a

$$|h'(\theta)|=\left| \int T_n(\mathbf{x})  \times  \frac{\partial f(\mathbf{x},\theta)}{f(\mathbf{x},\theta) } f(\mathbf{x},\theta)d\nu(x)-\int\mathbb{E}_\theta(T_n)\partial_\theta f(\mathbf{x},\theta)d\nu(x)\right|,$$
$$=\left| \int (T_n(\mathbf{x}) -\mathbb{E}_\theta(T_n)) \times  \frac{\partial f(\mathbf{x},\theta)}{f(\mathbf{x},\theta) } f(\mathbf{x},\theta)d\nu(x)\right|,$$
$$=\mathbb{E}_\theta\left[(T_n(\mathbf{X}) -\mathbb{E}_\theta(T_n)) \times  \frac{\partial f(\mathbf{X},\theta)}{f(\mathbf{X},\theta) }\right]$$

Et donc d'après l'inégalité de Cauchy-Schwarz,

$$|h'(\theta)|\leq \sqrt{\mathbb{E}_\theta\left[(T_n(\mathbf{X})-\mathbb{E}_\theta(T_n))^2\right] }\sqrt{\mathbb{E}_\theta\left[Sc(\mathbf{X}, \theta)^2\right]} $$
$$= \sqrt{V_\theta\left[T_n(\mathbf{X})\right] }\sqrt{I_X(\theta)}.$$

En prenant alors le carré de cette inégalité, l'on retrouve bien l'inégalité de Cramer-Rao annoncé.
::::

:::

