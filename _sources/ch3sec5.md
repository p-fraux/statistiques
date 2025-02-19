## Tests de proportion

### Le cas de base
On considère une expérience aléatoire où l’issue se ramène à « succès ou échec », c'est-à-dire une expérience qui peut se modéliser avec une expérience de Bernoulli. Par exemple,

- On a obtenu pile lors d’un lancer ;
- Le composant électronique testé fonctionne ;
- L’électeur sondé vote oui au référendum.


On note $p$ la probabilité de succès lors de l’expérience. On veut tester une des trois options suivantes :


$$\left\{ \begin{matrix}
    H_0 &:& p=p_0\\ \text{contre}&& \\ H_1 &:& p>p_0 \qquad \text{ test unilatéral à droite}\\
    &ou& p<p_0 \qquad \text{ test unilatéral à gauche}\\
    &ou& p\neq p_0 \qquad \text{ test bilateral}
\end{matrix}\right. $$


On répète n fois (dans des conditions identiques et indépendantes) l’expérience aléatoire. On note $X_n$ le nombre de succès obtenus. On sait que $X_n \sim \mathcal{B}in(n,p)$. On sait déjà, d'après la loi des grands nombres, que 

$$\frac{X_n}{n} \overset{p.s.}{\to} p.$$

On peut utiliser la vitesse de convergence donnée par le théorème central limite :

$$\frac{X_n-np}{\sqrt{n p(1-p)}} \overset{Loi}{\to} \mathcal{N}(0,1)$$

En effet, si cela ne nous donne malheureusement pas encore une statistique, sous $H_0$ l'on aura 

$$Z_n:=\frac{X_n-np
_0}{\sqrt{n p_0(1-p_0)}} \overset{Loi}{\to} \mathcal{N}(0,1)$$

On pourra alors pour notre test comparer $Z_n$ à une valeur critique, fonction du risque de $1^{re}$ espèce choisi. Pour que cette approximation soit valide, il faut prendre n suffisamment grand ($n\geq 30$) et éviter les proportions $p$ trop faibles ou trop importantes ($np_0>5$ ou $n(1-p_0)>5$).

Pour décrire cette valeur critique, nous pouvons utiliser la fonction quantile de la loi normale (que l'on pourra trouver dans des tables numériques) $q_\alpha$. Cette fonction est l'inverse de la fonction de répartition d'une loi normale centré réduite, c'est-à-dire que pour $Z\sim \mathcal{N}(0,1)$, 

$$\mathbb{P}(Z<q_\alpha)=\alpha.$$

En fonction du type d'hypothèse que l'on souhaite tester, on choisira à priori une région d'acceptation différente :

- Pour le test _unilatéral à droite_, on s'attend à ce que sous l'hypothèse alternative, la statistique soit plus la statistique soit plus grande. On choisit donc de _rejeter $H_0$ si $Z_n>q_{1-\alpha}$_.
- Pour le test _unilatéral à gauche_, on s'attend à ce que sous l'hypothèse alternative, la statistique soit plus petite. On choisit donc de _rejeter $H_0$ si $Z_n<q_{\alpha}$_.
- Enfin, pour le test _bilatéral_, on n'a pas de raison de préférer une direction, et l'on prend donc une zone d'acceptation symétrique. On choisit donc de _rejeter $H_0$ si $q_{\frac{\alpha}{2}}>Z_n$ ou si $Z_n>q_{1-\frac{\alpha}{2}}$_.


### Une généralisation : le test d'égalité de proportion

Il arrive souvent que ce qui nous intéresse n'est pas la valeur exacte de la proportion, mais la comparaison de la proportion entre deux échantillons. Quelques exemples de cela :

- Lorsqu'on veut étudier l'évolution d'une proportion ;
- Lorsqu'on veut savoir si un phénomène à un impact sur la variable d'intérêt (est-ce qu'un médicament a un effet supérieur à du placebo ?) ;

Nous avons alors deux séries $(X_i)\sim B(p_1)$ et $(Y_i)\sim B(p_2)$, supposé indépendants, et nous voulons tester l'hypothèse 

$$\left\{ \begin{matrix}
    H_0 &:& p_1=p_2\\ \text{contre}&& \\ H_1 &:& p_1>p_2 \qquad \text{ test orienté de comparaison des proportions.}\\
    &ou& p_1\neq p_2 \qquad \text{ test bilateral}
\end{matrix}\right. $$

Nous allons pouvoir réutiliser le théorème centrale limite. Notons $\hat{p_1}^{(n)}$ la fréquence de réussite des $X_i$ dans les n premiers termes, et $\hat{p_2}^{(n)}$ celle des $Y_i$. Pour un nombre de réalisations $n_i$ grand $n_i>5$ et des proportions théoriques ni trop grandes ni trop faibles ($n_ip_i >5$ et $n_i(1-p_i)>5$), nous pouvons utiliser l'approximation gaussienne, et approcher chaque fréquence par une loi normale de moyenne $p_i$ et d'écart-type $\sqrt{\frac{p_i(1-p_i)}{n_i}}$. 

Alors en utilisant l'indépendance, nous pourrons approcher la différence des deux proportions par une loi normale de moyenne $p_1-p_2$ et d'écart type $\sqrt{\frac{p_1(1-p_1)}{n_1}+\frac{p_2(1-p_2)}{n_2}}$.

Donc sous $H_0$, si l'on note $p$ le paramètre commun, nous pouvons choisir la statistique : 

$$\frac{\hat{p_1}^{(n_1)}-\hat{p_2}^{(n_2)}}{\sqrt{p(1-p)\left(\frac{1}{n_1}+\frac{1}{n_2}\right)}} \overset{Loi}{\underset{n_1 \&n_2 \to +\infty}{\to}}\mathcal{N}(0,1)$$

Comme nous ne connaissons pas sous l'hypothèse $H_0$ la valeur de p (puisqu'il s'agit d'une hypothèse composite), nous allons devoir l'approcher par le meilleur estimateur que l'on puisse trouver :

$$\hat{p}:=\frac{n_1\hat{p_1}^{(n_1)}+n_2\hat{p_2}^{(n_2)}}{n_1+n_2}$$

Nous prendrons donc la statistique de test

$$ \frac{\hat{p_1}^{(n_1)}-\hat{p_2}^{(n_2)}}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n_1}+\frac{1}{n_2}\right)}}\quad \text{où} \quad \hat{p}:=\frac{n_1\hat{p_1}^{(n_1)}+n_2\hat{p_2}^{(n_2)}}{n_1+n_2}.$$

