# mediscribe-ai
# Aira — Offline Emergency Response Assistant  
MedGemma Impact Challenge 2026 
Named it AIRA because:
A - Artificial
I - Intelligence
R - Response
A - Assitant

## Overview

Aira is an **offline-first emergency triage assistant** designed for disaster zones and rural settings where internet connectivity is unreliable or completely absent.

This repository contains the **first working prototype** of the system:

- A **rule-based emergency engine** that behaves like a senior emergency doctor for a few critical scenarios
- A **Gradio web UI** to interact with the assistant
- A **Hugging Face Space deployment** for a permanent live demo

The long-term goal is to plug this logic into an on-device **MedGemma / Gemma** model (HAI-DEF) so that the reasoning becomes fully model-driven while still running on edge devices.

---

## What I Implemented Today

### 1. Concept & Scope

- Defined the core **use case**:  
  An assistant that can guide first responders through **triage and immediate actions** for life‑threatening emergencies when:
  - There is **no internet**
  - There is **no senior doctor** available
  - Time is measured in **seconds–minutes**

- Chosen target scenarios for the prototype:
  - Sucking chest wound / open pneumothorax
  - Acute epiglottitis in a child (airway emergency)
  - Acute cardiogenic pulmonary edema
  - Femoral fracture with hemorrhagic shock
  - Severe anaphylaxis

### 2. Rule-Based Emergency Engine (Prototype Brain)

Because of repeated GPU and generation issues with MedGemma/Gemma in Colab, I implemented a **deterministic rule-based engine** to simulate how the assistant should behave.

Today’s engine:

- Takes a **free-text patient description** as input  
  (e.g. *“19yo male, stab wound to left chest, sucking sound, pale, agitated, BP 85/50, HR 138”*)
- Does simple **keyword / pattern matching** on the text
- Returns a **structured, medically realistic plan** for that scenario:
  - Triage level
  - Likely diagnosis
  - Step‑by‑step immediate actions
  - Short advice to the responder

Example (open pneumothorax):

```text
TRIAGE → IMMEDIATE

OPEN PNEUMOTHORAX → SUCKING CHEST WOUND

1. Seal wound NOW with occlusive dressing (3 sides taped or chest seal)
2. High-flow oxygen 15L/min
3. Monitor for tension pneumothorax → needle decompress if needed
4. Urgent trauma center — do not delay
This gives me a ground truth template for how the AI should eventually respond once MedGemma/Gemma is wired in.
3. Gradio UI
I created a simple Gradio interface around the emergency logic:

Input: multi-line textbox – “Patient Presentation”
Output: multi-line textbox – “Aira / MERS Response”
Includes example cases for quick testing:
Stab wound to left chest with sucking sound
Child with drooling, stridor, can’t swallow
Heart failure with pink frothy sputum
Femur fracture with shock
Severe anaphylaxis after peanuts
This UI is what I will use in:

The demo video
The judges’ live interaction via Hugging Face Space
4. Hugging Face Space Deployment
I deployed the prototype UI + logic as a permanent Space:

Live demo (permanent):
https://huggingface.co/spaces/spark-2026/mers-medgemma

Uses the app.py file with the Gradio interface.
Does not rely on any external API keys or GPUs → will continue to work through the entire competition period (up to March 2026 and after).
This Space link is what will be included in the Kaggle writeup and demo video.
Current Architecture (Prototype)
text

User (First Responder)
        ↓
Gradio UI (Hugging Face Space)
        ↓
Aira Emergency Engine (rule-based)
        ↓
Structured Response:
- TRIAGE level
- LIKELY DIAGNOSIS
- IMMEDIATE ACTIONS
- ADVICE
Today’s version uses a handcrafted rule engine for a small but critical set of emergencies.
The next step is to replace the rule-based engine with a MedGemma / Gemma model running locally (4‑bit quantized) and fine-tuned on these patterns.

Technology Stack
Python 3
Gradio (UI + deployment to Hugging Face Spaces)
Hugging Face Spaces (spark-2026/mers-medgemma) for permanent hosting
Planned (not fully wired in yet, but explored in Colab today):

google/medgemma-1.5-4b-it
google/gemma-2b-it
4-bit quantization for edge deployment
Integration via transformers + accelerate

got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions...
got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions...
got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions...
got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions...
got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions
got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions
got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions
other feature i included which is a voice input.in most of the scenarios the user might no be physically got a ui login page in which the user will give the description of the patient and ARIA will give a detailed descrition if what to do in various emergency situations.
This is if the patiient is not so severly injured .
which is the cause of the rise of the other feature i included which is a voice input.in most of the scenarios the user might no be physically present , i mean way too much shocked to even type the iput so inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions
This is if the patiient is
inorder to solve this a voice input is added just one click the speaker will deliver the situation and explain the seriousness of the injury to ARIA and she will assist the user in their next steps in such emergency sitautions
This is if the patiient is
in their next steps in such emergency sitautions
This is if the patiient is 


