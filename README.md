# EpiGraph

Anonymous code release for the submitted paper. 

## Included files

```text
epigraph/
  build_kg.py       Lightweight knowledge-graph construction
  retrieval.py      Graph retrieval and reasoning-path serialization
  metrics.py        Evaluation metrics
  common.py         Shared I/O and model-client utilities
tasks/
  t1_clinical_decision_accuracy.py
  t2_clinical_report_generation.py
  t3_biomarker_precision_medicine.py
  t4_treatment_recommendation.py
  t5_deep_research_planning.py
configs/default.json
examples/
requirements.txt
```

Project websites, large datasets, generated outputs, and
deployment scripts will be released in camera-ready version.

## Installation

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Generation tasks use an OpenRouter-compatible endpoint. Supply credentials at
runtime; credentials are never stored in this repository.

```bash
export OPENROUTER_API_KEY="<your-key>"
```

## Minimal examples

Run Task 1 without retrieval:

```bash
PYTHONPATH=. python tasks/t1_clinical_decision_accuracy.py \
  --dataset examples/t1_item.json \
  --model openai/gpt-4o \
  --mode no_rag \
  --out runs/t1_no_rag.json
```

Run the same task with Graph-RAG after placing the paper-aligned triplet file
at `data/epikg/triplets.json`:

```bash
PYTHONPATH=. python tasks/t1_clinical_decision_accuracy.py \
  --dataset examples/t1_item.json \
  --triplets data/epikg/triplets.json \
  --model openai/gpt-4o \
  --mode graph_rag \
  --out runs/t1_graph_rag.json
```

Build a lightweight graph preview from locally available PMC XML files:

```bash
python -m epigraph.build_kg \
  --pmc_dir /path/to/pmc_xml \
  --out_dir data/epikg
```

Each task script supports `--help` for its task-specific inputs and output
schema.

## Data availability

Large benchmark and graph files are omitted from the anonymous repository.
Task 2 uses credentialed EEG data and is represented only by code plus the
synthetic schema example in `examples/t2_harvard_local_schema.jsonl`. No patient
record or restricted clinical text is included.


## License

See `LICENSE`.
