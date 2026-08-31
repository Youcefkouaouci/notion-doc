# Front-end ressources

# Introduction Figma

- Comprendre et Connaitre les nouveautés 2024 :

[https://www.youtube.com/watch?v=pBl6wcPVTO4](https://www.youtube.com/watch?v=pBl6wcPVTO4)

# Introduction à Figma

## Qu'est-ce que Figma ?

- **Définition** : Figma est un outil de design d'interface utilisateur basé sur le cloud qui permet la conception collaborative en temps réel.
- **Caractéristiques principales** : Interface intuitive, composants réutilisables, prototypage interactif, collaboration en temps réel.

## Pourquoi utiliser Figma ?

- **Collaboratif** : Plusieurs utilisateurs peuvent travailler simultanément sur un même projet.
- **Composants et styles** : Réutilisation de composants et de styles pour garantir la cohérence.
- **Prototypage** : Création de prototypes interactifs pour visualiser les interactions et transitions.

# Avantages de Figma pour Vue 3

- **Cohérence** : Utiliser un design system centralisé pour garantir la cohérence entre les maquettes et l'implémentation.
- **Flexibilité** : Adapter les composants Figma à différents écrans et résolutions avec les outils de mise en page de Vue.
- **Prototypage rapide** : Tester rapidement les interactions et ajuster les maquettes en fonction des retours avant l’implémentation.

# Présentation des Maquettes

## Maquette Dashboard : à compléter @Allan Pereira @Anonyme

[Charlie Solution](https://www.figma.com/design/LLLbUGnbqSBuXPDJLr4rMT/Charlie-Solution?node-id=276-6135&t=7Vbb4QlGCedwURgw-1)

- **Description :** *à definir @Allan Pereira @Anonyme (Présentation de la maquette du dashboard, avec ses différents écrans et fonctionnalités. ⇒ peut être une vidéo)*
- **Objectifs** : *Montrer la disposition des éléments, les flux utilisateur et les interactions clés.*

## Design System : à compléter @Allan Pereira @Anonyme

[Charlie Solution (Design System)](https://www.figma.com/design/gIpaShbkVph3lofVcadvbY/Charlie-Solution-(Design-System)?node-id=1-1180&t=rRZItmABhhYgOXu2-1)

- **Description** : *Explication du design system utilisé, incluant les styles, composants et conventions. ⇒ à définir avec ugo @Allan Pereira et @Anonyme*
- **Composants** : Liste des composants (boutons, formulaires, cartes, etc.) et leurs variations sous forme de tableau par exemple ?
- **Styles** : Couleurs, typographie, espacements, etc.

# Boucle de Retour d'Information Itérative

L'intégration de Figma et Vue.js soutient un processus de conception et de développement itératif, permettant des ajustements rapides et une cohérence entre le design et le développement :

## Cycle Itératif

- **Réactivité aux Changements** : Les modifications apportées au design dans Figma peuvent être rapidement communiquées et intégrées dans le développement Vue.js.
- **Synchronisation Continue** : Ce cycle itératif assure que le produit final reste fidèle à l'intention initiale du design, tout en permettant des ajustements et des améliorations basés sur les retours et les tests.

## Processus

1. **Conception** : Le designer crée ou ajuste les maquettes dans Figma.
2. **Développement** : Les développeurs intègrent les designs dans Vue.js en utilisant les composants et les assets fournis.
3. **Retour d'Information** : Les développeurs fournissent des retours sur les aspects techniques et les incohérences potentielles.
4. **Révision** : Les designers ajustent les maquettes en fonction des retours reçus.
5. **Répétition** : Le cycle se répète jusqu'à ce que le design et le développement soient alignés.

## Avantages

- **Alignement** : Maintien de la cohérence entre le design et le produit final.
- **Flexibilité** : Adaptation rapide aux changements de design et aux nouvelles exigences.
- **Qualité** : Amélioration continue de la qualité du produit grâce à des ajustements basés sur les retours réels.

# Meilleures Pratiques pour un Flux de Travail Fluide

## Communication Régulière

- **Objectif** : Assurer que les designers et les développeurs sont toujours alignés sur les objectifs du projet, les détails du design, et les considérations techniques.
- **Réunions** : Planifier des réunions régulières pour discuter des progrès, des défis, et des ajustements nécessaires.

## Compréhension Partagée des Limitations

- **Compétences** : Les designers doivent comprendre les capacités et les limitations de Vue.js, tandis que les développeurs doivent connaître les fonctionnalités et les contraintes de Figma.
- **Expectations Réalistes** : Établir des attentes réalistes concernant ce qui peut être réalisé dans le design et le développement, pour éviter les malentendus et les retards.

## Contrôle des Versions

- **Figma** : Utiliser la fonctionnalité d’historique des versions de Figma pour suivre les modifications apportées aux maquettes, revenir à des versions précédentes si nécessaire, et gérer les changements de manière structurée.
- **Code** : Tout comme les développeurs utilisent des outils de contrôle des versions (comme Git) pour le code, il est important que les designers gèrent les versions des fichiers de design pour maintenir la cohérence et l’organisation.

## Documentation

- **Instructions Claires** : Fournir des documents de spécifications détaillés pour les composants, les interactions, et les styles afin que les développeurs aient toutes les informations nécessaires.
- **Mises à Jour** : Mettre à jour la documentation régulièrement pour refléter les changements dans les designs et les exigences.

## Tests et Validation

- **Prototypes** : Utiliser les prototypes interactifs de Figma pour tester les interactions et les flux utilisateur avant l’implémentation dans Vue.js.
- **Révisions** : Tester régulièrement les versions développées pour s’assurer qu’elles respectent les maquettes et faire des ajustements si nécessaire.

# Transition Fluide de Figma à Vue.js

La transition entre le design et le développement implique plusieurs étapes clés, chacune facilitée par des outils et des pratiques qui garantissent fidélité et efficacité :

## Exportation des Assets depuis Figma

- **Formats Disponibles** : Figma permet d’exporter des assets dans divers formats (images, icônes) avec la résolution et le format adaptés pour le développement web.
- **Précision** : Assurer que tous les fichiers nécessaires sont fournis aux développeurs, prêts à être intégrés dans l'application

## Utilisation des Design Tokens

- **Définition** : Les design tokens sont des ensembles de décisions de design (comme les couleurs, les polices, et les espacements) définis dans Figma et traduits en code.
- **Consistance** : Ces tokens garantissent la cohérence du design à travers l’application et facilitent l’application de thèmes ou les modifications de design.

## **Création des composants Vue**

Comment créer des composants Vue basés sur les maquettes Figma.

- **Template** : Convertir les designs en templates Vue.
- **Style** : Intégrer les styles de Figma dans les fichiers `vue`.
- **Script** : Ajouter la logique nécessaire pour chaque composant.

## Cartographie des Composants

- **Système de Composants** : Le système de composants de Figma peut être directement mappé aux composants Vue.js.
- **Réutilisabilité** : Ce mappage direct assure que les éléments de design réutilisables dans Figma (comme les boutons et les champs de saisie) deviennent des composants réutilisables dans Vue.js, promouvant les principes DRY (Don’t Repeat Yourself) dans le développement.

## Prototypage et Interactions

- **Modèles Interactifs** : Les fonctionnalités de prototypage de Figma permettent de créer des modèles interactifs de la façon dont l’application doit fonctionner.
- **Référence pour le Développement** : Ces prototypes servent de référence pour les développeurs en Vue.js, garantissant que les aspects dynamiques du design sont implémentés avec précision.

[[Checklist d'Intégration des Maquettes](https://app.notion.com/p/1b89f47911474901999458e33b0cb0a3?pvs=21)](Front-end%20ressources/Checklist%20d'Int%C3%A9gration%20des%20Maquettes%203cace96be58b808dbb24f407b9b85c11.md)

[[Introduction à Tailwind UI](https://app.notion.com/p/9c938671e39141d2918ab98bf3bd1e83?pvs=21)](Front-end%20ressources/Introduction%20%C3%A0%20Tailwind%20UI%203cace96be58b8033b285ed23a7b10d2a.md)

[[Guide de Configuration du Fichier `tailwind.config.js`](https://app.notion.com/p/9a5e701b201542e783a21fe2e0928e8e?pvs=21)](Front-end%20ressources/Guide%20de%20Configuration%20du%20Fichier%20tailwind%20config%20%203cace96be58b80abbb5ada3c0e581d83.md)

[[Guide d'Intégration des Maquettes (avec Tailwind CSS)](https://app.notion.com/p/a0e9e7e68842446eb52fcac4544902ba?pvs=21)](Front-end%20ressources/Guide%20d'Int%C3%A9gration%20des%20Maquettes%20(avec%20Tailwind%20C%203cace96be58b80b49c9fc228940b5725.md)

[[Guide Composants Dynamiques](https://app.notion.com/p/85614f2240614153bb8d57b8e50cc53f?pvs=21)](Front-end%20ressources/Guide%20Composants%20Dynamiques%203cace96be58b805e82b8e260ac6b3bce.md)

[[De Vue 2 à Vue 3](https://app.notion.com/p/ac69fc8cb30546bf846ac14c57a9507c?pvs=21)](Front-end%20ressources/De%20Vue%202%20%C3%A0%20Vue%203%203cace96be58b807ebd28d361624f856e.md)

[[Normes et bonnes pratiques](https://app.notion.com/p/87d02ea2350542bb8f60b6bfc3cb4c7d?pvs=21)](Front-end%20ressources/Normes%20et%20bonnes%20pratiques%203cace96be58b8068bcf8c3cbedd786d0.md)

---

Annexe

[[Fichier de config Tailwind css](https://app.notion.com/p/e8992808afae4b729286925927db77f8?pvs=21)](Front-end%20ressources/Fichier%20de%20config%20Tailwind%20css%203cace96be58b80ba82a5f6d6e796e60a.md)

[[Ressources](https://app.notion.com/p/b10cbe4f41d74317b22f6ebcc03c0335?pvs=21)](Front-end%20ressources/Ressources%203cace96be58b80628388e4f5d63d3b28.md)

[[Tailwind CSS : Classes Utilitaires de Base](https://app.notion.com/p/8d3d4c43aecf4adab52869c2b8b65272?pvs=21)](Front-end%20ressources/Tailwind%20CSS%20Classes%20Utilitaires%20de%20Base%203cace96be58b806c8a97c265107a57e3.md)