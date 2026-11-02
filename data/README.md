# Données

**Toutes les données sont synthétiques** : aucune demande, aucun nom ni numéro ne vient d'un vrai client.

| Fichier ou dossier | Contenu |
|---|---|
| `procedures/` | Les 8 procédures fictives de l'assistant |
| `demandes_synthetiques.csv` | 80 demandes étiquetées : 64 pour le test, 16 pour la validation (colonne `jeu`) |
| `cas_limites_escalade.csv` | 21 cas difficiles, tous à escalader (menaces, sécurité, fraude, hors périmètre) |
| `demandes_realistes.csv` | 15 demandes au style de vrais messages (courtes, fautes, plusieurs sujets), écrites par Claude, étiquettes revues par l'auteur le 31/10/2026 |

Colonnes : `id`, `jeu`, `origine` (toujours `SYNTHETIQUE`), `procedure_attendue`, `decision_attendue` (`repondre` ou `escalader`), et selon le fichier `difficulte` et `points_cles_reponse`.

Règle : le jeu de validation n'a servi qu'à mesurer, jamais à écrire ou ajuster un prompt.
