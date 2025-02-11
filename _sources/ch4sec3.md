## Test d'égalité de variance et de moyenne
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$


On considère $(X_1,...,X_{n_1})$ un échantillon de taille $n_1$ d’une loi normale $\mathcal{N}(m_1,\sigma_1^2)$ et $(Y_1,...,Y_{n_2})$ un échantillon de taille $n_2$ d’une loi normale $\mathcal{N}(m_2,\sigma_2^2)$.
On suppose de plus que $(X_i, Y_j)$ sont indépendants dans leur ensemble. Les paramètres $m_1,m_2,σ_1,σ_2$ sont inconnus, mais nous souhaitons tester la "ressemblance" de la loi de X avec celle de Y. Pour cela, nous allons tester l'égalité des paramètres Espérance et Variance.

### Test d'égalité des variances

L'on veut donc tester 

$$H_0 : \sigma_1^2=\sigma_2^2 \qquad \text{ contre } \qquad H_1 : \sigma_1^2 \neq \sigma_2^2.$$

On pose

$$ S_1^2 = \frac{1}{n_1-1} \sum_{i=1}^{n_1} (X_i-\overline{X})^2 \qquad \text{ avec } \overline{X}=\frac{1}{n_1}\sum_{i=1}^{n_1} X_i$$

et

$$ S_2^2 = \frac{1}{n_2-1} \sum_{j=1}^{n_2} (Y_j-\overline{X})^2 \qquad \text{ avec } \overline{X}=\frac{1}{n_2}\sum_{j=1}^{n_2} Y_j.$$

Enfin, on définit 

$$ Stat=\frac{S_1^2}{S_2^2}.$$

:::{prf:proposition}
Pour $k\in \{1,2\}$ on a que 

$$ \frac{1}{\sigma_k} S_k^2 \sim \chi^2_{n_k-1}.$$

Alors

$$\frac{\sigma_2^2}{\sigma_1^2} Stat$$

a la même loi que le rapport de deux lois du $\chi^2$ avec respectivement $n_1-1$ et $n_2-1$ degrés de liberté : la loi de Fisher-Snedecor ({ref}`Fisher-Snedecor`) noté $\mathcal{F}_{n_1-1, n_2-1}$. 

Sous $H_0$, le rapport des variances disparait car égal à 1.
:::


:::{prf:definition} Test d'égalité des variances
Notons $\mathcal{F}_{n,p;\alpha}$ le quantile d’ordre $\alpha $ de la loi $\mathcal{F}_{n,p}$. 

Nous rejetterons $H_0$ si 

$$ Stat > \mathcal{F}_{n_1-1,n_2-1;1-\alpha}$$
$$\text{(ou suivant les connaissances antérieures si} \quad Stat < \mathcal{F}_{n_1-1,n_2-1;\alpha}). $$

Nous admettrons que ce test est le test le plus puissant parmi tous les tests de niveau $\alpha$ (_test uniformément plus puissant_ U.P.P. ou U.M.P en anglais).

:::

```{admonition} Limitations du test
:class: hint, dropdown
Une critique principale de ce test est sa sensibilité à la non-normalité des variables $X,Y$ (l'on dit que le test n'est pas robuste). C'est pour cela que les statisticiens ont développé des alternatives comme le test de Bartlett ou le test de Levene.
```

### Test d'égalité des moyennes

On considère à présent que l'on sait que les variances des deux échantillons sont égales (par exemple en effectuant le test précédent), et l'on veut alors tester lorsque $\sigma_1^2=\sigma_2^2= \sigma^2$ l'hypothèse

$$H_0 : m_1=m_2 \qquad \text{ contre } \qquad H_1 : m_1\neq m_2.$$



:::{prf:definition} Test d'égalité des moyennes
On construit le test d'égalité à l'aide des quantiles de la loi de Student, car

$$ \frac{\overline{X}-\overline{Y}}{\sqrt{\frac{1}{n_1}+\frac{1}{n_2}} \cdot \sqrt{\frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}}} =
\frac{\frac{\overline{X}-\overline{Y}}{ \sqrt{\frac{1}{n_1}+\frac{1}{n_2}}}}
{\sqrt{\frac{Z}{n_1+n_2-2}}} \sim \text{ Student à } (n_1+n_2-1) \text{ d.d.l.}$$

En effet, d'après le théorème de Cochran ,

