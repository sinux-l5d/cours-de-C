# I Complexité des algos

Interessant pour nous, le pire cas

## 1. Mesure du temps d'execution d'un programme

influence du temps d'éxécution d'un programme de tri de données :

    - algo utilisé

    - la puissance de la machine
    - la vitesse de la memoire (ca va un peu avec la puissance de calcul)

    - le style du codeur
    - le langage utilisé
    - compilateur

    - la taille des données n
    - les valeurs des données

busy beaver pire algo du monde

<u>Influence :</u> change d'un facteur mutltiplicateur le temps d'éxecution.

<u>Influence :</u> pareil
- c, c++, Fortran, Ada $\rightarrow$ temps de calcul
- Java $\rightarrow 3 \times$
- Python, Ruby $\rightarrow 30-50 \times$

<u>Complexité :</u> qualité intrinsèque de l'algo en fonction des données, intépendament de la puissance de calcul ou du langage utilisé.

"L'algo X séxécute en un temps proportionel à un facteur n donnée"

## 2 Notations $\Omicron, \Omega, \Theta$

Ces notations vont nous premettre d'évaluer la qualité d'un algo en éliminant les fonctions multiplicatifs.

On s'interesse au cas ou n $\rightarrow \infty$, et on mesure des temps d'execution, donc nos fonctions seront positives.
- $f(n) = \Omicron(g(n)), f\ est\ un\ grand\ \Omicron\ de\ g$
ssi $\exists c > 0, \forall \ge n_0, f(n)\le cg(n)$

f ne croit pas plus vite que g.

- $f(n) = \Omega(g(n))$
ssi $\exists n_0 > 0, \forall n \ge n_0, f(n) \ge cg(n)$

f ne croit pas moins vite que g

- $f(n) = \Theta(g(n))$ ssi $\exists n_0,C_1 > 0, C_2 > 0, \forall n \ge n_0 \\$
$c_1g(n) $

<u>Règles d'Utilisation</u>
- $\alpha f(n) = \Theta (f(n)) si \alpha > 0$

Ex : $4n^2 = \Theta(n^2)$

En effet, $\forall n \ge 0 \\$
$c_1n^2 < 4 n^2 \le c_2 n^2$

- si f(n) tend vers l'infinit, $\forall \alpha, \alpha + f(n) = \Theta(f(n))$

- $f(n) = \Omicron(1) ou \Theta(1)$, on dit f s'exécute en temps constant
- $f(n) = \Omega(1)$ s'exécute au moins en temps constant (ridicule dans une copie)

- monômes : $n^a = \Omicron(n^b)$ si $\Omicron \le a \le b$
Ex : $n^2 = \Omicron(n^3)$, $n^2$ ne croit pas plus vite que $n^3$ 
Pourquoi : $\forall n \ge 1, n^a \ge n^b \Leftrightarrow 1 \le n^{b-a}$ vrai car $b \ge a$

- transitivité des $\Omicron, \Omega, \Theta$
Si $f(n) = \Omicron(g(n))$ et $g(n) = \Omicron(h(n))$ alors $f(n) = \Omicron(h(n))$
Ca veut dire qu'on peut virer les constantes dans les $\Omicron, \Omega, \Theta$

- Règle des sommes
$f(n) + g(n) = \Omicron(max(f(n),g(n)))\\$
$f(n) + g(n) = \Omega(min(f(n),g(n)))$

Ex : $4n^2 + 15n \\
= \Omicron(n^2) + \Omicron(n)\\
= \Omicron(max(n^2, n))\\
= \Omicron(n^2)$

- polynômes : on ne garde que le mônome de + grand degré

- règle des produits :
$\Omicron(f(n))\Omicron(g(n)) = \Omicron(f(n)g(n))$

- la base du logarithme peut etre ignorée. On écrit pas ln mais juste log.

