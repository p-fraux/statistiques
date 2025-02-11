## Hypothèses statistique et tests
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

La problématique des tests est vaste, prenons un exemple jouet avec nous pour ne pas nous perdre, et suivront au cours de cette section la démarche à suivre, tout en décrivant le vocabulaire :

:::{prf:example}
:class: dropdown
Les moteurs d’appareils électroménagers d’une marque donnée ont une durée de vie que l’on peut modéliser par une variable aléatoire réelle de loi gaussienne $\mathcal{N}(3000, (150)^2)$.
À la suite d’une modification dans la fabrication des moteurs, le fabricant affirme que
les nouveaux moteurs ont une durée de vie supérieure à celle des anciens moteurs. Nous allons voir comment les statistiques permettent de tester cette affirmation commerciale. 
:::

### Décrire ce qui est testé avec des hypothèses statistiques

Les tests permettent de savoir si l'on doit abandonner une idée actuelle en faveur d'une alternative raisonnable. Pour cela, il est nécessaire avant même de concevoir le test de dégager les hypothèses.

:::{prf:definition}
On appelle _hypothèse statistique_ toute proposition sur la nature de la loi d'une expérience statistique.
:::

:::{prf:example} Exemple d'hypothèses :
- Le paramètre de la loi vaut une valeur $m_0$.
- Le paramètre de la loi est dans une certaine région de l'espace des paramètres.
- La loi appartient à une famille donnée de lois.
- La loi est issue d'un tirage indépendant, etc.
:::



Pour construire un test binaire, on commencera toujours par formuler deux hypothèses statistiques :
- Une hypothèse conservatrice $H_0$ aussi appelée hypothèse nulle,
- Une hypothèse alternative $H_1$.

 On doit choisir ces hypothèses de manière à ce qu'elles ne se réalisent jamais simultanément, mais également à ce qu'elles couvrent l'ensemble des éventualités envisageables.


:::{danger}
Attention, si pour l'instant la distinction entre $H_0$ et $H_1$ est purement sémantique, la procédure de construction des tests conduit à briser la symétrie. Ces deux hypothèses ne jouent pas le même rôle, ce qui se lira dans la conclusion possible d'un test.
:::

:::{prf:example} 
:class: dropdown
Pour tester les dires du fabricant des nouveaux moteurs, on se donne deux hypothèses statistiques :
- $H_0$ : la durée de vie des moteurs suivent des lois normales indépendantes de moyenne inchangée $m=m_0=3000$
- contre $H_1$ : la durée de vie des moteurs suivent des lois normales indépendantes de moyenne supérieures $m>m_0=3000$
:::

### Construire un test statistique

Pour construire un test,  une fois l’hypothèse $H_0$ formulée, il faut choisir une statistique de travail et une règle de décision.
_En traitement du signal, les tests statistiques apparaissent dans les problèmes de détection : problèmes d’alarme, détection de la présence d’un signal noyé dans du bruit, etc._

:::{prf:definition}
On appelle _test_ sur une expérience statistique la donnée d'une statistique 
$ T: X \to \{0,1\}$.
    
Lorsque T vaut 1, l'on dira que l'on rejette l'hypothèse nulle $H_0$.

Le plus souvent, un test sera décrit par la donnée d'une statistique $ S: X \to \R^n$ et d'une _région d'acceptation_ $A\subset \R^n$ en posant $T=1_{S\in A}$.

Dans ce cas, on appellera zone critique la frontière (topologique) de la région d'acceptation.
:::

_On peut penser le test comme le Booléen qui répond a la question : doit-on raisonnablement rejeter $H_0$ ? Si le test est bien construit, l'on obtiendra de bons résultats._


:::{prf:definition}
 On dit qu'un test est _paramétrique_ lorsque les hypothèses $H_0$ et $H_1$ portent sur la valeur d’un paramètre de la loi.
Lorsque ce n'est pas le cas, on parle de test _non paramétrique_.


Pour les tests paramétriques, on distingue les _hypothèses simples_ qui fixent de façon unique la valeur d'un paramètre et les _hypothèses composites_ selon lesquelles les paramètres appartiennent à une région contenant au moins deux points.
:::

:::{prf:example} 
:class: dropdown
Pour les deux hypothèses statistiques que nous nous sommes fixés dans le cadre paramétrique des durées de vie des moteurs suivant des lois normales de même écart-type :
- $H_0$ : $m=m_0=3000$ est une hypothèse simple,
- $H_1$ : $m>m_0=3000$ est une hypothèse composite.

Nous choisissons (pour des raisons que nous verrons plus tard) de prendre comme statistique de test la moyenne empirique $\overline{x}$, et comme règle de décision

$$ \left\{\begin{matrix}
    \text{si } \overline{x}>\lambda_c& \text{on rejette }H_0\\
    \text{si } \overline{x}\leq\lambda_c& \text{on ne rejette pas}H_0
\end{matrix}\right.$$

Avec cette règle, on a que $]-\infty,\lambda_c[$ est la région d'acceptation, que $]\lambda_c, + \infty[$ est la zone de rejet, et $\{\lambda_c\}$ est la zone critique.
:::

