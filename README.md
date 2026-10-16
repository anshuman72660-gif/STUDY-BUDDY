# 📚 Study Buddy: Your Personal AI Learning Assistant

**Hackathon project by Team KATIX**

Study Buddy is an AI tutor that is available to students whenever they have a doubt. It explains difficult concepts in simple language, solves problems step by step, summarizes notes and PDFs, generates quizzes, and builds study plans that fit a student's real available time. Every answer is generated live by a large language model (the Claude API). There are no hardcoded replies.

## 👥 Team KATIX

| Member |
|---|
| Anshuman |
| Manish |
| Kaustubh |
| Rudra |
| Ankit |

## 🎯 The problem

- Many students, especially in Class 11 and 12 and in competitive exam preparation, cannot get a teacher's help at the moment they are stuck.
- Private tutoring is expensive and not available to everyone.
- Textbooks and notes are long, and students often do not know what to revise first.
- Most study tools give answers without building understanding.

## 💡 Our solution

A personal AI tutor that teaches the concept behind the answer. It adapts to the student's level (beginner, intermediate, advanced) and to how they want to learn (four learning modes), and it can quiz them and plan their time.

**Target users:** school students, Class 11 and 12 students, college students, competitive exam aspirants, and anyone who needs a simple explanation of a hard topic.

## ✨ Features

| Feature | What it does |
|---|---|
| **AI Study Chat** | Ask any academic question and follow up. Keeps conversation context. Clear and New conversation buttons. |
| **Doubt Solver** | Identifies the topic, explains the concept, solves step by step, gives the final answer and a practice question. A **hints only** option withholds the answer. |
| **Notes Summarizer** | Paste notes or upload a text-based PDF to get a summary, key concepts, definitions and formulas, and revision points. |
| **Quiz Generator** | Pick subject, topic, difficulty and number of questions. Gets original 4-option MCQs, with answers hidden until you submit, then a score and explanations. |
| **Study Planner** | Takes subjects, difficult topics, daily hours and exam date, and returns a realistic plan with breaks and revision sessions. |
| **Learning Modes** | Simple Explanation, Exam Preparation, Step-by-Step Tutor, Quiz Me. Each mode changes the actual instructions sent to the AI. |

The interface is a responsive light blue and white dashboard that works on phones and laptops.

## 🧠 AI technology

- **Model provider:** Anthropic Claude API.
- **Prompting:** a tutor system prompt (explain clearly, never fabricate sources, adapt to level) combined with a mode-specific instruction for each learning mode.
- **Structured output:** the quiz feature asks the model for JSON, which the app validates (4 options, valid answer index) before showing it.
- **PDF handling:** text is extracted from PDFs and limited to 12,000 characters. The app tells the user when material is cut.

## 🗂️ Two versions in this repository

```
study-buddy/
├── index.html          Standalone version: one file, no install
├── flask-version/      Full Python/Flask backend version
├── README.md
├── LICENSE
└── .gitignore
```

| | Standalone (`index.html`) | Flask (`flask-version/`) |
|---|---|---|
| Stack | HTML, CSS, JavaScript | HTML, CSS, JavaScript + Python, Flask |
| API key | Entered by the user in Settings, stored in their browser | Stored in a server-side `.env` file |
| PDF reading | PDF.js in the browser | PyPDF on the server |
| Rate limiting | Short delay between requests | 30 requests per minute per IP |
| Best for | Quick demo, GitHub Pages | Keeping the key private on a server |

## 🚀 Getting started

### Get an API key
Create a key at [console.anthropic.com](https://console.anthropic.com). Free credits and rate limits change over time, so check the current pricing page. Do not assume a key is free.

### Option 1: Standalone (fastest)
1. Open `index.html` in Chrome.
2. Go to **Settings**, paste your API key, and click **Save**.
3. Start asking questions.

Your key is kept only in your browser's localStorage and is sent only to `api.anthropic.com`. Use your own device, set a spend limit in the Anthropic console, and never commit a key into the file.

### Option 2: Flask version
```bash
cd flask-version
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env            # then add your ANTHROPIC_API_KEY
pytest                          # optional: run tests
python app.py                   # open http://127.0.0.1:5000
```

### Host the standalone version on GitHub Pages
Repository **Settings → Pages → Deploy from branch → `main` / root**. Each visitor uses their own API key.

## 🎬 Demo flow

1. Open the dashboard and ask: *"Explain Newton's second law."*
2. Ask a follow-up and switch to **Exam Preparation** mode to show the answer change.
3. Paste a chapter (or upload a PDF) in **Notes Summarizer** to get revision notes.
4. Generate a quiz (Physics / Motion / medium / 5), answer it, and submit to see the score.
5. Create a **Study Plan** with 3 hours per day and an exam date.

## 📈 Expected benefits

- Help at any time, for any subject, at the student's own level.
- Understanding of concepts instead of memorized answers.
- Faster revision from auto-generated notes and quizzes.
- Study schedules that match the time a student really has.

## ⚠️ Limitations

- Notes are capped at 12,000 characters and PDFs at 5 MB. Scanned or image-only PDFs are not supported.
- Math is shown as plain text, not typeset.
- Nothing is saved between sessions. Chats live in the browser tab only.
- The AI can make mistakes, so students should verify important facts with their teachers and textbooks.
- Standalone version: the API key lives in the user's browser, rate limiting is only a short delay, and quiz answers sit in page memory until submission.
- Flask version: the rate limiter and quiz store are in memory and work for a single process only.

## ✅ Testing status

The Python files and embedded JavaScript pass syntax checks. The Flask test suite (`flask-version/tests`) covers startup, the health endpoint, invalid input, missing API key, API failure handling, quiz validation and PDF validation, using mocked AI responses. **The tests and live API calls had not been run when this README was written**, so run `pytest` and try a real chat before demoing.

## 🛠️ Troubleshooting

| Problem | Fix |
|---|---|
| "API key is not set" or "No API key" | Flask: check `.env` is in `flask-version/` and restart. Standalone: paste the key in Settings. |
| "The API key was rejected" | Generate a new key in the Anthropic console. |
| "Rate limited" | Wait a minute and retry. |
| PDF says no text found | The PDF is scanned. Use a text-based PDF or paste the text. |
| PDF upload fails in the standalone version | PDF.js loads from the internet. Check your connection. |
| Page cannot reach the AI | Check your internet connection. |

## 🔮 Future scope

Login and saved progress, LaTeX math rendering, voice input, multi-language support, handwritten problem scanning, and progress analytics for students and teachers.

## 📄 License

MIT. See [LICENSE](LICENSE).

---
*Built with ❤️ by Team KATIX: Anshuman, Manish, Kaustubh, Rudra and Ankit.*
