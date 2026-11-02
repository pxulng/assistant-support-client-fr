# Comparaison des versions (demandes synthétiques)

> Toutes les demandes sont **synthétiques**. Résultats **mesurés**, une seule exécution par version. Modèle de toutes les versions Claude : Haiku 5.5.

## Jeu de test (64 demandes, dont 8 à escalader)

| Version | Bonnes décisions | Bonne procédure | Escalades repérées | Escalades inutiles (sur 56) |
|---|---|---|---|---|
| Baseline (mots-clés, sans IA) | 51/64 (80 %) | 47/64 (73 %) | 3/8 | 8 |
| Prompt v1 | 58/64 (91 %) | 61/64 (95 %) | 8/8 | 6 |
| Prompt v2 | 57/64 (89 %) | 61/64 (95 %) | 8/8 | 7 |
| Prompt v2.1 | 58/64 (91 %) | 60/64 (94 %) | 8/8 | 6 |
| Prompt v2.1 avec Claude Sonnet 5.5 | 64/64 (100 %) | 64/64 | 8/8 | 0 |

Lecture : la v1 améliore nettement la baseline, surtout sur les escalades (8/8 contre 3/8). La v2 améliore la forme des brouillons (« Bonjour » dans 64/64, numéro de commande demandé quand il le faut) sans améliorer les décisions. Les règles de la v2 et de la v2.1 ont été écrites en connaissant les erreurs de ce jeu : elles sont donc avantagées ici. La v2.1 corrige D025 (maillot de bain ouvert) mais, d'une exécution à l'autre, D005 et D072 ont changé de décision sans que le prompt ne les concerne : une même version ne donne pas toujours le même résultat. Avec Sonnet 5.5, le score est parfait par rapport à mes étiquettes, mais deux de ses réponses restent discutables malgré ce score : pour D055 (changer la couleur d'une commande en préparation), il affirme que la commande « peut encore être modifiée », ce que la procédure 05 ne prévoit pas ; pour D043 (baskets qui se décollent), il répond au lieu d'escalader le doute sur l'origine du défaut. Ces deux étiquettes figuraient déjà parmi celles que je jugeais discutables : le 64/64 est donc à lire avec prudence. Les 4 écarts de procédure de la v2.1 (D009, D018, D039, D070) concernent des demandes où deux procédures s'appliquent.

## Cas limites (21 demandes, toutes à escalader)

| Version | Escalades repérées |
|---|---|
| Baseline | non mesuré dans ce tableau |
| Prompt v1 | 20/21 (S003 répondu à tort) |
| Prompt v2 | 21/21 (la règle ajoutée visait S003 : non indépendant) |

## Jeu de validation (16 demandes, jamais utilisé pour écrire le prompt, dont 2 à escalader)

| Version | Bonnes décisions | Bonne procédure | Escalades repérées |
|---|---|---|---|
| Prompt v2.1 | 14/16 (88 %) | 16/16 | 2/2 |

Échantillon petit : « 2 sur 2 » escalades ne prouve rien de solide.

## Demandes « style réel » (15 demandes écrites par Claude à la demande de Paul, étiquettes revues par Paul le 31/10/2026 : toutes les hésitations passées en « escalader »)

| Version | Bonnes décisions | Escalades repérées (sur 9) | Réponses automatiques à tort |
|---|---|---|---|
| Prompt v2.1, Haiku 5.5 | 13/15 | 7/9 | 2 (R013, R014) |
| Prompt v2.1, Sonnet 5.5 | 13/15 | 7/9 | 2 (R013, R014) |

Les deux modèles prennent les mêmes décisions sur ces 15 demandes. Les deux erreurs viennent de demandes que Paul a classées « escalader » par prudence alors que les procédures écrites permettent de répondre : l'écart vient donc de la règle, pas du modèle. Coût mesuré : environ 0,0007 $ par demande avec Haiku (précision faible, 15 demandes) et environ 0,013 $ avec Sonnet (solde 3,97 → 3,77).

## Coût (mesuré à partir du solde du compte, précision 1 centime)

| Série | Demandes | Solde avant → après | Coût par demande |
|---|---|---|---|
| Cas limites, v2 | 21 | 4,94 → 4,91 | ≈ 0,0014 |
| Jeu de test, v2 | 64 | 4,91 → 4,84 | ≈ 0,001 (entre 0,0009 et 0,0013) |

| Jeu de test, v2.1 | 64 | 4,83 → 4,77 | ≈ 0,0009 (entre 0,0008 et 0,0011) |
| Jeu de test, v2.1, Sonnet 5.5 | 64 | 4,77 → 3,98 (hypothèse : aucun autre appel entre les deux relevés) | ≈ 0,012 (environ 13 fois Haiku) |

Le coût inclut la réflexion interne du modèle, facturée comme du texte de sortie. Monnaie supposée : dollars.
