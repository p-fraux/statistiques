## Erreurs et courbe ROC

### Erreurs et incertitude
Dans un monde réel, à information partielle, il est illusoire d'espérer obtenir la "bonne" réponse à chaque fois. Ceci est en particulier vrai pour les tests. L'avantage des tests est qu'ils peuvent être conçus pour connaitre la probabilité d'erreur, suivant la réalité.

:::{prf:definition} Espèce d'erreur
:class: dropdown
L'_erreur de première espèce_ consiste à rejeter $H_0$ à tort lorsque les données sont des tirages d'une loi qui vérifie l'hypothèse nulle.

Pour $\mathbb{P}$ vérifiant $H_0$, on appelle _risque de première espèce_ (sous-entendu vis-à-vis de $\mathbb{P}$) la probabilité sous cette loi de rejeter $H_0$.

$$ \phantom{a}$$

L'_erreur de seconde espèce_ consiste à ne pas rejeter $H_0$ lorsque les données sont des tirages d'une loi qui vérifie l'hypothèse alternative.

Pour $\mathbb{P}$ vérifiant $H_1$, on appelle _risque de seconde espèce_ (sous-entendu vis-à-vis de $\mathbb{P}$) la probabilité sous cette loi de ne pas rejeter $H_0$.

$$ \phantom{a}$$

De manière plus générale, on appelle _puissance_ du test pour la loi $\mathbb{P}$ (vérifiant $H_0$ ou $H_1$) la probabilité sous ce test de rejeter $H_0$.

On appelle _niveau_ du test le suppremum du risque de première espèce sur toutes les lois vérifiant $H_0$.
:::

_En traitement du signal, un deuxième nom du risque de première espèce est la probabilité de fausse alarme._


Si l'on fait un tableau pour résumer, on trouve :

$$
\begin{array}{|c|c c c|}
 \hline
 &
 \text{Etat réel}  &&
 ( \text{vraie probabilité})\\
&
 \text{La loi vérifie } H_0  &| & \text{La loi vérifie }H_1 \\
\hline
 \text{Test ne rejette pas }H_0 & 1-{\color{red} \alpha} &|& {\color{blue}\beta}  \\
\hline
\text{Test rejette }H_0 & {\color{red} \alpha} &|&  1-{\color{blue}\beta}     \\
\hline
\end{array}
$$

avec $\alpha$ le risque de première espèce, $\beta$  le risque de seconde espèce et  $1-\beta$  la puissance du test.

:::{prf:remark}
:class: dropdown
Être dans la zone d'acceptation ne signifie pas que $H_0$ est vraie, mais seulement que les observations dont on dispose ne sont pas incompatibles avec cette hypothèse et que l’on n’a pas de raisons suffisantes de lui préférer $H_1$ au vu des résultats expérimentaux. C'est pour cela que nous préférons l'appellation _ne pas pouvoir rejeter $H_0$_ à _accepter $H_0$_.
:::


:::{admonition} Principe d'incertitude
:class: dropdown
Il n'est en général pas possible de minimiser à la fois le niveau de test et le risque de seconde espèce.

En effet, une telle optimisation n'est possible que s'il est possible de faire un test qui ne se trompe jamais, et donc que si aucune des lois vérifiant $H_0$ prend avec probabilité positive des valeurs qu'une des lois vérifiant $H_1$ peut prendre avec probabilité positive (c'est-à-dire si les lois ont des supports disjoints).

Pour se forger une intuition du phénomène, considérons le problème suivant. Nous voulons tester un échantillon suivant une loi supposée normale d'écart-type connu pour donner sa valeur entre deux hypothèses. Nous choisissons alors une statistique de test et une région de rejet, disons $\overline{x}$ et une zone de la forme $\overline{x}>\mu_a$. Utilisons alors le graphique suivant :

```{figure} test_normal.png
---
height: 300px
---
Illustrations des diverses zones dans un test sur des moyennes de loi normales
```

Sous $H_0$, la probabilité de dépasser $\mu_a$, et donc de se tromper sur la réalité avec une erreur de première espèce, est égale à l'aire en rouge. De même, l'aire en bleue est égale au risque de seconde espèce.
:::



### Courbe ROC et évaluation AUC de tests

:::{prf:definition} Courbe ROC

On appelle courbe ROC d'un test (donné par une statistique et un ensemble de région de rejet des divers niveaux $\{I_\alpha\}$) la courbe représentative de la puissance du test en fonction du niveau du test.

::::{admonition} Origine historique 
:class: dropdown
Connaitre la puissance d'un test en fonctions de la précision demandé est un élément central. C'est pour cette raison que les ingénieurs électriques et radar, en charge de la détection en terrain hostile, ont développé un outil graphique pour le décrire : la courbe ROC (Receiver Operating Characteristic). Cet outil a depuis trouvé des applications en médecine, en radiologie, en prévision de catastrophes naturelles et en météorologie. 

::::

:::



