# Workflow

`support_tri_brouillon_v1.json` est l'export du workflow n8n : un nœud Code « Demandes » qui fournit les demandes, un nœud Anthropic « Message a model » avec le prompt, et un nœud Code « Lecture » qui lit la réponse JSON et escalade par sécurité si elle est illisible. Pour l'utiliser : l'importer dans n8n, coller le prompt voulu (dossier `prompts/`) et régler « Maximum Number of Tokens » à 4000.
