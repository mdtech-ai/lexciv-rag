# LexCIV — instructions pour Claude

## Contexte

- Auteur : Mamadou DIALLO (GitHub `mdtech-ai`), jeune diplômé d'un Master IA & Big Data (ESP – UCAD, Dakar), Ivoirien basé à Dakar, en recherche d'un poste d'Ingénieur IA à Abidjan.
- Ce dépôt est le **projet de portfolio n°1** (sur 3) destiné à prouver des compétences IA générative demandées par les recruteurs (offre cible immédiate : Ingénieur Développeur IA chez SKAN Technologies, date limite 30/10/2026).
- Feuille de route détaillée, objectifs et planning : [docs/00_feuille_de_route.md](docs/00_feuille_de_route.md).

## Règles de travail (convenues avec l'auteur)

1. **Pédagogie d'abord** : l'auteur doit pouvoir défendre chaque ligne en entretien.
   - Avancer par petites étapes. Avant de coder, expliquer le concept en quelques lignes simples.
   - C'est l'auteur qui lance les commandes et regarde les résultats ; ne pas tout générer d'un bloc.
   - À la fin de chaque étape : proposer une entrée pour `docs/journal.md` et poser 3 questions type entretien sur l'étape.
2. **Honnêteté des résultats** : ne jamais inventer de chiffres. Les résultats publiés (README, CV) sont ceux mesurés par `eval/`, même s'ils sont moins bons que les cibles. Si une info manque, poser la question.
3. **Qualité de dépôt** : code propre et typé, docstrings courtes, tests `pytest`, README soigné, ADR pour chaque choix technique important (`docs/adr/`).
4. **Langue** : échanges et documentation en français ; code, noms de variables et commits en anglais.
5. **Secrets** : clés API uniquement dans `.env` (jamais commité) ; maintenir `.env.example`.
6. **Machine de l'auteur** : Windows 11, 16 Go RAM, GPU NVIDIA Quadro T2000 (4 Go), Python 3.12, Docker, Ollama, Git. LLM de génération via Groq (API gratuite) ; Ollama (petit modèle 3-4B) en alternative locale.
7. **Ne pas commiter** de fichiers personnels (CV, etc.) ni les données brutes volumineuses.
