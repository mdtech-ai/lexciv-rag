# 01 — Cadrage du projet LexCIV

## 1. Contexte

En Côte d'Ivoire, les relations de travail sont régies par le Code du travail (loi n° 2015-532 du 20 juillet 2015) et la Convention collective interprofessionnelle de 1977 ; la vie des entreprises par les Actes uniformes de l'OHADA, applicables dans 17 États membres.

Ces textes sont longs, structurés en livres, titres, chapitres et articles, et rarement consultés directement par les non-juristes. Les assistants IA généralistes, de plus en plus utilisés pour ce type de questions, ont deux défauts majeurs dans ce contexte :

- ils mélangent les droits nationaux (réponses fondées sur le droit **français**) ;
- ils ne citent pas leurs sources ou inventent des références d'articles (hallucinations).

## 2. Problème

> Un responsable RH ou un dirigeant de PME ivoirienne qui se pose une question juridique simple n'a pas de moyen rapide et fiable d'obtenir une réponse fondée sur le bon texte, avec l'article de référence.

## 3. Utilisateurs cibles

| Utilisateur | Besoin type | Exemple de question |
|---|---|---|
| **Responsable RH de PME** (principal) | Appliquer correctement le droit du travail | « Quelle est la durée maximale de la période d'essai d'un cadre ? » |
| **Dirigeant / créateur d'entreprise** (principal) | Connaître les règles OHADA pour créer et gérer une société | « Quel est le capital minimum d'une SARL ? » |
| **Salarié** (secondaire) | Connaître ses droits | « À combien de jours de congés payés ai-je droit ? » |

## 4. Proposition de valeur

LexCIV répond en français, **en s'appuyant uniquement sur les textes officiels**, **cite l'article et le texte source** de chaque affirmation, et **refuse de répondre** lorsque l'information n'est pas dans son corpus.

## 5. Objectifs

1. Constituer un corpus propre et à jour des textes officiels (versions validées par un juriste).
2. Répondre avec citation exacte de l'article et du texte source.
3. Refuser les questions hors périmètre au lieu d'inventer.
4. Mesurer objectivement la qualité et la comparer à un LLM seul.
5. Améliorer le système version par version en chiffrant chaque gain.
6. Rendre l'outil accessible en ligne (API + interface de chat).

## 6. Périmètre

**Inclus (v1)**

- Code du travail ivoirien (version consolidée) et principaux décrets d'application
- Convention collective interprofessionnelle de 1977 et avenants
- Décret fixant le SMIG en vigueur
- Acte uniforme relatif au droit commercial général (AUDCG)
- Acte uniforme relatif au droit des sociétés commerciales et du GIE (AUSCGIE)

**Exclu (v1)**

- Jurisprudence, doctrine, conventions collectives de branche
- Droit fiscal, droit social CNPS (possible extension)
- Droit national des autres États OHADA
- Rédaction d'actes (contrats, statuts) et conseil sur un cas particulier

## 7. Ce que LexCIV n'est pas

LexCIV fournit de **l'information juridique**, pas un **conseil juridique**. Il ne remplace pas un avocat ou un juriste. Chaque réponse affiche un avertissement et recommande de consulter un professionnel pour toute situation litigieuse.

## 8. Critères de succès (indicateurs)

| Indicateur | Définition | Cible indicative |
|---|---|---|
| Recall@5 | Part des questions dont l'article attendu figure dans les 5 passages retrouvés | ≥ 85 % |
| MRR | Rang moyen inverse du premier passage pertinent | ≥ 0,70 |
| Exactitude | Part des réponses jugées correctes (LLM-juge + échantillon vérifié à la main) | ≥ 80 % |
| Fidélité | Part des réponses sans information absente des sources | ≥ 90 % |
| Citation exacte | Part des réponses citant le bon article | ≥ 85 % |
| Refus correct | Part des questions hors corpus correctement refusées | ≥ 90 % |
| Latence | Temps de réponse médian | < 5 s |

Les résultats publiés seront ceux effectivement mesurés, même s'ils n'atteignent pas ces cibles.

**Jeu d'évaluation** : 60 à 80 questions avec réponse et article de référence, dont une partie fournie et validée par un juriste, plus 10 à 15 questions hors corpus pour tester les refus.

## 9. Contraintes

- Outils gratuits ou à offre gratuite uniquement.
- Machine de développement : 16 Go RAM, GPU 4 Go → génération via API (Groq), modèles locaux légers en option (Ollama).
- Aucune donnée personnelle traitée : uniquement des textes juridiques publics.
- Délai : version présentable le 27/10/2026.

## 10. Risques

| Risque | Impact | Parade |
|---|---|---|
| Textes obsolètes ou non officiels | Réponses fausses | Versions validées par un juriste, date de mise à jour documentée |
| PDF scannés de mauvaise qualité | Erreurs d'extraction | OCR + contrôle manuel d'un échantillon d'articles |
| Hallucinations du LLM | Perte de confiance | Citations obligatoires, mesure de fidélité, refus hors corpus |
| Quotas de l'API gratuite | Évaluation interrompue | Mise en cache des réponses, alternative locale Ollama |
| Jeu d'évaluation biaisé | Chiffres non représentatifs | Questions écrites avant d'optimiser le système, validation par un juriste |
