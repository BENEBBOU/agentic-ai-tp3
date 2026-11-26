# TP3 - RAG multimodal agentique

Notebook : [`TP3_RAG_multimodal_agentique.ipynb`](TP3_RAG_multimodal_agentique.ipynb)

Application RAG qui extrait, indexe et interroge le texte **et les images** de l'article *Attention Is All You Need* :

1. Extraction PyMuPDF (texte par page, fragments compatibles CLIP, images).
2. Embeddings **CLIP ViT-B-32** (open_clip) : texte et images dans le même espace, vecteurs normalisés.
3. Indexation **ChromaDB** (cosinus), identifiant SHA-256 pour éviter les réindexations inutiles, métadonnées.
4. Recherche par similarité cosinus à partir d'un texte **ou** d'une image.
5. `retriever_tool` : le retriever devient un outil pour un agent (schéma Pydantic, registre d'images).
6. Agent **ReAct** construit avec **LangGraph** : MIND (LLM) → BODY (ToolNode) → OBSERVATION (le LLM voit les figures retrouvées) → MIND.
7. Six scénarios de test (texte, figure, requête hybride texte + image, chiffres, information absente, salutation) et analyse du comportement de l'agent.

## Exécution

```bash
uv sync
echo OPENAI_API_KEY=sk-... > .env     # nécessaire pour les étapes 6 et 7
uv run jupyter lab
```

Le PDF de l'article (version NeurIPS 2017) est téléchargé automatiquement. Les étapes 1 à 5 tournent sans clé d'API.
