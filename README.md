[README.md](https://github.com/user-attachments/files/26243213/README.md)
# AI Resume Analyser 🧠

[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Groq](https://img.shields.io/badge/Groq-LLaMA_3.3_70B-F55036?style=for-the-badge)](https://groq.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)](LICENSE)

Hiring the right person for an IT or cybersecurity role is harder than it looks. Most resume screeners are generic — they don't know the difference between what a SOC analyst needs versus a penetration tester, and they definitely can't tell you *why* a candidate might fail a technical interview three rounds in.

This tool was built to fix that. Upload a resume, select the role you're hiring for, and get a full AI-powered breakdown in seconds — scores, skill gaps, red flags, improvement suggestions, suggested interview questions, and a final hire/reject decision backed by reasoning.

---

## What it actually does

When you upload a resume, the app runs it through LLaMA 3.3 70B via Groq's API. The AI evaluates the candidate specifically for the role you selected — not generically. A penetration tester gets judged on Metasploit and OSCP. An AI/ML engineer gets judged on PyTorch and model evaluation. Every role has its own scoring weights.

Here's what you get back:

- **Overall score** with a gauge showing hire/review/reject zone
- **6-dimension breakdown** — Technical Skills, Cybersecurity Relevance, Experience, Education, Soft Skills, ATS Compatibility
- **Radar chart** comparing the candidate against industry averages
- **Skills audit** — what they have, what they're missing, what certifications they should get
- **Strengths and weaknesses** referenced directly to resume content, not generic observations
- **Improvement plan** with HIGH / MEDIUM / LOW priority action items
- **3 suggested interview questions** targeting the specific gaps found
- **Final decision** — HIRE, MAYBE, or REJECT — with a confidence score and written reasoning
- **Downloadable report** in `.txt` or `.json` format

---

## Roles supported

The app currently evaluates candidates for 7 IT and cybersecurity roles, each with its own required skills, preferred skills, and scoring weights:

| Role | Focus |
|---|---|
| 🔴 Penetration Tester / Ethical Hacker | Offensive security, exploit dev, bug bounty |
| 🔵 Security Analyst (SOC / DFIR) | SIEM, incident response, threat hunting |
| 🟢 DevSecOps Engineer | CI/CD security, containers, cloud pipelines |
| 🟡 Full Stack Developer (Security-Focused) | Secure coding, REST APIs, frontend + backend |
| 🤖 AI / ML Engineer | PyTorch, model evaluation, MLOps, LLMs |
| 🌐 Network Security Engineer | Firewalls, VPN, routing, IDS/IPS |
| ☁️ Cloud Security Engineer | AWS/Azure/GCP, IAM, CSPM, compliance |

---

## Getting started locally

**1. Clone the repo**

```bash
git clone https://github.com/Tktirth/ai-resume-analyser.git
cd ai-resume-analyser
```

**2. Install dependencies**

```bash
pip install -r requirements.txt
```

**3. Add your Groq API key**

Create a `.env` file in the root folder:

```
GROQ_API_KEY=gsk_your_key_here
```

You can get a free API key at [console.groq.com](https://console.groq.com). No credit card required.

**4. Run the app**

```bash
streamlit run app.py
```

Open [http://localhost:8501](http://localhost:8501) and you're good to go.

---

## Deploying to Streamlit Cloud

If you want to host it publicly:

1. Push this repo to your GitHub account
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub
3. Click **New app** → select this repo → set main file to `app.py`
4. Open **Advanced settings → Secrets** and add:

```toml
GROQ_API_KEY = "gsk_your_key_here"
```

5. Hit **Deploy** — it'll be live in 2-3 minutes

---

## Project structure

This project ships as a single file for simplicity. Everything — the parser, AI engine, charts, and UI — lives in `app.py`.

```
ai-resume-analyser/
├── app.py                  # Everything in one file
├── requirements.txt        # Python dependencies
├── .env.example            # API key template
├── .gitignore
└── .streamlit/
    └── config.toml         # Dark theme configuration
```

---

## Tech stack

| What | How |
|---|---|
| UI | Streamlit |
| AI Model | LLaMA 3.3 70B Versatile via Groq API |
| PDF parsing | pdfplumber |
| DOCX parsing | python-docx |
| Charts | Plotly |
| Env management | python-dotenv |

---

## Known limitations

- **Scanned PDFs won't work.** The parser reads text directly from the file. If someone submitted a photo of their resume exported as PDF, it'll come back empty. They need to provide a text-based PDF.
- **Resume length matters.** The app sends up to 7,000 characters to the AI. Very long resumes get trimmed. Most standard resumes are well within this limit.
- **AI is not infallible.** The hire/reject recommendation is a starting point, not a final answer. Always have a human review before making a real hiring call.

---

## About this project

I built this as part of my portfolio while studying IT at GTU. The idea came from wanting to build something that sits at the intersection of AI, cybersecurity, and real-world HR workflows — not another CRUD app or weather dashboard.

The AI persona used in the prompts is "Dr. Alexandra Reid" — a fictional senior HR analyst with 20 years of cybersecurity hiring experience at firms like CrowdStrike and Palo Alto Networks. This gives the model a concrete evaluation frame rather than producing vague, generic output.

---

## Author

**Tirth** — Third year IT undergrad at Gujarat Technological University  
Certified in Ethical Hacking from IIT Delhi · Pursuing AI/ML from IIT Guwahati  
GitHub: [@Tktirth](https://github.com/Tktirth)

---

## License

MIT — use it, modify it, build on it. Just don't use it to make hiring decisions without a human in the loop.
