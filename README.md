# Correlation & Anova 
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Correlation%20%26%20Anova.py

Lorsque l'on effectue une analyse en ux analytics et que l'on souhaite savoir si des variables ont un lien les unes avec les autres, plusieurs tests statistiques peuvent permettre d'analyser cette question. Le test de corrélation est un test statistique qui permet de savoir quel est le degré de relation linéaire entre 2 variables numériques. Il calcule un coefficient de corrélation pouvant aller de -1 à 1, plus ce coefficient est proche de 1 en valeur absolue plus il y a une forte relation de proportionnalité (positif ou négatif) entre ces 2 variables et donc cela signifie que ces variables sont liées entre elles. Plus ce coefficient est proche de 0 et moins ces variables sont liées entre elles.

Également dans le cadre d'un A/B testing on peut être amener à comparer le nombre moyen de conversions sur plusieurs effectifs mais comment savoir si ces effectifs sont significatifs. L'analyse de variance (anova) nous permet justement de savoir si les effectifs sont suffisamment importants pour conclure à une significativité des résultats. En statistique on pose l'hypothèse nulle (H0) estimant d'une égalité entre les groupes. Si cette hypothèse est vraie alors la différence de moyenne est due à un échantillon trop faible puisque chaque effectif provient de la même distribution et en augmentant la taille de l'échantillon les moyennes devraient tendre vers une même valeur. En revanche si l'hypothèse nulle est fausse alors même en augmentant la taille de l'échantillon on ne pourrait pas faire disparaitre les différences entre les moyennes puisque les effectifs viendraient de 2 distributions distinctes. Le test calcule la probabilité (p-valeur) d'observer ces résultats sous H0 et si celle-ci est très petite (souvent inférieure au seuil de 0,05) alors on rejette H0. On se tourne alors vers l'hypothèse alternative (H1), que nos effectifs proviennent de 2 distributions significativement différentes et on conclut alors à une différence significative entre les moyennes. En revanche si la p-valeur est supérieure à 5% alors on ne peut pas rejeter H0.
# Chi-2 & Logistic Regression 
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Chi-2%20%26%20Logistic%20Regression.py

En A/B testing, lorsqu'on souhaite maintenant savoir s'il y a un lien entre 2 variables catégorielles, par exemple la mise à jour d'une page et le fait d'effectuer une conversion, on peut utiliser le test statistique du chi-2 afin d'analyser la significativité des résultats. Le test du chi-2 est un test statistique qui comme le test de corrélation permet de savoir si des variables sont liées entre elles mais cette fois 2 variables catégorielles. Ici la première variable sera le type de page vue (originale, A ou B) et la seconde, le fait d'effectuer une conversion (oui ou non). Comme tout test statistique, le test du chi-2 pose H0 estimant d'une égalité entre les groupes, c'est à dire ici qu'il y aurait en proportion autant de conversions effectuées parmi les personnes qui ont vu la page originale que parmi celles qui ont vu la page A et celles qui ont vu la page B, et l'hypothèse alternative H1 estimant d'une différence significative entre les groupes. Si la p-valeur calculée par le test sous H0 est inférieure à 5% alors on rejette H0 et on se tourne vers H1 pour en conclure qu'il y a bien un lien significatif entre les variables, le type de page vue et le fait d'effectuer une conversion.

Si à la suite du test du chi-2 on conclut à un lien significatif entre les 2 variables et que la variable dépendante est dichotomique (2 modalités) alors il est pertinent d'effectuer un modèle de régression logistique binomiale afin de mesurer l'impact de la variable explicative sur la variable dépendante. Ici on modélise le fait d'effectuer une conversion (variable dépendante) en fonction du type de page vue (variable explicative). Le modèle de régression logistique calcule la probabilité qu'un individu à de prendre la première modalité de la variable dépendante connaissant ses modalités de variables explicatives par rapport au profil de référence. Généralement on prend comme profil de référence les modalités des variables explicatives qui ont le plus fort effectif mais ici dans le cadre d'un A/B testing le profil de référence sera le fait d'avoir vu la page originale. On pourra ainsi mesurer de combien fait évoluer les chances d'effectuer une transaction le fait d'avoir vu la page A ou B par rapport au fait d'avoir vu la page originale.

Également si on veut aussi modéliser une variable numérique en fonction de variables catégorielles on peut utiliser le modèle linéaire généralisé qui comme la régression logistique calcule l'impact des modalités des variables explicatives sur la variable dépendante par rapport au profil de référence. On peut par exemple pour un site e-commerce analyser le montant des transactions en fonction des versions du site et voir de combien fait évoluer ce montant le fait d'avoir vu la page A ou B par rapport au fait d'avoir vu la page originale.
# Factor Analyzes & Clustering K-Means
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Clustering%20K-Means.py

En marketing digital il est assez important de bien connaître ses consommateurs, la façon dont ils se comportent afin de bien les segmenter et ainsi pouvoir diriger des actions marketing ciblées. Le modèle de machine learning de clustering k-means peut justement aider à effectuer une segmentation optimale car il permet de découper une population de manière à ce que les groupes constitués soient à la fois en intra les plus homogènes possible et en extra les plus différents les un des autres. Dans un contexte e-commerce on peut par exemple segmenter les transactions afin de mieux comprendre le comportement des acheteurs sur le site. On va donc créer un jeu de données provenant des données Google Analytics requêtées dans BigQuery indiquant pour chaque achat le device et son os, la source de traffic et de campagne de l'acheteur, son pays, les produits et catégories produits qu'il a acheté, le nombre de visites que l'acheteur a effectué sur les produits et catégories produits achetés, et enfin le CA.

