# AI-Powered Personal Learning Assistant (Telegram Bot)

This project is an AI-driven educational assistant delivered as a Telegram bot. Built using **n8n**, **Supabase**, and **Google Gemini 2.5 Flash Lite**, the system helps users process long educational articles, creates structured summaries, and generates interactive comprehension quizzes to track progress.

---

## 🚀 Features

- **Teacher AI Role (`/learn`):** Fetches web content, extracts key concepts, identifies difficulty levels, and provides structured summaries (5–7 key points).
- **Examiner AI Role (`/quiz`):** Dynamically generates a 5-question multiple-choice quiz based on saved materials. Handles interactive "one-by-one" flows and provides intelligent response validation.
- **Global Progress Tracker (`/stats`):** Persists data across sessions, calculates total quizzes taken, and displays overall lifetime accuracy.
- **Bulletproof Fallback System:** Uses advanced routing logic to filter out wrong texts and command structures, preventing the bot from freezing and guiding the user with a helpful menu.

---

## 📋 Prerequisites & Tech Stack

To run or inspect this workflow, the following components are used:
- **n8n** (Cloud or self-hosted) – Workflow automation engine
- **Supabase** (PostgreSQL) – Database for storing learning materials, active quiz sessions, and user global stats
- **Google Gemini API** (Model: `gemini-2.5-flash-lite`) – AI engine for summaries and quiz generation
- **Telegram Bot API** – User interface

---

## 🛠️ Step-by-Step User Guide

Follow these steps to interact with the bot and test its full functionality:

### Step 1: Initialize the Bot
Send the `/start` command to open the conversation. If you send any unrecognized message or typo, the built-in **Fallback System** will instantly send you an interactive help menu with valid command formats.

### Step 2: Submit Learning Material
Send the `/learn` command followed by a URL to an educational article **in the same message**.
* **Example:** `/learn https://example.com/useful-article`
* **What happens:** The bot will fetch the page, the **Teacher Agent** will analyze it, and you will receive a structured summary containing 5–7 bullet points, core concepts, and the assessed difficulty level. The data is saved to the database.

### Step 3: Start a Quiz
Send the `/quiz` command to test your comprehension.
* **What happens:** The bot will offer you an inline keyboard to choose the topic (e.g., *Latest Material* or *Random Material*). 
* Once selected, the **Examiner Agent** prepares 5 unique multiple-choice questions.

### Step 4: Answer Questions (One-by-One Flow)
Questions will appear one by one with inline buttons (**A**, **B**, **C**).
* Click a button to answer.
* The bot will instantly reply with a verdict (✅ Correct or ❌ Incorrect), provide an AI-generated explanation if you missed it, and **immediately send the next question**.

### Step 5: Check Your Global Stats
At the end of the 5th question, the bot calculates your score percentage and saves it to your permanent profile. 
* Send the `/stats` command at any time.
* **What happens:** The bot queries the database and returns your lifetime learning progress, including total quizzes completed, total correct answers, and your overall accuracy percentage.
