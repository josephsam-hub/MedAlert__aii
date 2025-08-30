# MedAlert AI
#App link :https://appzi71fzuwhvktx.qraptor.ai/#/

> ⚠️ **Medical & Safety Disclaimer**
>
> MedAlert AI is **not a substitute** for professional medical advice, diagnosis, or treatment. In an emergency, call your local emergency number immediately.

A mobile‑first, **agent‑orchestrated emergency medical assistant** that delivers real‑time **triage**, **emergency coordination**, **nearest‑hospital lookup**, and **step‑by‑step first‑aid** using AI and APIs.

---

## ✨ Features

* **Instant Symptom Analysis** — Enter symptoms, age, and medical history for immediate triage using AI.
* **Emergency Coordination** — Clear recommendations: call ambulance, urgent care, or self‑care based on severity.
* **Hospital Finder** — Finds and displays the nearest hospitals using Google Maps Places API.
* **Step‑by‑Step First Aid** — Contextual first‑aid guidance tailored to the user’s situation.
* **Mobile‑First UI** — Fast, responsive experience for time‑critical use.
* **Agent Orchestration** — Multiple AI agents collaborate for accuracy and speed.

---

## 🧠 How It Works

1. **Input** — User enters symptoms, age, medical history, and (optionally) location.
2. **Processing** — AI agents assess urgency, recommend actions, locate hospitals, and draft first‑aid instructions.
3. **Output** — Clear, actionable guidance for rapid decision‑making.

**Real‑World Scenario**

> Tested on simulated cases (e.g., chest pain + breathlessness) to validate quick assessment, instant emergency guidance, live hospital lookup, and first‑aid support in real time.

---

## 🏗️ Tech Stack

* **[qRaptor](https://qraptor.ai/)** — Agent‑native workflow platform
* **GPT‑based LLM agents** — Triage, guidance, and instruction generation
* **Google Maps Places API** — Nearby hospital search & details
* **Responsive Web Front‑End** — Mobile‑first layout with custom CSS

---

## 🚀 Quick Start

### 1) Prerequisites

* Node.js 18+ (for front‑end) *(optional, adapt to your stack)*
* qRaptor account & workspace
* API keys: `QRAPTOR_API_KEY`, `OPENAI_API_KEY`, `GOOGLE_MAPS_API_KEY`

### 2) Environment

Create a `.env` file (or use your deployment’s secret manager):

```bash
QRAPTOR_API_KEY=your_qraptor_key
OPENAI_API_KEY=your_openai_key
GOOGLE_MAPS_API_KEY=your_google_maps_key
```

### 3) Configure Agents & Flows (qRaptor)

* Import or build flows for: **Triage Agent**, **Emergency Action Agent**, **Hospital Finder Agent**, **First‑Aid Agent**.
* Connect tools: LLMs (GPT), Google Maps Places API, optional geolocation.
* Expose the flow via qRaptor endpoint or embed in the front‑end.

### 4) Run the App

* Deploy your front‑end (e.g., Vercel/Netlify) or run locally.
* Point the UI to your qRaptor endpoint.

---

## 📱 Usage

1. Open the web app on mobile.
2. Enter **symptoms**, **age**, **medical history**, and **location** (or allow geolocation).
3. Receive: **triage level**, **recommended action**, **nearest hospitals**, and **first‑aid steps**.

---

## 🎥 Demo

Watch the demo: **[MedAlert AI Demo](https://appzi71fzuwhvktx.qraptor.ai/#/)**


---

## 🗺️ Architecture (High‑Level)

```text
[Mobile UI]
   │
   ├─ Collects inputs: symptoms, age, history, location
   │
   ▼
[qRaptor Orchestration]
   ├─ Triage Agent (GPT)
   ├─ Emergency Action Agent (GPT)
   ├─ Hospital Finder (Google Places)
   └─ First‑Aid Instruction Agent (GPT)
   │
   ▼
[Response Builder] → Structured results for UI (severity, actions, hospitals, steps)
```


## 🔐 Privacy & Security

* User inputs are processed only to provide assistance.
* Store as little data as possible; prefer **ephemeral** logs.
* If persisting, encrypt at rest and in transit; restrict PII access.
* Provide a **Data Use Notice** in‑app.

---

## 🧪 Testing

* Include simulated cases (e.g., chest pain, allergic reaction) to validate:

  * Triage accuracy
  * Action recommendations
  * Hospital lookup
  * First‑aid clarity



## 🛣️ Roadmap

* Offline fallback (cached first‑aid steps)
* Multilingual support
* Accessibility & voice input
* Wearable and sensor integrations
* Incident export (PDF) for handoff to clinicians

## 👥 Team

Developed by joseph sam mand Manivelavan k for **A2HackFest 2025**.


## 🤝 Contributing

Pull requests welcome! Please open an issue to discuss major changes.



