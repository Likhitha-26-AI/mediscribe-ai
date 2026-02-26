# MedRoute — AI-Powered Clinical Triage & Care Navigation

[![MedGemma](https://img.shields.io/badge/Powered%20by-MedGemma-blue)](https://huggingface.co/google/medgemma-4b-it)
[![HuggingFace](https://img.shields.io/badge/Model-HuggingFace-yellow)](https://huggingface.co/spark-2026/medroute-medgemma-finetuned)
[![Demo](https://img.shields.io/badge/Demo-HuggingFace%20Spaces-green)](https://huggingface.co/spaces/spark-2026/MedRoute)

A 4-agent AI pipeline that guides patients from symptom description to a clinician-ready care plan in under 2 minutes using fine-tuned MedGemma — Google's Health AI Developer Foundations model.

---

## Problem

Over 136 million patients visit US emergency rooms annually — 40–50% for non-emergency conditions, costing $38 billion annually. Patients don't know where to seek care. MedRoute solves this.

---

## Solution

MedRoute uses a 4-agent pipeline powered by fine-tuned MedGemma-4B:

| Agent | Role |
|---|---|
| Agent 1 — Clinical Intake | Extracts symptoms, asks follow-up question |
| Agent 2 — Triage Classifier | Fine-tuned MedGemma classifies urgency (0-3) |
| Agent 3 — Care Navigator | Personalized care plan |
| Agent 4 — Clinical Handoff | SOAP-format physician note |

---

## Model

- **Base Model:** google/medgemma-4b-it
- **Fine-tuning:** LoRA (r=8, alpha=16)
- **Dataset:** 18,000 synthetic patient triage records
- **Training Loss:** 1.6509 → 0.2792 (83% reduction)
- **Accuracy:** 90% (9/10 test cases)
- **Fine-tuned Model:** [spark-2026/medroute-medgemma-finetuned](https://huggingface.co/spark-2026/medroute-medgemma-finetuned)

---

## Demo

- **Live Demo:** [HuggingFace Spaces](https://huggingface.co/spaces/spark-2026/MedRoute)
- **Video:** [YouTube](https://youtu.be/-ziJYH_IQvU)

---

## Setup
```bash
pip install transformers accelerate peft trl gradio
```
```python
from huggingface_hub import login
login("your_hf_token")
```

---

## Run

Open `medroute_demo.ipynb` in Kaggle or Colab with GPU enabled and run all cells.

---

## Results

| Case | Expected | Predicted | Result |
|---|---|---|---|
| Chest pain, HR 147, ambulance | 3 Emergency | 3 | ✅ |
| Mild pain, walk-in | 0 Non-Urgent | 0 | ✅ |
| O2 92%, pain 4/10 | 1 Less Urgent | 1 | ✅ |
| HR 58, pain 2/10 | 0 Non-Urgent | 0 | ✅ |
| Pain 5/10, 2 chronic | 1 Less Urgent | 1 | ✅ |
| HR 130, O2 88%, ambulance | 3 Emergency | 3 | ✅ |
| BP 180, pain 7/10 | 2 Urgent | 2 | ✅ |
| Temp 39.5°C, pain 6/10 | 2 Urgent | 2 | ✅ |
| Age 72, 4 chronic, ambulance | 3 Emergency | 2 | ❌ |
| Mild pain, walk-in | 0 Non-Urgent | 0 | ✅ |

**Accuracy: 9/10 (90%)**

---

## Deployment

Because MedGemma is open-weight, MedRoute can be deployed entirely on-premise — zero patient data leaving the facility, fully HIPAA compliant.

**Roadmap:**
- Phase 1: Hospital kiosks (quantized on-device)
- Phase 2: EHR integration via HL7 FHIR API
- Phase 3: Offline rural mobile app

---

## Author

G. Likhitha Rao — AI/ML Student
Built for the MedGemma Impact Challenge 2026

---

## License

MIT License
........
