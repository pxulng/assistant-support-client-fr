# Évaluation

Résultats et analyses de toutes les versions de l'assistant. **Toutes les demandes sont synthétiques.** Chaque résultat vient d'une seule exécution. Pour la synthèse, commencer par les deux premiers fichiers.

| Fichier | Contenu |
|---|---|
| `comparaison_versions.md` | Tableau comparatif baseline, v1, v2, v2.1 (Haiku 5.5) et Sonnet 5.5, avec le coût par demande |
| `journal_erreurs.md` | 13 erreurs relevées : ce qui s'est passé, cause probable, correction, décision |
| `resultats_baseline.csv`, `resultats_baseline_cas_limites.csv` | Référence par mots-clés, sans IA |
| `resultats_v1_haiku55.csv`, `resultats_v1_cas_limites.csv` | Prompt v1 (jeu de test, cas limites) |
| `resultats_v2_haiku55.csv`, `resultats_v2_cas_limites.csv` | Prompt v2 |
| `resultats_v2_1_haiku55.csv`, `resultats_v2_1_sonnet55.csv` | Prompt v2.1 sur le jeu de test, avec Haiku 5.5 et Sonnet 5.5 |
| `resultats_v2_1_validation.csv` | Prompt v2.1 sur les 16 demandes de validation (jamais utilisées pour écrire le prompt) |
| `resultats_realistes_v2_1_haiku55.csv`, `resultats_realistes_v2_1_sonnet55.csv` | Prompt v2.1 sur les 15 demandes « style réel » |
| `notation_brouillons_v1.xlsx` | Notation de 40 brouillons de la v1 sur 4 critères, **réalisée par un modèle d'IA** (5 lignes corrigées) |
| Fichier de contrôle humain | 10 lignes de la notation recontrôlées à la main (échantillon petit et facile) |

Colonnes principales des fichiers de résultats : `decision_attendue` (étiquette), la décision du modèle, `decision_ok` (1 si conforme), la raison donnée et le brouillon. Les étiquettes ne sont pas modifiées après avoir vu les résultats ; les corrections sont datées dans le journal.
