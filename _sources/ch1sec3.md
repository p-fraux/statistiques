(Statistiques_usuelles)=
## Moyenne, variance et fonction de répartition empirique
$\newcommand{\R}{\mathbb{R}}$
$\newcommand{\Q}{\mathbb{Q}}$
$\newcommand{\N}{\mathbb{N}}$

:::::::{tabs}

````{tab} Moyenne empirique
 La statistique que l'on voit le plus souvent est celle de la moyenne empirique :
:::{prf:definition} Moyenne empirique
:label: Moydef
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires. On appelle moyenne empirique la variable aléatoire 

$$\overline{X}=\frac{1}{n}\sum_{i=1}^nX_i.$$

On la note aussi parfois $\overline{X}_n$. On note $\overline{x}$ une réalisation de la moyenne empirique.
:::
On l'utilisera dans le cadre de variables aléatoire indépendantes et identiquement distribuées. Elle est naturelle : il s'agit de remplacer une intégrale par sa version discrète, en espérant approcher suffisamment la quantité finale.
::::{prf:property}
:label: Moyprop
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires indépendantes et identiquement distribuées ayant un moment d'ordre 2. On note $m=\mathbb{E}(X_1)$ leur moyenne et $\sigma^2=V(X_1)$ leur variance commune. Alors : 

$$\mathbb{E}(\overline{X}) = m, \qquad V(\overline{X})=\frac{\sigma^2}{n},$$

$$\overline{X}\overset{L^2}{\to} m, \qquad \sqrt{n}\frac{\overline{X}-m}{\sigma}\overset{Loi}{\to}\mathcal{N}(0,1)$$

:::{prf:proof} 
Les deux premiers points sont des conséquences immédiates des propriétés de l'espérance et de la variance. Les deux derniers points sont les conséquences de la loi des grands nombres et du théorème central limite, dont les hypothèses sont clairement vérifiées.
:::

::::

````

````{tab} Variance empirique


:::{prf:definition} Variance empirique

Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires, on appelle variance empirique des $(X_i)$ la quantité 

$$\frac{1}{n}\sum_{i=1}^n \left(X_i-\overline{X}\right)^2.$$
On appelle écart-type empirique débiaisé la quantité 

$$S_X^2\overset{def}{=}\frac{1}{n-1}\sum_{i=1}^n \left(X_i-\overline{X}\right)^2.$$

:::

La variance empirique étant une variable aléatoire, elle peut avoir une espérance et une variance si les variables aléatoire **n'explosent** pas.

(moy_var_empirique)=
:::{prf:property} Espérance de la variance empirique
:class: dropdown
:label: moy_var_empirique
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires indépendantes et identiquement distribuées ayant un moment d'ordre 2, alors

$$\mathbb{E}\left[\frac{1}{n}\sum_{i=1}^n \left(X_i-\overline{X}\right)^2\right]=\frac{n-1}{n}\sigma^2.$$

::::{prf:proof} 
Commençons par remarquer que pour $m\in \R$,

$$\sum_{i=1}^n(X_i-\overline{X})^2 =\sum_{i=1}^n(X_i-m)^2 - n(\overline{X}-m)^2.$$

En effet, 

$$\sum_{i=1}^n(X_i-\overline{X})^2 =\sum_{i=1}^n\left(X_i-m-(\overline{X}-m)\right)^2,$$
$$=\sum_{i=1}^n(X_i-m)^2+(\overline{X}-m)^2-2(\overline{X}-m)(X_i-m),$$
$$=\sum_{i=1}^n(X_i-m)^2+\sum_{i=1}^n(\overline{X}-m)^2-\sum_{i=1}^n2(\overline{X}-m)(X_i-m),$$
$$= \sum_{i=1}^n(X_i-m)^2+ n (\overline{X}-m)^2 - 2(\overline{X}-m)\sum_{i=1}^n(X_i-m),$$
$$= \sum_{i=1}^n(X_i-m)^2+ n (\overline{X}-m)^2-2n(\overline{X}-m)^2,$$
$$=\sum_{i=1}^n(X_i-m)^2- n (\overline{X}-m)^2.$$

