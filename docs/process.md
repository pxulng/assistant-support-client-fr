# Process : avant et après

> Schéma du client fictif. Le « après » est la cible à tester, pas un résultat mesuré.

## Process actuel (manuel)

```mermaid
flowchart LR
    A["Réception de la demande<br/>(email ou formulaire)"] --> B["Tri manuel<br/>par un conseiller"]
    B --> C["Recherche de la procédure"]
    C --> D["Rédaction de la réponse"]
    B --> E["Cas sensible"]
    E --> F["Escalade au responsable"]
    D --> G["Envoi au client"]
    F --> G
```

## Process cible (avec l'assistant)

```mermaid
flowchart LR
    A["Réception de la demande"] --> B["Assistant : classification<br/>(type, urgence, escalade oui/non)"]
    B -->|"Cas standard"| C["Assistant : brouillon<br/>basé sur la procédure citée"]
    B -->|"Cas sensible ou doute"| E["Escalade au responsable<br/>+ message d'attente au client"]
    C --> D["Conseiller : relecture<br/>et validation"]
    D --> G["Envoi au client"]
    E --> G
```

**Principe :** l'assistant ne répond jamais seul. Un humain relit chaque brouillon
et traite tous les cas sensibles.
