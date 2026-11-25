# Laboratorio OWASP Top 10 LLM: LLM01 / LLM02 / LLM07

Entorno en Github Actionscon **Python + Ollama** (`llama3.2:3b`), sin APIs externas.
Reproduce la extracción del *system prompt* (Experimento 1) y la evaluación de
defensas habituales, delimitadores y filtro regex, con su bypass (Experimento 2).

> Solo para uso educativo, sobre un entorno propio y con secretos ficticios.

## Requisitos
- Python 3.10+
- [Ollama](https://ollama.com/download) instalado (~2 GB para el modelo, 8 GB de RAM recomendados)

## Instalación
```bash
ollama pull llama3.2:3b
pip install -r requirements.txt
```

## Uso
```bash
python lab.py exp1 --runs 5      # Experimento 1
python lab.py exp2 --runs 5      # Experimento 2
python lab.py all  --runs 5      # ambos + results/resumen.md (tablas 2 y 3)
python lab.py demo               # modo clase, paso a paso con Enter
python lab.py replay             # repite el último resultado guardado SIN modelo
python lab.py all --temperature 0.8   # para mostrar variabilidad
```
Todo se guarda en `results/` (JSON con cada respuesta completa + `resumen.md`).

## Cómo se decide si hay fuga
Se normaliza la respuesta (minúsculas, sin separadores) y se busca el secreto,
así que también cuenta `A_C_M_E-...`. **No** detecta Base64, traducciones ni otras
codificaciones: pueden existir fugas no contadas. Revisa a mano las respuestas
dudosas en los JSON.

## Ejecutar en la nube
- **GitHub Codespaces:** abre un Codespace, instala Ollama con
  `curl -fsSL https://ollama.com/install.sh | sh`, `ollama serve &`,
  `ollama pull llama3.2:3b` y lanza el script. Solo CPU, es lento.
- **GitHub Actions:** pestaña *Actions* → *Laboratorio LLM* → *Run workflow*.
  Los resultados se descargan como artefacto `resultados-lab`.
