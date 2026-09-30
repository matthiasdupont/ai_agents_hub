# Architecture des agents

## Contrat des composants

### Instructions

`.github/copilot-instructions.md` contient uniquement les règles applicables à
presque toutes les tâches. Les règles ciblées utilisent
`.github/instructions/*.instructions.md` avec un `applyTo` précis.

### Agents

Un agent est propriétaire d'un rôle et d'un type de décision. Son frontmatter
définit sa surface de découverte et ses capacités; son corps définit sa méthode,
ses limites et son format de sortie.

| Agent | Responsabilité | Mutation |
| --- | --- | --- |
| Orchestrator | Décomposer, déléguer et synthétiser | Non |
| Explorer | Trouver les faits et chemins de code pertinents | Non |
| Reviewer | Identifier les défauts et risques d'un changement | Non |
| Agent principal | Implémenter et valider une demande | Oui |

L'agent principal fourni par l'environnement reste responsable des edits. Cela
évite de dupliquer ses capacités dans un agent custom trop généraliste.

### Skills

Un skill encode une procédure indépendante du rôle qui l'exécute. Il peut
contenir :

```text
<skill-name>/
├── SKILL.md
├── scripts/       # Automatisation exécutable, optionnelle
├── references/    # Documentation détaillée, optionnelle
└── assets/        # Modèles et ressources, optionnels
```

Les ressources ne sont ajoutées que lorsqu'elles sont utilisées. Le chargement
progressif garde le contexte initial réduit.

### Prompts

Un prompt expose une action courte dans le menu `/`. Dès qu'une action exige
plusieurs étapes, des ressources ou une gestion d'échec, elle devient un skill.

## Routage d'une demande

1. Appliquer les instructions globales et les éventuelles instructions ciblées.
2. Traiter directement une tâche locale et claire.
3. Utiliser Explorer si le propriétaire du comportement est inconnu.
4. Utiliser Orchestrator si plusieurs rôles ou étapes indépendantes sont requis.
5. Charger un skill quand une procédure connue correspond au besoin.
6. Faire intervenir Reviewer lorsque le risque ou la portée justifie une revue
   indépendante.

## Ajouter un composant

### Nouvel agent

Utiliser `/create-agent`, puis vérifier : responsabilité unique, description
déclenchable, outils minimaux, contraintes explicites et sortie structurée.

### Nouveau skill

Utiliser `/create-skill`, puis vérifier : nom identique au dossier, workflow
réutilisable, ressources relatives, condition de succès et stratégie d'échec.

### Nouvelle instruction

Créer une instruction ciblée seulement si la règle doit s'appliquer
automatiquement à une famille de fichiers. Éviter `applyTo: "**"` sauf règle
réellement universelle.

## Critères de qualité

- **Découvrable** : la description contient les mots employés dans les demandes.
- **Borné** : le composant indique ce qu'il ne fait pas et quand il s'arrête.
- **Minimal** : outils et contexte sont limités au besoin réel.
- **Observable** : le résultat et sa validation peuvent être vérifiés.
- **Composable** : agents et skills communiquent par des sorties explicites.