Et comme dans le point précédent, nous construirons alors des zone de rejet asymptotique à l'aide de la loi normale en fonction du type d'hypothèse.

```{exercise}
:label: exer15
 Lors d’une enquête, menée en 2019 sur 490 français, 387 estimaient que le niveau de vie en France était en déclin. À la même question posée en août 2023 à 400 personnes, 242 estimaient déjà que cela était le cas.
 
Peut-on en conclure, à l’aide d’un test d’hypothèse avec un niveau d’erreur de 5\%, que la proportion de Français pessimistes a diminué entre 2019 et 2023 ?

:::{admonition} Solution 
:class: dropdown
Nous allons faire un test d'égalité de proportion. Notons $p_1$ la proportion de pessimiste en 2019 et $p_2$ celle de 2023. Nous allons tester
   
$$\left\{ \begin{matrix}
    H_0 &:& p_1=p_2\\ \text{contre } H_1 &:& p_1>p_2\\
    \end{matrix}\right. $$
    
Les effectifs $n_1=490$ et $n_2=400$ sont bien supérieurs à 30, et les hypothèses sur les proportions sont également vérifiées. Nous pouvons donc utiliser l'approximation gaussienne.

Nous avons $\hat{p_1}=\frac{387}{490}\approx 0.7898$ et
     $\hat{p_2}=\frac{242}{400}\approx 0.608$. L'estimateur de la proportion est 

$$\hat{p}=\frac{387+242}{490+400}\approx 0.7067.$$

et la statistique d'intérêt est alors :
     
$$\frac{\hat{p_1}-\hat{p_2}}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n_1}+\frac{1}{n_2}\right)}} \approx 5.824$$

Au vu de l'hypothèse, la zone de rejet est de la forme $[q(0.05);+\infty[$. En regardant dans les tables de la loi normale centrée réduite (voir {ref}`fig:normale-centre-reduite-table`), nous trouvons qu'il faut prendre $q(0.05)=1.65$. Comme la statistique est supérieure à cette valeur, nous rejetons l'hypothèse $H_0$, et pouvons en conclure qu'avec un niveau d'erreur de 5\%, la proportion de pessimiste a diminué.
:::
```

La question des tests est loin d'être épuisé. Pour aller plus loin, l'on pourra voir :

 Dans le chapitre {ref}`Gaussien` deux autres tests, propres au modèle Gaussiens.


Dans le chapitre {ref}`test-non-parametrique` un ensemble de tests non paramétriques, qui proposent d'étudier des questions plus générales lorsqu'on ne s'intéresse pas forcément à une loi en particulier.





    