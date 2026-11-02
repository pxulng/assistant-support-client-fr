# Journal d'erreurs : assistant de support client (v1)

> Toutes les demandes sont **synthétiques** (fictives). Version évaluée : workflow n8n v1, modèle Claude Haiku 5.5, une seule exécution complète par jeu.
> Statuts des chiffres : **mesuré** = observé sur le jeu de test ; **hypothèse** = supposé ; **projeté** = calculé à partir des deux premiers.

## 1. Contexte de la mesure

| Jeu | Taille | Résultat mesuré |
|---|---|---|
| Jeu principal (test) | 64 demandes, dont 8 à escalader | 58/64 bonnes décisions (91 %) ; 8/8 escalades repérées ; 6 escalades inutiles sur 56 |
| Cas limites | 21 demandes, toutes à escalader | 20/21 escalades repérées ; 1 réponse automatique à tort (S003) |
| Notation des brouillons | 40 brouillons, notés par un modèle d'IA (grille 4 critères) | 24/40 jugés prêts à envoyer tels quels (22/40 avant correction de 5 lignes, voir erreurs 4 et 5) |
| Demandes « style réel » (15, écrites par Claude, étiquettes revues par Paul) | 15 demandes, dont 9 à escalader | Haiku et Sonnet : 13/15 décisions conformes, 7/9 escalades repérées, mêmes décisions (voir erreur 13) |
| Contrôle humain | 10 lignes, à l'aveugle | 40 notes sur 40 identiques à celles du modèle (échantillon petit et facile) |

Réserves : le prompt, les procédures et les demandes ont été écrits dans la même démarche, ce qui rend les résultats probablement optimistes. Les notes des lignes D010, D037, D038, D071 et D072 ont été corrigées (fichier `notation_brouillons_v1.xlsx`) ; le contrôle humain portait sur 10 autres lignes, notées avant cette correction.

## 2. Les erreurs relevées

Gravité : **Haute** = viole le critère « aucun cas à escalader ne reçoit de réponse automatique » ; **Moyenne** = information fausse ou décision inutile ; **Faible** = finition.