::::{prf:property} Comparaison de courbe ROC
:class: dropdown
Si un premier test à une courbe ROC en dessous d'un autre, alors pour tout niveau $\alpha$, le deuxième test est plus puissant.

Si la courbe ROC d'un test est sous la bissectrice  $y=x$, alors passer au complémentaire des zones de rejet permet d'obtenir un test plus puissant.

Un test dont la courbe ROC est la bissectrice est aussi efficace qu'un test ignorant les données et tirant un résultat au hasard.


:::{prf:proof} 
Le premier point est immédiat avec la définition de la courbe.

$\phantom{a}$

Pour le deuxième point, notons $I_\alpha$ la zone de rejet de niveau $\alpha$ et $\pi_1(\alpha)$ la puissance du test.

Alors en notant $\pi_2$ la puissance du test obtenu en passant au complémentaire, l'on trouve :

$$\mathbb{P}(X\notin I_\alpha | H_1)=1-\alpha $$

donc

$$\pi_2(1-\alpha) = \mathbb{P}(X\notin I_\alpha | H_1)=1-\pi_1(\alpha).$$ 

Nous pouvons réécrire cela comme $\pi_2(\alpha) =1-\pi_1(1-\alpha)$, ou encore que la nouvelle courbe ROC est toujours au dessus de la bissectrice (car il s'agit de la symétrique de l'ancienne autour du 0.5,0.5), donc plus puissante.

$\phantom{a}$

Enfin, pour un niveau $\alpha$ donné, un test suivant une Bernoulli (indépendante des données) de paramètre $\alpha$ est bien de niveau $\alpha$ et de puissance $\alpha$. Sur la bissectrice, l'on n'est pas mieux que le hasard.

:::

::::


:::{prf:definition} AUC
On appelle aire sous la courbe (sous-entendu d'un test), ou AUC, l'aire sous la courbe ROC. 

::::{admonition} Intérêt et justification
:class: dropdown
Ce nombre permet de resumer la courbe ROC, et donc la qualité d'un test.

Un test qui se trompe toujours sous l'alternative a une AUC de 0, s'il n'est pas meilleur que le hasard, il aura une AUC de 0.5 et s'il ne se trompe jamais sous l'alternative son AUC vaudra 1.
::::

:::


:::{prf:example} Un cas d'utilisation en médecine
:class: dropdown
Nous allons nous interesser au papier de médecine de 2001 intitulé _Head-to-head comparison of N-terminal pro-brain natriuretic
peptide, brain natriuretic peptide and N-terminal pro-atrial
natriuretic peptide in diagnosing left ventricular dysfunction_,  écrit par **Angelika Hammerer-Lercher, Elke Neubauer, Silvana Muller, Otmar Pachinger, Bernd Puschendorf, Johannes Mair**.

Les auteurs cherchent alors à comparer trois test de détection d'une anomalie médicale. Après les mesures, ils les regroupent dans le graphique suivant :

```{figure} ROC-medecine.png
---
height: 300px
---
Courbe ROC comparant trois tests pour la détection de l'anomalie LVEF.
```

On reconnait trois courbe ROC avec en abscisse la _specificity_ (ou erreur de première espèce) et en ordonné la _sensitivity_ (ou puissance) du test.

Dans les résultats du papier de médecine, l'on peut lire :

_ROC analysis showed that among the evaluated
natriuretic peptides, BNP had the best diagnostic
performance to detect patients with [...] LVEF. The area under curve AUC was greater than those of the NT-natriuretic peptides.[...] The current results concur with our previous findings, demonstrating that BNP was a superior marker compared with ANP, NT-ANP, and cGMP
for the identification of patients with asymptomatic
LVD._


Les auteurs utilisent ainsi la notion d'aire sous la courbe pour comparer au mieux les trois tests qui les intéressent, et conclure.
:::

:::{admonition} Méthode de construction empirique de courbe ROC :
:class: tip
Bien souvent, l'ingénieur est plus intéressé par la construction de telles courbes ROC pour des données réelles. Pour ce faire, il suivra la méthodologie suivante :

- Pour un grand nombre de $\alpha$ répartit sur $[0,1]$, déterminer les zones de rejet (par exemple déterminer $\mu_\alpha$ pour des zones de la forme $]-\infty,\mu_\alpha]$). Pour cela, soit nous connaissons les lois sous $H_0$ et nous faisons un calcul théorique ; soit nous n'avons accès qu'à un grand nombre de tirages suivant des lois de $H_0$ et utilisons alors les quantiles empiriques.
- Effectuer un grand nombre de tirages vérifiant $H_1$ et utiliser les fréquences empiriques pour estimer la puissance du test de niveau $\alpha$.
- Tracer alors la fonction en escalier (ou affine par morceau) avec des sauts sur les diverses valeurs de $\alpha$ évalués.
- (Pas systématique) Tracer les intervalles de confiance associés à la construction, obtenu pour des très grands ensembles de données par des intervalles de confiance de loi normales.
:::