En prenant alors $m=\mathbb{E}(X_1)$ et en intégrant l'égalité précédente, nous obtenons que

$$\mathbb{E}(\sum_{i=1}^n(X_i-\overline{X})^2 )=\mathbb{E}\left(\sum_{i=1}^n(X_i-m)^2- n (\overline{X}-m)^2\right),$$
$$=nV(X_1)-nV(\overline{X}),$$
$$\mathbb{E}(\sum_{i=1}^n(X_i-\overline{X})^2 )=(n-1)V(X_1).$$

Ce qui nous donne bien le résultat annoncé.
::::

:::


:::{prf:property} Variance de la variance empirique
:class: dropdown
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires indépendantes et identiquement distribuées ayant un moment d'ordre 4, alors en notant $\mu$ le moment d'ordre 4 commun et $\sigma^2$ la variance commune, l'on a 

$$V(S_X^2)=\frac{1}{n}\left(\mu-\frac{n-3}{n-1}\sigma^4\right).$$
::::{prf:proof} 
Commençons par remarquer que pour $m\in \R$,

$$\sum_{i=1}^n(X_i-\overline{X})^2 =\sum_{i=1}^n(X_i-m)^2 - n(\overline{X}-m)^2.$$

En effet, 

$$\sum_{i=1}^n(X_i-\overline{X})^2 =\sum_{i=1}^n\left(X_i-m-(\overline{X}-m)\right)^2,$$
$$=\sum_{i=1}^n(X_i-m)^2+(\overline{X}-m)^2-2(\overline{X}-m)(X_i-m),$$
$$=\sum_{i=1}^n(X_i-m)^2+\sum_{i=1}^n(\overline{X}-m)^2-\sum_{i=1}^n2(\overline{X}-m)(X_i-m),$$
$$= \sum_{i=1}^n(X_i-m)^2+ n (\overline{X}-m)^2 - 2(\overline{X}-m)\sum_{i=1}^n(X_i-m),$$
$$= \sum_{i=1}^n(X_i-m)^2+ n (\overline{X}-m)^2-2n(\overline{X}-m)^2,$$
$$=\sum_{i=1}^n(X_i-m)^2- n (\overline{X}-m)^2.$$

En prenant alors $m=\mathbb{E}(X_1)$ et en intégrant l'égalité précédente, nous obtenons que

$$\mathbb{E}(\sum_{i=1}^n(X_i-\overline{X})^2 )=\mathbb{E}\left(\sum_{i=1}^n(X_i-m)^2- n (\overline{X}-m)^2\right),$$
$$=nV(X_1)-nV(\overline{X}),$$
$$\mathbb{E}(\sum_{i=1}^n(X_i-\overline{X})^2 )=(n-1)V(X_1).$$

Ce qui nous donne bien le résultat annoncé.
::::

:::
Un résultat important qui permet de calibrer de nombreux tests, que nous reverrons dans {ref}`Cochran`, est le suivant 

::::{prf:theorem}

Soit $(X_i)$ une suite iid de variables, de loi $\mathcal{N}(m,\sigma^2)$. Alors :

$$\overline{X} \sim \mathcal{N}(m,\frac{\sigma^2}{n}),$$ 
$$\overline{X} \text{ et } S_X^2 \text{ sont indépendants,}$$
$$\frac{(n-1)S_X^2}{\sigma^2} = \frac{\sum_{i=1}^n \left(X_i-\overline{X}\right)^2}{\sigma^2}\sim \chi_{n-1}^2 \quad\text{ loi du chi-2 à (n-1) degré de libertés.}$$
::::

````
````{tab} Fonction de répartition empirique
Si nous voulons conserver toute l'information, quoi de mieux que la fonction de répartition ? En effet, elle contient toute l'information de la loi selon laquelle ont été tirés nos observations. C'est dans cette philosophie d'approche de la fonction de répartition théorique que nous posons la définition suivante :

::::{prf:definition} Fonction de répartition empirique

