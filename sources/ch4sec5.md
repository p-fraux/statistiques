## Test d'hypothèse linéaire

$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

### Quantitées d'interet.

::::{prf:definition} Coefficient de corrélation multiple
  

 On appelle _coefficient de détermination_ la quantité 

$$ R^2 =\frac{Cov_{y,\hat{y}}}{S_y^2}= \frac{\sum_{i=1}^n(y_i-\overline{y})(\hat{y}_i-\overline{\hat{y}})}{\sum_{i=1}^n (y_i-\overline{y})^2}$$


On appelle _coefficient de corrélation multiple_ le coefficient R de corrélation linéaire entre la série $(y_1, y_2, ..., y_n)$ et la série ajustée $(\hat{y_1} , \hat{y_2},..., \hat{y_n})=X\hat{\theta}$ sa racine carré.



::::

::::{prf:proposition} Réecriture du coefficient de détermination
:class: dropdown  
Le coefficient de détermination $R^2$ se réécrit comme :

$$  \frac{\sum_{i=1}^n(y_i-\overline{y})(\hat{y}_i-\overline{\hat{y}})}{\sum_{i=1}^n (y_i-\overline{y})^2}=\frac{\sum_{i=1}^n (y_i-\overline{y})^2-\sum_{i=1}^n (y_i-\hat{y}_i)^2}{\sum_{i=1}^n (y_i-\overline{y})^2} = 1- \frac{\sum_{i=1}^n (y_i-\hat{y}_i)^2}{\sum_{i=1}^n (y_i-\overline{y})^2} $$
```{prf:proof}
Comme les numérateurs sont les mêmes, considérons uniquement les numérateurs. On peut écrire :

$$\sum_{i=1}^n(y_i-\overline{y})(\hat{y}_i-\overline{\hat{y}})= \sum_{i=1}^n(y_i-\overline{y})(\hat{y}_i-y_i+y_i-\overline{\hat{y}})$$
$$=\sum_{i=1}^n(y_i-\overline{y})(\hat{y}_i-y_i) +\sum_{i=1}^n(y_i-\overline{y})(y_i-\overline{\hat{y}})$$
$$= \left[\sum_{i=1}^n(y_i-\hat{y}_i)(\hat{y}_i-y_i) + \sum_{i=1}^n(\hat{y}_i-\overline{y})(\hat{y}_i-y_i) \right] + \left[ \sum_{i=1}^n(y_i-\overline{y})(y_i-\overline{y}) + (\overline{y}-\overline{\hat{y}})\sum_{i=1}^n(y_i-\overline{y})  \right]$$

Le vecteur $\hat{y}$ est la projection du vecteur $y$ sur l'espace engendré par les colonnes de X, et le vecteur $\begin{pmatrix}
1\\\vdots\\1
\end{pmatrix}$ appartient à cet espace. Par définition de la projection orthogonale, $\hat{y}-y$ est orthogonale à l'espace engendré par les colonnes de X, et donc en particulier au vecteur 
$\hat{y}- \overline{y}\begin{pmatrix}1\\\vdots\\1\end{pmatrix}$. 
    
C'est-à-dire que 

$$ \sum_{i=1}^n(\hat{y}_i-\overline{y})(\hat{y}_i-y_i)=0$$

Enfin, par définition de la moyenne empirique, 

$$(\overline{y}-\overline{\hat{y}})\sum_{i=1}^n(y_i-\overline{y})=0 $$

Donc nous avons bien

$$\sum_{i=1}^n(y_i-\overline{y})(\hat{y}_i-\overline{\hat{y}})=-\sum_{i=1}^n (y_i-\hat{y}_i)^2 + \sum_{i=1}^n (y_i-\overline{y})^2.$$
```
```{prf:remark} Interprétation
Le coefficient $R^2$ s’interprète comme la proportion de variabilité expliquée par la régression.

Géométriquement, R représente la valeur du cosinus de l’angle formé dans $\R^n$ entre $y − \overline{y}$ et $\hat{y} − \overline{y}$ où $\overline{y}$ désigne le vecteur de $\R^n$ dont toutes les coordonnées sont égales à $\overline{y}$.
Le coefficient $R^2$ est donc compris entre 0 et 1. Plus il est proche de 1 et meilleure est la régression.

```
::::
::::{prf:proposition} Réecriture de la variance d'un échantillon
:class: dropdown  
Avec le même argument que dans la preuve précédente, $\hat{y}-y$ et $\hat{y}-\overline{y}$ sont orthogonaux. En particulier, l'on peut utiliser le théorème de Pythagore pour écrire :