$$\frac{\overline{X}-\overline{Y}}{\sigma} \sim \mathcal{N}(m_1-m_2, \frac{1}{n_1}+\frac{1}{n_2})$$
$$Z=\frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{\sigma^2}  \sim \chi^2_{n_1+n_2-2} \text{ comme somme de deux variables indépendante de loi du }\chi^2,$$

et comme les moyennes empiriques sont indépendantes des variances empiriques, l'on a la loi de la statistique.


Si l'on prend la zone de rejet symétrique, ce test est le test le plus puissant parmi tous les tests de niveau $\alpha$.
:::

```{exercise}
:label: exer17
On considère un système électronique, alimenté par une source continu de tension x connue. On observe à la sortie une tension Y. Nous supposerons que Y peut s'écrire de la forme

$$ Y=ux+v+ A$$

Avec $A \sim \mathcal{N}(0,\sigma^2)$. On désire estimer les valeurs de $u$ et $v$. Pour cela, on mesure les valeurs $y_j$ de Y pour diverses valeurs $x_j$ de X. Ces valeurs sont "entachées" des erreurs $A_j$.

a) On effectue ces mesures à Yaoundé (Cameroun) par $30°C$. En supposant que les $A_j$ soient issus de tirages indépendants, déduire du tableau suivant les estimations $\hat{U}$ et $\hat{V}$ de u et v.

$$\begin{array}{|c|c|c|c|c|c|c|c|c|c|}
            \hline
             x_j :&5 &7 &9 & 11 &13 &15& 17 &19 & 21  \\
             \hline 
             y_j :& 6 &8&9.6&9.1&10&10.4&13.7&14.1&14.6\\
             \hline
        \end{array}$$


:::{admonition} Solution a)
:class: dropdown
On sait que les estimateurs pour une variable explicative sont :

$$\hat{u_1}= \frac{Cov(x,y)}{\tilde{S_x}^2} \qquad \hat{v_1} =\overline{y} -\hat{u_1}\overline{x}$$

Et ici nous trouvons 

$$\hat{u_1}= 0.52 \qquad \hat{v_1} =3.87$$
:::


b) On refait à présent ces mesures au Pôle Nord par $-30°C$. Avec les mêmes hypothèses, déduire les estimations $\hat{U}$ et $\hat{V}$ de u et v. Quel remarque peut-on faire ?

$$\begin{array}{|c|c|c|c|c|c|c|c|c|c|}
            \hline
             x_j :&2 &4 &6 & 8 &10 &12& 14 &16   \\
             \hline 
             y_j :& 8 &8&10.5&10.1&12.8&12.8&13.1&14.2\\
             \hline
        \end{array}$$

:::{admonition} Solution b)
:class: dropdown
On trouve :

$$\hat{u_2}= 0.47 \qquad \hat{v_2} =6.98$$

si l'estimateur de U reste proche, celui de V change beaucoup. La valeur moyenne semble beaucoup impactée par la température, mais sa réponse au signal l'est peu. Nous allons essayer de le montrer
:::

c)  Donner un estimateur de la variance $\sigma$ du bruit. Le calculer pour les deux séries de mesure.

_On pourra démontrer ou utiliser le fait que pour une estimation $\hat{Y}$ de Y par la méthode des moindres carrés avec bruit gaussien par J paramètres $X_i$ sur n mesures, $Y-\hat{Y}$ suit une loi normale de dimension (n-J-1)_

:::{admonition} Solution c)
:class: dropdown
En reprenant les notations de la démonstration de la preuve des moindres carré, 
        $Y-\hat{Y}=(X(X^tX)^{-1}X^t - I_n)A$. 

Or la matrice $X(X^tX)^{-1}X^t - I_n$ est la matrice de projection sur l'orthogonal de l'espace des colonnes de X. Donc le théorème de Cochran montre l'indication.

On peut alors estimer la variance du bruit avec la variance empirique de ce vecteur.

Pour la première série, on trouve

$$\hat{\sigma_1}^2 := \frac{1}{n-2}\sum_{i=1}^n(y_i-\hat{u_1}x_i-\hat{v_1})^2 =0.69 $$

$$\hat{\sigma_2}^2 =0.539 $$
:::

d) Montrer avec un test adapté que l'on peut supposer que les deux séries ont la même variance du bruit (ce qui revient à tester que les mesures ont la même précision) avec un risque de $5\%$. L'on pourra s'aider des tables du chapitre {ref}`Lois-usuelles`.

:::{admonition} Solution d)
:class: dropdown
On sait déjà (encore avec le théorème de Cochran) que $(n_i-2)\frac{\hat{\sigma^2_i}}{\sigma_i^2}$ suit une loi du $\chi^2$ à $n_i-2$ degré de liberté.

On veut tester $H_0 : \sigma^2_1=\sigma^2_2 $ contre l'alternative.


Sous $H_0$, on peut donc faire un test d'égalité de variance, puisque alors $\frac{(n_2-2)\sigma_2^2}{(n_1-2)\sigma_1^2}$ suit une loi de Fisher-Snedecor à  $n_2-2=6$ et $n_1-2=7$ degrés de libertés.

On trouve ici $\frac{(n_1-2)\sigma_1^2}{(n_2-2)\sigma_2^2}= 1.49$. 

Avec la table {ref}`fig:quantile-fisher`, l'on trouve le quantile $q_{1-\alpha}=3.87$. 

On ne peut donc pas rejeter l'hypothèse, à un risque de 5\% que 

$$\sigma^2_1=\sigma^2_2 $$
        
:::

e)  Étudier avec des tests d'égalité de moyenne si les valeurs de u sont les mêmes pour les deux séries de mesures.

_Vous pourrez admettre que $\hat{U}\sim \mathcal{N}(u,\frac{\sigma^2}{n})$_

:::{admonition} Solution e)
:class: dropdown
Nous voulons tester $H_0 : u_1=u_2$ contre l'alternative.

Nous savons que $\hat{u_i}\sim \mathcal{N}(u_i,\frac{\sigma}{n_i})$.

En particulier, 

$$\hat{u_1}-\hat{u_2} \sim \mathcal{N}(u_1-u_2,\sigma(\frac{1}{n_1}+\frac{1}{n_2}))$$

$$\frac{(n_1-2)\hat{\sigma}_1+ (n_2-2)\hat{\sigma}_2}{\sigma^2} \sim \chi_{n_1+n_2-4}^2$$

Donc sous $H_0$, l'on a que 

$$ \frac{\hat{u_1}-\hat{u_2} }{\sigma \sqrt{\frac{1}{n_1}+\frac{1}{n_2}}}\sim \mathcal{N}(0,1)$$

Et donc que

$$S=\frac{\hat{u_1}-\hat{u_2} }{\sqrt{\frac{1}{n_1}+\frac{1}{n_2}}\sqrt{\frac{(n_1-2)\hat{\sigma}_1+ (n_2-2)\hat{\sigma}_2}{n_1+n_2-4}}} \sim t_{n_1+n_2-4} \text{ loi de Student à } n_1+n_2-4 \text{ degrés de libertés.}$$
 
_Loi du rapport d'une loi normale par la racine d'une loi d'une variable du $\chi^2_n$ divisé par son nombre de degrés de liberté_. 

Pour l'échantillon, $S=0.0308$. le quantile d'ordre 0.975 (car nous cherchons une région de rejet pour un test bilatéral d'une loi symétrique) pour une loi de Student à 13 degrés de liberté est 1,1604.

Comme $-1.1604\leq S \leq 1.1604$, nous ne pouvons pas rejeter $H_0$ avec un risque de 5\%.
:::

f) Étudier avec des tests d'égalité de moyenne si les valeurs de v sont les mêmes pour les deux séries de mesures.

_Vous pourrez admettre que $\hat{V}\sim \mathcal{N}\left(v,\frac{\sigma^2}{n}(1+\frac{\overline{x}_i^2}{S_{x_i}^2})\right)$_.

:::{admonition} Solution f)
:class: dropdown
 Comme pour la question précédente, nous voulons tester $H_0 : v_1=v_2$ contre l'alternative.

Nous savons que $\hat{v_i}\sim \mathcal{N}\left(v_i,\frac{\sigma^2}{n_i}(1+\frac{\overline{x}^2}{S_X^2})\right)$.

Avec le même raisonnement qu'à la question précédente, l'on trouve que 

$$S'=\frac{\hat{v_1}-\hat{v_2} }{\sqrt{\frac{1}{n_1}(1+\frac{\overline{x}_1^2}{S_{X_1}^2})+\frac{1}{n_2}(1+\frac{\overline{x}_2^2}{S_{x_2}^2})}\sqrt{\frac{(n_1-2)\hat{\sigma}_1+ (n_2-2)\hat{\sigma}_2}{n_1+n_2-4}}} \sim t_{n_1+n_2-4}$$

Pour l'échantillon, $S'=-3.31$. 

Comme $S'\notin [-1.1604 ; 1.1604]$, nous rejetons $H_0$ avec un risque de 5\%.
:::

```
 
 