Soient $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires, et $(x_i)$ une réalisation. On définit la fonction de répartition empirique de ces réalisations comme la fonction :

$$F_n : t\mapsto \frac{Card\{k\in [\![1,n]\!], x_k \leq t\}}{n} = \frac{1}{n} \sum_{k=1}^n 1_{]-\infty,t]}(x_k).$$

::::

::::{prf:remark}
:class: dropdown
La fonction de répartition empirique est un exemple de fonction aléatoire.

La fonction de répartition empirique n'est pas continue. Elle a n points de discontinuités.
```{figure} FdR-exp.png
---
height: 350px
name: FdR-exp
---
Un tirage de fonction de répartition
```

::::

La fonction de répartition empirique porte bien sont nom, vu qu'elle converge vers la fonction de répartition.


:::{prf:property} Convergence simple 
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires indépendantes et identiquement distribuées, $F$ la fonction caractéristique de la loi commune, $F_n$ la fonction caractéristique empirique correspondante et $t\in\R$. Alors :

$$\lim\limits_{n\to+\infty}F_n(t) \overset{p.s.}{=} F(t).$$

::::{prf:proof} 
On a que 

$$n F_n(t)=\sum_{k=1}^n 1_{]-\infty,t]}(X_k)\sim \mathcal{B}in(n, F(t)).$$

la loi forte des grands nombres permet de conclure. En effet, pour $X_n \sim \mathcal{B}in(n,p)$, la convergence $\frac{X_n}{n}\overset{p.s.}{\to} p$ est toujours vraie.
::::

:::

Nous pouvons l'observer via des simulations numériques :

::::{prf:remark} 
:class: dropdown

```{figure} FdR-exp-n=4.png
---
height: 200px
name: FdR-exp-n=4
---
Un tirage de fonction de répartition pour 4 observations
```
```{figure} FdR-exp-n=10.png
---
height: 200px
name: FdR-exp-n=10
---
Un tirage de fonction de répartition pour 10 observations
```
```{figure} FdR-exp-n=100.png
---
height: 200px
name: FdR-exp-n=100
---
Un tirage de fonction de répartition pour 100 observations
```

::::

:::{prf:property} Convergence uniforme  
:class: dropdown
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires indépendantes et identiquement distribuées, $F$ la fonction caractéristique de la loi commune, $F_n$ la fonction caractéristique empirique correspondante. Alors presque surement,

$$F_n \overset{CVU}{\to} F.$$

De plus, la loi de $\sup\limits_{t\in \R} |F_n(t)-F(t)|$ ne dépend que de n, et pas de la loi commune des variables aléatoires.

::::{prf:proof} 
Il s'agit en fait d'une généralisation du deuxième théorème de Dini, auquel nous allons nous ramener.

Pour cela, on définit l'inverse généralisé de F comme la fonction

$$F^{\leftarrow} : s \mapsto \inf \{x,\ F(x)\geq s\}$$

qui vérifie $\{F^{\leftarrow}(u)\leq t\}\iff\{u\leq F(t)\}$

On se donne alors une suite de variable aléatoire indépendante $(U_i)$ de loi uniforme sur $[0,1]$, et alors la fonction de répartition des variables $F^{\leftarrow} \circ U_i$ est la fonction F. En particulier, nous avons les égalités en loi suivante :


$$\sup\limits_{t\in \R}\left|F_n(t)-F(t)\right| = \sup\limits_{t\in \R}\left|\frac{1}{n}\sum_{k=1}^n1_{\{F^{\leftarrow} \circ U_k\leq t\}} -F(t)\right|, $$

$$=  \sup\limits_{t\in \R}\left|\frac{1}{n}\sum_{k=1}^n1_{\{ U_k\leq F(t)\}} -F(t)\right|,$$

c'est à dire en changeant de variable que :

$$\sup\limits_{t\in \R}\left|F_n(t)-F(t)\right|=\sup\limits_{s\in F(\R)}\left|\frac{1}{n}\sum_{k=1}^n1_{\{ U_k\leq s\}} -s\right|,$$

et donc