| N° | ID concernés | Gravité | Ce qui s'est passé | Cause probable | Correction prévue en v2 | Statut |
|---|---|---|---|---|---|---|
| 1 | S003 | Haute | Un client qui a porté des baskets 10 minutes dehors reçoit un refus poli, au lieu d'être escaladé. Réponse automatique sur un cas à escalader (1 sur 29). | La règle « non porté » n'est pas définie : où commence « porté » ? Le modèle tranche seul. | Préciser la règle dans la procédure 02 **Décision de Paul (31/10/2026) : tout cas ambigu est escaladé** (aucun refus automatique si l'état du produit est douteux). | Décidé, à implémenter en v2 |
| 2 | D002 | Moyenne | Pour une commande du samedi, le brouillon s'excuse d'un retard le mardi, alors que 48 h ouvrées ne sont pas encore dépassées. | Le prompt ne dit pas comment compter les jours ouvrés, et le modèle conclut à un retard sans pouvoir le vérifier. | Ajouter : « ne conclus jamais à un retard si les dates ne le montrent pas ; reste au conditionnel ». | À corriger en v2 |
| 3 | D008, D009, D043, D055, D071, D072 | Moyenne | 6 escalades inutiles sur 56 demandes à traiter (11 %) : le modèle passe la main alors que la procédure permettait de répondre ou que l'étiquette est discutable. | Consigne « en cas de doute, escalader » : prudente par construction. | À arbitrer : réduire les doutes en précisant les procédures, sans toucher à la règle de sécurité. Mesurer que les réponses automatiques à tort ne remontent pas. **Décision de Paul (31/10/2026) : on garde la prudence actuelle** ; seules les procédures ambiguës sont précisées. | Décidé |
| 4 | D010, D037, D038 | Faible | Le brouillon ne demande pas le numéro de commande, ce qu'un conseiller ferait en pratique. | Cette règle n'existe pas dans les procédures v1 : le reproche vient de la notation, pas du modèle. | Ajouter la règle aux procédures v2, puis noter la v2 avec cette règle. Retirer la pénalité dans la notation v1. | Notation v1 corrigée ; règle à ajouter en v2 |
| 5 | D071, D072 | Faible | Complétude notée 2 parce que le modèle a escaladé : la note mélangeait la décision et le texte du message. | Défaut de notation, pas de modèle. | Noter le message d'attente pour ce qu'il est ; la décision est comptée dans l'erreur 3. | Notation v1 corrigée |
| 6 | 15 brouillons sur 85 | Faible | Le brouillon commence sans « Bonjour » (mesuré par comptage automatique sur les 85 brouillons des deux jeux). | Le prompt n'impose pas de salutation. | Ajouter : « commence toujours par Bonjour ». | À corriger en v2 |
| 7 | D009, S001, S009, D061 | Faible | Fautes de langue relevées : « ssincèrement » (2 fois), « que un conseiller », « Restez à votre disposition » au lieu de « Nous restons ». | Variation du modèle économique ; aucune relecture automatique. | Comparer avec Claude Sonnet 5.5 ; ajouter une consigne de relecture. Relevé partiel : les 85 brouillons n'ont pas tous été relus. | À corriger en v2 |
| 8 | D004 | Faible | Le brouillon écrit « nous ne pouvons pas deviner la taille qui vous conviendra », ton sec. | Le modèle reprend le mot de la consigne interne (« sans deviner ») dans le message client. | Reformuler la consigne en langage client (« conseillez de comparer avec un vêtement bien ajusté »). | À corriger en v2 |
| 9 | D001 à D005 (essais) | Moyenne | Les brouillons changent d'une exécution à l'autre pour la même demande. Un message d'attente de D003 a laissé entendre un refus lors d'un essai, pas lors de l'exécution finale. | Le modèle ne répond pas deux fois exactement pareil. | Garder une seule exécution complète comme référence. Tester un réglage de température si le nœud n8n le permet (non vérifié). | À documenter |
| 10 | D002 (essai) | Moyenne | Une réponse a été coupée en plein milieu et n'a pas pu être lue (« ERREUR_JSON »). | Limite du nombre de tokens trop basse : la réflexion interne du modèle consommait la place de la réponse. | Limite relevée à 4000 tokens, problème résolu. Le code de lecture escalade par sécurité quand une réponse est illisible, ce qui a évité une réponse défectueuse. | Résolu |
| 11 | D025, D005, D018, D063 | Moyenne | En v2, le maillot de bain ouvert (D025) est escaladé alors que la procédure prévoit un refus pour hygiène ; D005, D018 et D063 aussi passent à « escalader ». Escalades inutiles : 7 sur 56 en v2 (6 en v1). | La règle ajoutée en v2 (état du produit douteux → escalader) est trop large pour D025 ; pour les 3 autres, le modèle change de décision sans règle précise (variation d'une exécution à l'autre possible). | v2.1 : la règle ne s'applique pas aux exclusions déjà écrites (hygiène, personnalisé, soldés). Effet à mesurer sur les 64 demandes. | Corrigé : D025 redevient « répondre » en v2.1 (jeu de 64 : 58/64 bonnes décisions, 6 escalades inutiles). D005 aussi, mais D072 passe à « escalader » sans lien avec la règle (variation d'une exécution à l'autre) |
| 12 | D077, D022 | Moyenne | Le brouillon de D077 conseille de ne pas réutiliser le casque « par précaution » ; celui de D022 (v2.1) demande de ne pas communiquer de mot de passe par email. Aucune procédure ne dit ces deux choses. | Le modèle ajoute un conseil de sécurité de bon sens, hors procédures (règle 1 : ne rien inventer). | Un conseiller relit toujours ce brouillon (cas escaladé). À décider : interdire tout conseil non écrit, ou l'accepter sur les cas de sécurité. | À arbitrer |
| 13 | R013, R014 (demandes « style réel ») | Moyenne | Haiku et Sonnet répondent à un suivi bloqué depuis 6 jours (R013) et à un retour de casque de vélo (R014), alors que Paul les a étiquetés « escalader » (règle : toute hésitation est escaladée). 13/15 décisions conformes, 7/9 escalades repérées. | Les procédures écrites couvrent ces deux cas : la règle de Paul est plus stricte que les procédures, ce n'est pas un défaut de modèle. | **Décision de Paul (31/10/2026) : on garde les procédures telles quelles** ; l'écart est documenté, aucune règle ajoutée. | Décidé (option A) |

## 3. Défauts du jeu de test (pas du modèle)

Ces écarts viennent de mes étiquettes de départ, pas du comportement de l'assistant. Ils ne seront corrigés que dans une version 2 du jeu, datée, pour ne pas modifier les attentes après avoir vu les résultats.

| ID | Pourquoi l'étiquette est discutable |
|---|---|
| D008 | « Cette tente convient pour 3 adultes ? » : l'assistant n'a aucune fiche produit, donc ne peut pas répondre. Attendu à revoir (escalade). |
| D018, D039, S002 | Deux procédures s'appliquent à la demande (08 et 02 ; 02 et 05 ; 01 et 08) : la procédure « attendue » était arbitraire. |
| D043, D055 | La procédure ne tranche pas clairement (doute sur l'origine du défaut ; changement de couleur non prévu). |
| D009, D039, D070 | Deux procédures s'appliquent (08 et 01 ; 02 et 05 ; 01 et 05) : l'écart de procédure en v2 n'est pas une erreur du modèle. |
| D059, D074 (validation) | « Cette veste est-elle imperméable ? » (information absente de la fiche) et « changer l'adresse d'un colis déjà expédié » (non prévu) : escalader se défend, l'étiquette « répondre » est discutable. Non modifiées après coup. |

## 4. Ce que ce journal ne montre pas

- Le comportement avec de vraies demandes, qui seront plus variées et plus désordonnées.
- Le comportement du modèle sur de nombreuses exécutions : une seule exécution par jeu.
- La fiabilité de la notation par le modèle sur les cas difficiles : le contrôle humain ne portait que sur 10 lignes, surtout simples.
