# Prompts

| Fichier | Version | Changement |
|---|---|---|
| `prompt_v1.txt` | v1 | Règles, format de sortie JSON et 8 procédures |
| `prompt_v2.txt` | v2 | Ajoute : salutation « Bonjour », pas de conclusion de retard sans preuve, demande du numéro de commande, pas de reprise des consignes internes, escalade des produits d'état douteux |
| `prompt_v2_1.txt` | v2.1 | Corrige un effet de bord de la v2 : la règle sur l'état du produit ne s'applique pas aux exclusions déjà écrites (hygiène, personnalisé, soldés) |

Tous les prompts finissent par `{{ $json.demande }}`, où n8n insère la demande du client. Résultats de chaque version dans `evaluation/comparaison_versions.md`.