$$\sup\limits_{t\in \R}\left|F_n(t)-F(t)\right|=\sup\limits_{s\in [0,1]}\left|\frac{1}{n}\sum_{k=1}^n1_{\{ U_k\leq s\}} -s\right|.$$

Remarquons dès à présent que nous venons de montrer le deuxième point : la loi du plus grand écart entre fonction de répartition empirique et théorique est indépendante de la loi commune.



Grâce à la loi forte des grands nombres, pour tout $s \in [0,1]$, nous avons convergence presque sûre de $|\frac{1}{n}\sum_{k=1}^n1_{\{ U\leq s\}} $ vers $s$. Notons $A_s$ l'ensemble des expériences pour lesquelles il y a convergence, et l'on aura $\mathbb{P}(A_s)=1$. Nous aimerions en déduire une convergence presque sûre en tout $s\in [0,1]$, mais cet ensemble est indénombrable. Nous allons donc donner un argument supplémentaire pour dépasser cet obstacle.

Tout d'abord, $[0,1]\cap\mathbb{Q}$ est dénombrable, donc 

$$\mathbb{P}(\bigcap_{s\in [0,1]\cap \Q}\left\{\omega, \omega \in A_s\right\})=1$$

Soit $s\in [0,1]$ et $(v_l)_{l\in \N}$ une suite croissante et $(w_l)_{l\in \N}$ une suite décroissante de limite commune s. Soit alors $l\in \N$, alors pour tout $n\in \N$, par croissance des ensembles correspondants, pour tout $\omega \in A:= \cap_{s\in\Q} A_s$, l'on a l'inégalité numérique suivante : 

$$\frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq v_l\}}\leq \frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq s\}}\leq \frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq w_l\}}.$$

En passant alors à la limite respectivement inférieure et supérieure dans les deux inégalités quand $n$ tend vers l'infini, l'on obtient

$$v_l\leq \liminf\limits_{n\to+\infty}\frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq s\}}\leq\limsup\limits_{n\to+\infty}\frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq s\}}\leq w_l.$$
    
Maintenant, comme les termes centraux sont indépendants de l, nous obtenons par encadrement que 
    
$$\liminf\limits_{n\to+\infty}\frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq s\}}=\limsup\limits_{n\to+\infty}\frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq s\}}=s$$
    
Donc pour tout $\omega \in A$, nous avons bien pour tout $s\in [0,1]$ la convergence simple suivante  $ \lim\limits_{n\to+\infty}\frac{1}{n}\sum_{k=1}^n1_{\{ U_k(\omega)\leq s\}}=s$. 
    
Nous pouvons alors conclure grâce au deuxième théorème de Dini qui énonce que la convergence simple d'une suite $(f_n)$ de fonctions réelles d'une variable réelle définies et croissantes (non nécessairement continues) sur un segment $[a, b]$ de $\R$ vers une fonction continue $f$ sur $[a, b]$ implique la convergence uniforme. Notons d'abord que la fonction f est croissante comme limite simple de fonctions croissante.

Soit $\epsilon>0$, et on fixe $k$ un entier tel que $k\geq \frac{f(a)-f(b)}{\epsilon}$.
D'après le théorème des valeurs intermédiaires appliqué à f, il existe $(a_i)$ une subdivision ($a=a_0<a_1<\cdots<a_{k-1}<a_k=b$ telle que $\forall i \in [\![0,k-1]\!], f(a_i)-f(a_{i+1}) \leq \epsilon$.
        
On se donne à présent un $N$ tel que 

$$\forall n\geq N,\forall i \in [\![0,k]\!], |f_n(a_i)-f(a_i)|\leq \epsilon$$