L'inconvénient du modelé K-Means est qu'on ne sait pas a priori quel est le nombre optimal de groupes (clusters) il faut choisir pour que le population soit séparée de manière à ce que les clusters constitués soient à la fois le plus homogènes possible et différents les uns des autres. On utilise pour cela la courbe d'elbow en testant une décomposition de 1 à 10 groupes.

![Figure 2021-08-20 201348](https://user-images.githubusercontent.com/83826055/130276345-b0c1d754-406f-4642-ab88-181224ad96c3.png)

Le nombre optimal de clusters qu'il faut choisir afin que la population soit découpée de la meilleure des manières est celui du point des abscisses où la courbe marque une cassure et devient linéaire. On voit ici que la meilleure des manières de segmenter nos acheteurs est de les séparer en 3 ou 4 groupes. On vera que ce qui caractérise le plus les clusters constitués sont le niveau de CA par transaction. On renvoie ainsi ces résultats vers Google Cloud pour une analyse plus en détail de ce qui différencie ces différents clusters sur un outils BI : https://datastudio.google.com/s/hRcohz4T4DI.
# Kaplan Meier Survival
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Kaplan%20Meier%20Survival.py

Lorsqu'on effectue un A/B testing on peut également être amener à analyser la performance du site en termes de durée. Quelle version permet de gêner une conversion le plus rapidement ? Pour cela il peut être pertinent d'effectuer une analyse de survie de Kaplan Meier. Souvent utilisée en médecine et en finance cette analyse permet de calculer la probabilité qu'un évènement à de ne pas se produire (le décès) à un instant t. C'est la raison pour laquelle elle se nomme analyse de "survie", la fonction S(t) donne la probabilité d'être en vie à l'instant t. Pendant la durée complète de l'analyse on observe des individus pour qui après une certaine durée, soit l'évènement est intervenu (ils sont décédés) soit on a arrêté de les observer (ils sont censurés).

Dans un contexte ux on peut symboliser le décès par le fait d'effectuer une conversion. Sur un site e-commerce on va par exemple générer un jeu de données provenant des données Google Analytics requêtées dans BigQuery indiquant pour chaque visiteur la durée entre sa première visite et son premier achat (le décès) s'il en a effectué, et la durée entre sa première et sa dernière visite s'il n'en a pas effectué (la censure). On indique également le device sur lequel il a effectué la transaction ou sa dernière visite s'il n'en a pas effectué afin de voir quelle version du site est la plus performante.

![KMF](https://user-images.githubusercontent.com/83826055/129444429-fcef0f33-b30f-4c5c-9b22-af75347ed59e.png)

On voit ici la survie globale, indépendamment des versions du site, qui signifie ici la probabilité de n'avoir effectué aucun achat x jours après sa première visite (99% le premier jour, 60% après 1 an (le site n'est pas très efficace)). Mais l'intérêt de l'analyse est bien de segmenter les individus afin de voir dans quelle situation la survie est la meilleure ou la moins bonne suivant le contexte de l'analyse.

![KMF_Device](https://user-images.githubusercontent.com/83826055/129444431-0271e2aa-c5cc-4988-9497-2b6b61337bb1.png)

On regarde maintenant la survie en fonction du device et on constate que la survie la moins bonne est celle de la version du site sur desktop, ce qui signifie que l'on y décède plus rapidement. Dans un contexte de santé cela serait négatif mais ici dans notre contexte e-commerce cela signifie en fait que la version du site sur desktop est la plus performante en termes de durée pour gêner une conversion. La probabilité de n'avoir effectuer aucun achat 200 jours après sa première visite est de 95% sur mobile et tablet et de 75% sur desktop (plus faible mais tout de même élevé). Afin de savoir si ces résultats sont significatifs on effectue le test statistique du log rank qui pose H0 et H1, et conclue à une significativité des résultats si la p-valeur calculée sous H0 est inférieure à 5%. On peut également à l'aide du modèle de cox calculer l'impact des différents segments sur le risque ablsolu de décès.

![KMF_2](https://user-images.githubusercontent.com/83826055/129450587-cf45114a-ea53-49d4-b7ee-a1bb04a8b7f3.png)
Également si l'on souhaite maintenant non plus analyser la rapidité d'une conversion mais la durée de rétention, on ne calcule plus la durée entre la première visite et le premier achat mais avec le dernier. On voit que l'analyse survie en termes de rétention vient corroborer la constatation de l'inefficacité du site. La probabilité qu'un individu continue d'acheter sur le site un an après sa première visite est de 48%.

![KMF_Device_2](https://user-images.githubusercontent.com/83826055/129450589-e52c90a2-8391-4d86-9827-43318689c2ae.png)

Si on analyse maintenant la survie en fonction du device, on voit que c'est la version sur tablet qui a la meilleure rétention. La probabilité qu'un individu continue d'acheter un ans après sa première visite est de 95% sur tablet et de 40% sur desktop. Ce résultat peut néanmoins comporter un biais car on voit que nos fonctions de conversion de retention sont assez similaires, cela peut en fait signifier que la plupart des individus n'ont en fait réalisé qu'une seule transaction et que ceux qui l'ont fait sur tablet l'ont fait tardivement. Pour mieux analyser la rétention il faudrait ajouter aux individus censurés ceux qui n'ont effectué qu'un seul achat.
