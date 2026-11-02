# Étude de cas : trier les demandes d'un support client avec un assistant IA, et mesurer ce qu'il vaut

> Projet de démonstration sur **données entièrement synthétiques** : l'entreprise (un distributeur de sport), ses 8 procédures et toutes les demandes sont inventées. Aucune donnée client réelle. J'ai travaillé sur un vrai support client (mission freelance), mais rien de ce projet n'en vient.

## Le problème

Un support client reçoit des demandes de natures très différentes : certaines se règlent avec une procédure écrite (délai de livraison, retour d'un produit), d'autres ne doivent jamais être traitées automatiquement (menace, sécurité, données personnelles, cas qui sort des procédures). L'erreur coûteuse n'est pas une réponse un peu longue, c'est **répondre seul à une demande qu'un conseiller aurait dû prendre**.

Question posée : un assistant peut-il lire une demande, décider s'il répond ou s'il passe la main, et rédiger un brouillon qu'un conseiller relit, **sans jamais envoyer seul** ?

## Ce que j'ai construit

Un workflow n8n + Claude. Pour chaque demande, l'assistant choisit une procédure parmi 8, décide « répondre » ou « escalader », donne sa raison et rédige un brouillon (ou un message d'attente si escalade). La règle de sécurité est simple : **en cas de doute, il escalade**, et si sa réponse est illisible, il escalade aussi.

## Comment je l'ai évalué

- **Une baseline sans IA** : un script de mots-clés, pour savoir ce que vaut l'outil le plus simple.
- **80 demandes synthétiques** (64 de test, 16 de validation jamais utilisées pour écrire le prompt), **21 cas limites** tous à escalader, **15 demandes de style plus « réel »**.
- **La bonne mesure.** Une règle « ne jamais escalader » obtiendrait 87,5 % de bonnes décisions sur le jeu de test (56 demandes sur 64 sont à traiter) tout en ratant 100 % des escalades. J'ai donc suivi surtout les **escalades repérées** et les **escalades inutiles**.
- **Une notation des brouillons** par un modèle d'IA (4 critères), puis un **contrôle humain** de 10 lignes.
- **Un journal des erreurs** (13 entrées) avec cause, correction et décision.

## Ce qui s'est passé

**Le passage du mot-clé au modèle a le plus d'effet.** Sur le jeu de test, la baseline par mots-clés repère 3 escalades sur 8 ; le premier prompt les repère toutes (8/8) et passe de 80 % à 91 % de bonnes décisions.

**Améliorer la forme n'a pas amélioré la décision.** La version 2 ajoute des règles (toujours « Bonjour », demander le numéro de commande) : les brouillons sont meilleurs, les décisions pas (89 % puis 91 %). Une règle ajoutée pour corriger un cas (D025, un maillot de bain ouvert) en a fait changer d'autres, sans lien avec elle. Ce genre de bruit est normal d'une exécution à l'autre ; je l'ai mesuré au lieu de le raconter autrement.

**Sonnet 5.5 fait 64/64, mais il faut lire ce score avec méfiance.** Il n'escalade aucune demande à tort sur le jeu de test (contre 6 pour Haiku), pour un coût 13 fois plus élevé (environ 0,012 $ par demande contre 0,001 $). Mais deux de ses réponses sont contestables malgré le score parfait, sur des étiquettes que je jugeais déjà discutables, et sur les 15 demandes « style réel » il ne fait pas mieux que Haiku (13/15 pour les deux).

**Mes propres étiquettes sont une source d'erreur.** Plusieurs demandes relèvent de deux procédures, et certaines de mes étiquettes sont arbitraires. J'ai décidé de ne jamais les modifier après avoir vu les résultats (sauf correction datée), et de les lister.

**Des décisions de ma part, documentées.** Tout cas ambigu est escaladé (31/10/2026), même si cela crée des escalades inutiles. Sur les demandes « style réel », deux demandes que j'avais classées « escalader » par prudence reçoivent une réponse des deux modèles alors que les procédures écrites le permettent : c'est ma règle qui est plus stricte que les procédures, pas un défaut de modèle. J'ai choisi de ne pas modifier les procédures et de l'écrire.

## Ce que j'en retiens

- **Choisir la mesure avant de regarder les résultats.** Le taux de bonnes décisions seul aurait récompensé un outil qui n'escalade jamais.
- **Séparer le jeu qui sert à corriger de celui qui sert à juger.** Les règles de la v2 ont été écrites en connaissant les erreurs du jeu de test : elles y sont avantagées. Seule la validation (16 demandes, 14 bonnes décisions) ne l'est pas, mais elle est petite (2 escalades seulement).
- **Un modèle plus cher n'est pas toujours utile.** Sonnet 5.5 réduit les escalades inutiles mais ne se distingue pas sur les cas « réels » ; la relecture par un conseiller reste de toute façon obligatoire.
- **Garder une trace des erreurs.** Le journal m'a servi à décider quoi corriger et quoi laisser (par exemple les conseils de bon sens que le brouillon ajoute hors procédures).

## Limites

Données et procédures écrites dans la même démarche que le prompt : résultats probablement trop favorables. Une seule exécution par version. Notation des brouillons faite par un modèle d'IA, contrôlée sur 10 lignes surtout simples (40 notes sur 40 identiques, ce qui ne prouve rien sur les cas difficiles). Coûts calculés à partir du solde du compte, avec un centime de précision. Aucun test sur de vraies demandes.

## Ce que je ferais ensuite

1. Tester sur de vraies demandes, anonymisées, avec l'accord d'un client.
2. Répéter chaque exécution plusieurs fois pour mesurer la variation.
3. Faire noter un échantillon plus grand et plus difficile par un conseiller.
4. Chiffrer le temps de traitement avec et sans assistant, étiqueté « hypothèse » tant qu'il n'est pas mesuré.