Soit à présent $n\geq N$ et on se donne un $x\in [a,b[$, et l'on note $i$ l'indice tel que $a_i\leq x<a_{i+1}$.

Maintenant, comme $f_n$ et $f$ sont croissantes, $f_n(a_i)\leq f_n(x)\leq f_n(a_{i+1})$ et $f(a_i)\leq f(x)\leq f(a_{i+1})$.

Finalement,

$$|f_n(x)-f(x)|\leq |f_n(x) - f_n(a_i)| + |f_n(a_i)-f(a_i) |+ |f(a_i)-f(x)|$$
$$\leq  |f_n(a_{i+1}) - f_n(a_i)| + |f_n(a_i)-f(a_i) |+\epsilon ,$$
$$        \leq 3\epsilon + \epsilon +\epsilon.$$

Ce qui nous donne bien la convergence uniforme.
::::

:::

:::{prf:property} Vitesse de la convergence en probabilité : _Dvoretzky, Kiefer, Wolfowitz et Massart_
:class: dropdown
Soit $(X_i)_{i\in [\![1,n]\!]}$ des variables aléatoires indépendantes et identiquement distribuées, $F$ la fonction caractéristique de la loi commune, $F_n$ la fonction caractéristique empirique correspondante et $t\in\R$. Alors :

$$\forall \epsilon>0, \mathbb{P}(\sup\limits_{t\in\R}|F_n(t) -F(t)|>\epsilon)\leq 2 e^{-2n\epsilon^2}$$


::::{prf:remark} 
Si l'on note $D_n$ ce supremum, alors $\mathbb{P}(D_n>0.04)\leq 0.1$ dès que $n\geq 996$. Et dès $n=1992$, cette majoration chute à $1\%$.

::::

:::





````
:::::::


```{exercise}
:label: exer04
On considère une suite $(X_n)$ de variables aléatoires réelles de Loi de Cauchy (c'est-à-dire de densité $x\mapsto \frac{1}{\pi(1+x^2)}$). Calculer la loi de la moyenne empirique de ces variables à l'aide de la fonction caractéristique. Que remarque-t-on ?


:::{admonition} Solution 
:class: dropdown
La fonction caractéristique d'une loi de Cauchy est 

$$t \mapsto e^{-|t|}$$

Alors la fonction caractéristique de la moyenne empirique vérifie pour $t\in \R$:

$$ \varphi_{\frac{1}{n}\sum_{i=1}^n X_i}(t) =\varphi_{\sum_{i=1}^n X_i}(\frac{t}{n}) =  \prod_{i=1}^n \varphi_{X_i}(\frac{t}{n})= \left(e^{-|\frac{t}{n}|}\right)^n =e^{-|t|}.$$

On reconnait alors la fonction caractéristique d'une loi de Cauchy !

On remarque qu'en particulier que la moyenne empirique ne converge pas presque surement vers une constante. Ceci n'est pas trop étonnant, puisque la loi de Cauchy n'a pas d'espérance vers laquelle converger.
:::


```


```{exercise}
:label: exer02
On suppose que $X$ admette un moment d'ordre 4. Montrer les convergences $L^2$ et presque sûre de la variance empirique d'un échantillon de réalisation de variables indépendante de même loi que X, et donner la limite. Que dire de la vitesse de convergence ?

:::{admonition} Solution 
:class: dropdown
Nous notons $m=\mathbb{E}(X)$ et $\sigma^2=V(X)$.

La loi forte des grands nombres appliquée deux fois nous assure que 

$$S_X^2 = \frac{\sum_{i=1}^n(X_i-\overline{X})^2}{n-1} =\frac{n}{n-1}\left(\frac{1}{n}\sum_{i=1}^n(X_i-m)^2\right) + \frac{n}{n-1}(\overline{X}-m)^2 \overset{L^2 ; p.s.}{\to} \sigma^2 + 0.$$

Le théorème central limite  nous assure que la convergence (en loi) sera en $\frac{1}{\sqrt{n}}$.
:::


```

```{exercise}
:label: exer01
Montrer que la fonction de répartition empirique vérifie les propriétés d'une fonction de répartition : limites en $±\infty$, continuité à droite et limite à gauche.


:::{admonition} Solution 
:class: dropdown
Il s'agit en fait de la fonction de répartition d'une variable aléatoire uniforme sur $\{x_1, ...,x_n\}$, et vérifie donc toute propriété d'une fonction de répartition
:::


```





