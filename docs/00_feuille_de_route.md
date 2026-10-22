# LexCIV — Feuille de route

> **LexCIV** — Assistant IA de réponse juridique pour le droit du travail ivoirien et le droit des affaires OHADA, avec réponses sourcées et évaluées.
> Dépôt : `github.com/mdtech-ai/lexciv-rag`

## Problématique

PME, responsables RH et salariés ivoiriens se posent des questions juridiques au quotidien (période d'essai, préavis, congés, création de SARL…). Les textes officiels (Code du travail ivoirien, Actes uniformes OHADA) sont longs et difficiles à parcourir. Les assistants IA généralistes répondent souvent avec le droit **français**, inventent des articles ou ne citent pas de source.

**Question du projet** : un système RAG spécialisé, appuyé sur les textes officiels, répond-il plus juste qu'un LLM seul, en citant l'article exact — et de combien ?

## Objectifs

1. Construire un corpus propre à partir des textes officiels publics (Code du travail ivoirien + 2-3 Actes uniformes OHADA).
2. Répondre en français en citant l'article et le texte source ; refuser quand l'information n'est pas dans le corpus.
3. Mesurer la qualité sur un jeu de test construit et vérifié à la main (60-80 questions).
4. Améliorer le système version par version et chiffrer le gain de chaque version.
5. Déployer : API, interface de chat en ligne, Docker.

## Indicateurs (cibles indicatives — les résultats publiés seront ceux mesurés)

| Indicateur | Mesure | Cible |
|---|---|---|
| Recall@5 | Le bon article est dans les 5 passages retrouvés | ≥ 85 % |
| MRR | Le bon passage est classé haut | ≥ 0,70 |
| Exactitude | Réponse correcte (LLM-juge + échantillon vérifié à la main) | ≥ 80 % |
| Fidélité | Pas d'information hors sources | ≥ 90 % |
| Citation exacte | Le bon article est cité | ≥ 85 % |
| Refus correct | Refus des questions hors corpus | ≥ 90 % |
| Latence | Temps de réponse | < 5 s |

## Versions évaluées

| Version | Changement |
|---|---|
| v0 | LLM seul, sans documents (référence) |
| v1 | RAG naïf : découpage fixe + embeddings |
| v2 | Découpage par article (structure juridique) |
| v3 | Recherche hybride (BM25 + vecteurs) |
| v4 | Reranking (cross-encoder) |
| v5 (bonus) | Ajustement (fine-tuning) du modèle d'embeddings |

## Architecture

```
Collecte (PDF officiels) → Extraction (PyMuPDF / OCR Tesseract) → Nettoyage
→ Découpage par Livre/Titre/Chapitre/Article + métadonnées
→ Embeddings multilingues (bge-m3 / e5) → Qdrant + index BM25
→ Recherche hybride → Reranker → LLM (Groq / Ollama) avec citations + garde-fous
→ API FastAPI → Interface Streamlit
→ Évaluation (eval/) + tests (pytest) + GitHub Actions → Docker → Hugging Face Spaces
```

## Structure du dépôt

```
docs/ (cadrage, données, architecture, évaluation, adr/, journal.md)
data/ (raw, processed — ignorés par git)
src/lexciv/ (ingestion, processing, retrieval, generation, api)
app/ (Streamlit) · eval/ · tests/ · .github/workflows/
Dockerfile · docker-compose.yml · pyproject.toml · .env.example
```

## Planning

| Jour | Étape | Livrable |
|---|---|---|
| J1 – 21/10 | Cadrage, squelette du dépôt, collecte des textes | `01_cadrage.md`, PDF récupérés |
| J2 – 22/10 | Extraction, nettoyage, découpage par article | Corpus structuré, `02_donnees.md` |
| J3 – 23/10 | Indexation, RAG v1 fonctionnel | Premières réponses |
| J4 – 24/10 | Jeu d'évaluation + scripts de mesure | Scores v0 et v1 |
| J5 – 25/10 | v2, v3, v4 mesurées | Tableau comparatif |
| J6 – 26/10 | API, interface, Docker, tests | App complète en local |
| J7 – 27/10 | Déploiement, README, schéma, GIF démo | Dépôt présentable |
| J8 – 28/10 | CV mis à jour avec les chiffres, candidature SKAN | Candidature envoyée |
| Après | v5 (fine-tuning embeddings) | Bonus entretien |

## Projets suivants du portfolio

2. **KYC Copilot** — OCR/vision, extraction LLM, agents (tool calling), scoring ML, explicabilité, PostgreSQL, dashboard.
3. **Prévision & MLOps** (ex. churn mobile money) — XGBoost, MLflow, CI/CD, monitoring de dérive, API.
