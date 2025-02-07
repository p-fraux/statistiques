(Lois-usuelles)=
## Lois Usuelles et leurs tabulations
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$



### Loi normale

Les lois normales sont centrales en probabilité et en statistiques. Nous renvoyons à la section {ref}`Rappel-Gaussienne` pour tous les rappels sur cette loi, et nous concentrerons ici sur l'intuition et la manipulation concrète des lois normales unidimensionnelles. Une loi normale est décrite par deux paramètres : la moyenne m, qui décrit la localisation de la variable, et la variance $\sigma^2$ qui décrit l'étalement autour de cette moyenne (où un $\sigma^2$ petit correspond à un étalement moindre).

```{figure} densite_normale.png
---
height: 400px
name: fig:densite_normale
---
Densité de lois normales
```



Lorsqu'on cherche à manipuler ou calculer des probabilités d'évènements "simple" (_i.e._ intersection fini d'évènements du type $X\in ]-\infty,a|$ ou de leurs complémentaires) pour des cas concrets, on pourra utiliser  la  table {ref}`fig:normale-centre-reduite-table`. Pour cela, il s'agit de commencer par se ramener à une loi normale centrée et réduite avant d'aller chercher dans la table la valeur de la probabilité.

```{figure} table-normal.png
---
height: 400px
name: fig:normale-centre-reduite-table
---
Table de la fonction de répartition d'une loi Normale centrée réduite
```

```{exercise}
:label: exer_externe
Une usine produit des bobines de fil électriques. Soit X la variable aléatoire qui à toute bobine extraite de la production associe sa longueur de fil en mètres. On suppose que X suit la loi normale d’espérance 50 et d’écart-type 0,2. 

a) Calculer la probabilité que la longueur du fil de la bobine soit inférieure à 50,19 .

b) Trouver à présent un écart $a>0$ tel que $95\% $ des bobines contiennent entre $50-a$ et $50+a$ mètres de fils.


:::{admonition} Solution a)
:class: dropdown
 On pose $Z=\frac{X-50}{0.2} \sim \mathcal{N}(0,1)$. On trouve alors

$$\mathbb{P}(X\leq 50.19) =\mathbb{P}(Z\leq 0.95)=0.8289$$

où l'on a lu la probabilité dans la $6^e$ colonne de la $10^e$ ligne ($\mathbb{P}(Z\leq 0.95)=F_Z(0.95)=F_Z(0.9+0.05)$).
:::

:::{admonition} Solution b)
:class: dropdown
Une fois la loi est centré $Z=\frac{X-50}{0.2} \sim \mathcal{N}(0,1)$, il y aura autant de chance de dépasser la longueur maximale que de ne pas atteindre la longueur minimale : 

$$\mathbb{P}(-b\leq Z\leq b) = 2\mathbb{P}(Z\leq b)-1.$$

Comme l'on veut 

$$0.95= \mathbb{P}(50-a\leq X\leq 50+a)=\mathbb{P}(-\frac{a}{0.2}\leq Z\leq \frac{a}{0.2}) = 2\mathbb{P}(Z\leq \frac{a}{0.2})-1 = 2 F_Z(\frac{a}{0.2})-1 ,$$

on doit chercher l'antécédent pour la fonction de répartition de $0.975$. On trouve $1.96$ comme valeur, il faut donc prendre $a= 1.96*0.2=0.392 m$.
:::

```

```{exercise}
:label: exer03
Julie habite en face du métro. Elle part de chez elle 25 min avant le début de ses cours à l’INP.

Son temps d’attente du métro suit une loi normale d’espérance 5 et d’écart type 3 et la durée de son trajet ensuite suit une loi normale d’espérance 15 et d’écart type 4. Une fois au pied de l'ENSEEIHT, elle met 1 min à rejoindre sa salle de cours.

On suppose que le temps d’attente du métro et le temps de trajet sont indépendants. Pour répondre aux questions, l'on pourra se servir de la table {ref}`fig:normale-centre-reduite-table`.

a) Donner la loi du temps total de trajet de Julie.

:::{admonition} Solution a)
:class: dropdown
Le temps total de trajet $X$ de Julie suit une loi normale, d'espérance 21 et de variance 25.

:::

b) Ce matin Julie a un cours de Statistiques, quelle est la probabilité qu’elle arrive à l’heure ? qu’elle ait plus de 5 minutes de retard ?

:::{admonition} Solution b)
:class: dropdown
On sait que $Z= \frac{X-21}{5}$ suit une loi centrée réduite. En regardant dans la table, l'on trouve
        
$$\mathbb{P}(X\leq 25)=\mathbb{P}(Z\leq \frac{4}{5})\approx 0.7881 $ et $\mathbb{P}(X\geq 30)=\mathbb{P}(Z\geq \frac{9}{5})\approx 1-0.9641.$$

:::

c) Sur un semestre, elle effectue 80 trajets pour venir à la faculté. On note $X_1, X_2, . . . , X_{80}$ les 80 variables aléatoires représentants les temps de parcours de Julie pour ces trajets.
Quel est le nom et la loi de la variable aléatoire Y représentant son temps moyen de parcours pour
aller de chez elle à l'INP ?

:::{admonition} Solution c)
:class: dropdown
Il s'agit de la moyenne empirique, de loi $\mathcal{N}(21,\frac{25}{{80}})$.

:::

d) Quelle est la probabilité que, sur un semestre, elle passe plus de 27h30min en trajet pour venir à la ENSEEIHT (temps d’attente et de transport




:::{admonition} Solution d)
:class: dropdown
Il s'agit de calculer 

$$\mathbb{P}(Z_2\geq \frac{27.5\times 60-80\times 21}{5\times \sqrt{80}})\approx 0.7454 .$$

:::

```


### Loi du $\chi^2$


```{prf:definition} Loi du $\chi^2$
Soit Y une variable aléatoire réelle, $k\in \N^*$ un entier et $X=(X_1,...,X_k)^t$ un vecteur gaussien standard. Les deux propositions suivantes sont équivalentes. Lorsqu'elles sont vérifiées, on dit que Y suit une loi du $\chi^2_k$.
- Y suit une loi $\gamma(\frac{k}{2},\frac{1}{2})$, loi absolument continue par rapport à la mesure de Lebesgue de densité 

$$ g_{\frac{k}{2},\frac{1}{2}} : x\mapsto \frac{x^{\frac{1}{2}(k-2)}e^{-\frac{x}{2}}}{2^{\frac{k}{2}}\Gamma(\frac{k}{2})}{1}_{\R^+}(x)$$

- Y suit la même loi que la variable $\sum_{i=1}^k X_i^2$, somme de k variables gaussiennes indépendantes centrées et réduites. 

:::{prf:proof}
Rappelons que pour deux lois gamma indépendantes $X\sim \gamma(p,\lambda)$ et $Y\sim \gamma(q,\lambda)$, alors $X+Y \sim \gamma(p+q,\lambda).$ Ceci se montre soit en passant par la fonction caractéristique, soit directement par le calcul d'un produit de convolution.

Un changement de variable montre que le carré d'une gaussienne unidimensionnelle centré réduite suit une loi $\gamma(\frac{1}{2}, \frac{1}{2})$, ce qui permet de conclure.

:::

```

```{figure} densite_chi_2.png
---
height: 400px
name: fig:densite_chi_2
---
Densité de lois du $\chi^2$ pour divers degrés de libertés.
```




Comme pour la loi normale, la loi du $\chi^2$ est tabulé :

```{figure} Chi-Square-table.png
---
height: 400px
name: fig:Chi-Square-table
---
Table des valeurs critiques pour des lois de $\chi^2$
```



### Loi de Student

De manière similaire, l'on peut prendre plusieurs routes pour définir les lois de Student. 

```{prf:definition} Loi du $\chi^2$
Soit $Z$ une variable aléatoire réelle et pour $n\in \N$, $X\sim \mathcal{N}(0,1)$ et $Y\sim \chi^2_n$. Les deux propositions suivantes sont équivalentes. Lorsqu'elles sont vérifiées, on dit que Z suit une loi de Student à n degré de liberté (abrégé en d.d.l.).

- La loi de Z et absolument continue par rapport à la mesure de Lebesgue, de densité 

$$ g_{Z} : x\mapsto \frac{\Gamma(\frac{n+1}{2})}{\sqrt{n\pi}\Gamma(\frac{n}{2}) } \left(1+\frac{t^2}{n}\right)^{-\frac{n+1}{2}}$$

- Z suit la même loi que la variable $\frac{X}{\sqrt{\frac{Y}{n}}}$.

```


```{figure} densite_Student.png
---
height: 400px
name: fig:densite_Student
---
Densité de lois de Student pour divers degrés de libertés
```

:::{prf:property}
:class: dropdown
Soit Z une variable suivant une loi de Student à n degré de liberté.

Si $n>1$, alors $\mathbb{E}(Z)=0$

Si $n>2$, alors $V(Z)=\frac{n}{n-2}$ 

::::{prf:proof} 
Les conditions sur n sont là pour assurer l'existence des moments.

Pour calculer l'espérance, nous pouvons prendre la première définition et remarquer que la densité est paire.

Pour calculer la variance, l'on pourra remarquer que si $z_k$ suivent des lois de Student à k degré de liberté

$$g_{Z_n}(t)+ \frac{1}{n} t^2g_{z_n}(t)=(1+\frac{t^2}{n})g_{z_n}(t)=\frac{\sqrt{n-1}}{\sqrt{n}} \frac{\Gamma (\frac{n+1}{2})\Gamma (\frac{n-2}{2})}{\Gamma (\frac{n}{2})\Gamma (\frac{n-1}{2})}   g_{z_{n-2}}\left(\frac{t\sqrt{n-1}}{\sqrt{n}}\right), $$

avant d'effectuer un changement de variable et d'utiliser la relation fonctionnelle de $\Gamma$ pour conclure.
::::

:::


On retrouve encore la table des quantiles d'une loi de Student :

```{figure} table_student.png
---
height: 400px
name: fig:tableStudent
---
Tabulation des quantiles des lois de Stendent
```

:::{prf:observation}
:class: dropdown
```{figure} t_distribution.png
---
height: 300px
---
Si les données échouent au test t de l'enseignant, vous pouvez simplement les forcer à repasser le test jusqu'à ce qu'elles réussissent.

(crédit https://xkcd.com/1347/)
```

:::



(Fisher-Snedecor)=
### Loi de Fisher-Snedecor

L'on suit encore une fois le même parcours pour présenter les lois de Fisher-Snedecor. 

```{prf:definition} Loi de Fisher-Snedecor
Soit $Z$ une variable aléatoire réelle et pour $(n,m)\in \N^2$, $X\sim \chi^2_n$ et $Y\sim \chi^2_m$. Les deux propositions suivantes sont équivalentes. Lorsqu'elles sont vérifiées, on dit que Z suit une loi de Fisher-Snedecor à n et m degré de liberté (abrégé en d.d.l.).

- La loi de Z et absolument continue par rapport à la mesure de Lebesgue, de densité 
$$ g_{Z} : x\mapsto \frac{\Gamma(\frac{n+m}{2}) n^{\frac{n}{2}}m^{\frac{m}{2}}}{\Gamma(\frac{n}{2})\Gamma(\frac{m}{2})}
    \frac{x^{\frac{n}{2}-1}}{(nz+m)^{\frac{n+m}{2}}} {1}_{\R^+}(x)$$
    
- Z suit la même loi que la variable $\frac{X/n}{Y/p}$.

```


```{figure} densite_Fisher-Snedecor.png
---
height: 400px
name: fig:densite_Fisher-Snedecor
---
Densité de lois de Fisher-Snedecor pour divers degrés de libertés
```

:::{prf:property}
:class: dropdown
Soit Z une variable aléatoire de loi de Fisher-Snedecor à n et m degrés de libertés. 

Alors si $m>2$, $\mathbb{Z}=\frac{m}{m-2}$ et si $m>4$, $V(Z)= 2\frac{m^2(m+n-2)}{n(m-2)^2(m-4)}$

:::


On retrouve encore la table des quantiles d'une loi de Student :

```{figure} Table-Fisher.jpg
---
height: 400px
name: fig:quantile-fisher
---
Quantile d'ordre 95% d'une loi de Fisher-Snedecor
```






### Loi de Kolmogorov

Il s'agit d'une famille de loi très pratique pour les tests adéquation de loi. 

```{prf:definition}  Loi de Kolmogorov
Pour $n \in \N^*$, la loi de Kolmogorov est celle de la variable aléatoire 

$$\sup_{t\in[0,1]} |\frac{Card(U_i\leq t)}{n} - t|$$

où $(U_i)$ est une famille de variable aléatoire indépendante de loi uniforme sur $[0,1]$. 

```


Le plus important à retenir est que cette loi est tabulé :

```{figure} Kolmogorov-Smirnov_Table.jpeg
---
height: 400px
name: fig:quantile-Kolmogorov
---
Quantile de niveau $1-\alpha$ des lois de Kolmogorov
```

