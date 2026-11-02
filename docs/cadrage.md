
# Cadrage du cas client (client fictif)

> Document de cadrage. Toutes les données sont synthétiques.
> Les chiffres marqués (H) sont des hypothèses, pas des mesures.

## 1. Le client
- **Nom :** Vélora Sport, distributeur de sport en ligne et en magasin (fictif)
- **Volume de demandes :** 3 000 par mois (H)
- **Canaux :** email et formulaire web
- **Équipe support :** 6 conseillers (H)
- **Problème :** les conseillers passent leur temps sur des demandes répétitives
  (suivi de commande, retours), ce qui retarde les cas complexes.

## 2. Types de demandes
| Type | Exemple | Part estimée (H) |
|---|---|---|
| Suivi de commande | « Où est mon colis ? » | 35 % |
| Retour et remboursement | « Je veux renvoyer mes chaussures » | 25 % |
| Produit défectueux / garantie | « Les chaussures sont abimées après deux semaines » | 15 % |
| Réclamation / litige | « Je n'ai jamais reçu mon remboursement » | 25 % |

## 3. Toujours escaladé vers un humain
- Litige, menace juridique ou client très en colère
- Remboursement hors des conditions écrites
- Information absente des procédures
- Données personnelles sensibles
- Toute demande où l'assistant a un doute

## 4. Process actuel
1. **Réception** : la demande arrive par email ou formulaire.
2. **Tri** : un conseiller lit et classe la demande.
3. **Réponse** : le conseiller cherche la procédure et rédige.
4. **Escalade** : les cas sensibles remontent à un responsable.

## 5. User stories
1. En tant que conseiller, je veux que chaque demande soit classée automatiquement pour ne pas la trier à la main.
2. En tant que conseiller, je veux un brouillon de réponse qui cite la procédure utilisée, pour vérifier vite.
3. En tant que conseiller, je veux être alerté quand l'assistant doute, pour traiter ces cas moi-même.
4. En tant que responsable, je veux que les cas sensibles ne reçoivent jamais de réponse automatique.
5. En tant que responsable, je veux connaître le coût par demande pour juger si l'outil est rentable.
6. En tant que client, je veux une réponse correcte et polie, ou un message m'indiquant qu'un conseiller me répond.

## 6. Critères de réussite (objectifs fixés par moi, à confirmer par la mesure)
- Aucune demande à escalader ne reçoit de réponse automatique.
- Taux de bon classement : objectif ≥ 85 % (H)
- Qualité des brouillons : objectif ≥ 3 sur 4 en moyenne (grille à définir en semaine 4)
- Coût par demande : à mesurer en semaine 4

## 7. Périmètre
- **Inclus :** classification, brouillon sourcé, règle d'escalade, mesure de qualité et de coût.
- **Exclus :** envoi automatique des réponses, intégration à un vrai outil de ticketing, données réelles.