- $log(n) = \Omega(1)$ (log tens vers l'infinit)
- $log(n) = \Omicron(n^a)$ pour $a > 0$

Rq : pour les algos de tri basés sur les comparaisons, $\Omega(n\log n)$

## 4 Calcul de complexité algo

Modèle RAM : suppose que certains calculs sont temps constant.
- accès mémoire avec entier/réel...
- opérations arithmetiques, comparaisons
- appel de fct, passage d'une taille borné de parametres,

- Si $B_1$ $T_1(n)$     
  alors $B_2$ $T_2(n)$  
  Sinon $B_3$ $T_3(n)$  

Total : $\Omicron(max(T_1(n), T_2(n), T_3(n)))$
        $\Omega(min(max(T_1(n), T_2(n)),max(T_1(n)),T_3(n)))$

- For/While

$f(n) \times |B| T(n)$ | $\Omicron(f(n))\Omicron(T(n))$

- Appel d'une fct :
 - empilement des params
 - exécution de la fct
 - valeur de retour

/!\ temps d'execution des fcts récusrsives

Ex difficile :

```pseudo code
Procedure Syracuse(E n:entier)
    Si n = 1 alors retourne 1
    sinon si n est pair
        alors retourne 1 + Syracuse(n/2)
    sinon retourne 1 + Syracuse(3n + 1)
```
On ne sait pas borner le temps d'éxecution de Syracuse

Un calcul de min est linéaire sur la taille des données

## 5 Complexité usuelles des algos

- Temps constant $\Omicron(1)$ : instruction élémentaires
- Temps logarithme $\Omicron(\log n)$ : recherche dichotomique
- Temps linéaire $\Omicron(n)$ : min/max, somme...
- Temps quasilinéaire $\Omicron(n\log n)$ : tri par tas, tri fusion...
- Temps quadratique $\Omicron(n^2)$ : tri bulle...
- Temps cubique $\Omicron(n^3)$ : LU, PLU, sol $Ax = b$, algo naif de produit matrice.
- Temps polynomial $\Omicron(n^k)$ avec k borné
- Algo vérifier en temps polynomial, mais pas d'algo polynomial pour le calculer. On pense que $P \neq NP$, mais on est pas sur
- Temps exponnentiel $\Omicron(a^n)$ avec $a > 1$

# II Analyse amortie des algorithmes

- borné es pire cas le temps d'éxécution d'une séquence de m opérations.
$\rightarrow$ coût amorti de chaque opération correspond au coût réel de cette opération lorsqu'on s'en sert un nombre importatn de fois.

coût amorti $\neq$ coût moyen d'une opération

Plusieurs méthodes existent pour calculer les coûts amorti.
1. Méthode de l'agrégat.
On trasse une borne $T_{total}(m)$ qui est majorant du temps d'éxecution total des m opérations
Le coût amorti de chaque opération sera $T_{total}(m)$

- Illustration 1 :On se donne des opératons sur une pile P
```
empiler(P,v)
Depiler(P) --> val
MultiDepiler(P,k) --> k 1ère valeur sur la pile
PileVide(P)? booléen
```

2. Méthode comptable
On assigne des coûts amortis ĉ à chaque opération. Parfois le cout amorti ĉ est $\neq$ du cout réel c. de l'opération. La différence ĉ-c quand elle est positive est un crédit que l'on place dans la strucure de données et qui pourra servir à payer des opérations futures. Lorsque ĉ-c est négatif, on dépense un crédit qui était dans la structure de données.
Il faut évidemment que le crédit total reste positif.
La somme des ĉ nous donnera le coût amorti total $T_{total}(m)$

Th : Toute séquence de m opération creer/Union/Trouver dont n creer, prend un temps amorti total de $\Omicron(m \alpha(m))$ ou $\alpha(m)$ est une $fct \rightarrow \infty$, mais en pratique ne dépasse pas 4
Preuve : Utilise la méthode du potentiel.

# V Géométrie algorithmique

- algorithmes qui résolvent des probèmes géométriques.
- robotique, Concept AO, jeux vidéos, calcul scientifique, système d'info géo, etc...

Ici, On va se placer dans le plan
$\mathbb{R}^2$
### 1 Notions élémentaires.

Chaque point du plan à deux coordonnées (x,y)

La distance entre 2 points p et q d(p,q) = $\lvert pq \rvert = \sqrt{pq \times pq} = \sqrt{(q_x - p_x)^2 + (q_y - p_y)^2}$

Le segment $[pq]$ est l'ensemble des points "entre p et q"
$[pq] = \{(1-t)p+tq,t \in [0,1]\}$

droite $(pq)= \{(1-t)p+tq, t \in  \mathbb{R}\}$

les points sur la droite $(pq)$ s'obtiennent par combinaison linéaire de p et q avec une somme de coefficients = 1

### 2 Orientation et produit en croix

On veut déterminer si un point r est à gauche, en face, ou à droite du vecteur $\overrightarrow{pq}$

Sii $\overrightarrow{u}$ et $\overrightarrow{v}$ sont 2 vecteurs, leur produit en croix (ou déterminant) s'écrit.

$\overrightarrow{u} \times \overrightarrow{v}= u_xv_y - u_yv_x$

$\overrightarrow{pq} \times \overrightarrow{pr} > 0 $ si r est à gauche de $\overrightarrow{pq}$
 = 0 si r sur la droite $(pq)$
 < 0 si r est à droite de $\overrightarrow{pq}$

<u>Note :</u> si = 0, $\overrightarrow{pq}$ et $\overrightarrow{pr}$ sont colinéaires

Géométriquement, $\overrightarrow{u} \times \overrightarrow{v}$ (ou $det(\overrightarrow{u},\overrightarrow{v})$) est l'aire signée du parallélogramme de coté $\overrightarrow{u}$ et $\overrightarrow{v}$

### 3 Intersection de 2 segments

```

```