$$||y-\overline{y}||^2 = ||\hat{y}-y||^2 + || \hat{y}-\overline{y}||^2 $$

ce qui se développe en :

$$ \sum_{i=1}^n (y_i-\overline{y})^2 =\sum_{i=1}^n (y_i-\hat{y}_i)^2 + \sum_{i=1}^n (\hat{y}_i-\overline{y})^2$$

::::

::::{prf:definition}
 On appelle _somme des carrés d’écarts totale_ d'un échantillon, noté **ST** ou SST en anglais (pour (total sum of squares), la variance (biaisé) de l'échantillon : 
 
 $$\sum_{i=1}^n (y_i-\overline{y})^2 $$


On appelle _somme des carrés des erreurs_ (sous entendu de la régression linéaire) d'un échantillon, noté **SE** ou SSE en anglais (sum of squared errors), l'écart quadratique de la régression linéaire à l'échantillon : 

$$ \sum_{i=1}^n (y_i-\hat{y}_i)^2 $$

On appelle _somme des carrés de la régression_  d'un échantillon, noté **SR** ou SSR en aglais (regression sum of squares) les carrés de la régression de l'échantillon recentré : 

$$ \sum_{i=1}^n (\hat{y}_i-\overline{y})^2 $$

L'expression de la proposition précédente se réécrit alors 

$$\text{ST=SE +SR}$$

```{prf:remark}
Avec ces notations, $R^2= \frac{SR}{ST}$
```
::::



### Validation d'une régression linéaire

nous allons supposer que le bruit (la partie aléatoire du modèle) est gaussien, centré et de variance $\sigma^2$, c'est-à-dire que $U \sim \mathcal{N}(0,\sigma^2 I_n)$ ou encore que $\epsilon_i \sim \mathcal{N}(0,\sigma^2)$ et sont indépendants.

Résumons la situation de la section précédente


$$\begin{array}{|c|c|c|c|c|}
    \hline
    \text{Type de variation}& \text{Variable}  & \text{Somme des carrés} & \text{Dimension de l'espace de la} &  \text{Carrés} \\
    &\text{correspondante}&& \text{variable/ Degrés de libertés}& \text{moyens}\\ 
    \hline 
    \text{De la régression} & \hat{y}-\overline{y} & SR & J &  \frac{SR}{J}\\
    \text{Erreur dans la régression}  & y-\hat{y} & SE & n-J-1 &  \frac{SR}{n-J-1}\\
    \hline
    \text{Totale} & y-\overline{y} & ST & n-1 & \\
    \hline
\end{array}
$$



Nous voulons alors tester l'hypothèse 

$$H_0 : (a_1 =a_2 =···=a_J =0),$$
c'est-à-dire que la régression linéaire n'est pas significative.

Or, sous $H_0$, nous avons que $y=U \sim \mathcal{N}(0,\sigma^2 I_n)$ est une dilatation d'une gaussienne standard. Comme $\hat{y}$ est la projection orthogonale de $y$, nous allons pouvoir appliquer le théorème de Cochran :



::::{prf:proposition}
Sous l'hypothèse $H_0$, $\frac{SR}{J}$ et $\frac{SE}{N-J-1}$ sont indépendantes et de loi respective $\chi^2_{J}$ et $\chi^2_{n-J-1}$.
En particulier, 

$$ \frac{\frac{SR}{J}}{\frac{SE}{n-J-1}}$$

suit une loi de Fisher-Snedecor à J et n − J − 1 degrés de liberté (voir {ref}`Fisher-Snedecor`). 

Le test qui rejette $H_0$ si ce quotient dépasse le quantile d'ordre $1-\alpha$ de la loi de Fisher-Snedecor à J et n − J − 1 degrés de liberté est un test de risque $\alpha$.

```{prf:proof}
Il s'agit d'une application directe du théorème de Cochran {ref}`Cochran`.
```

::::