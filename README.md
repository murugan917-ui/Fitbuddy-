# FitBuddy - AI Fitness Plan Generator using Gemini Models

FitBuddy is a web application that generates a personalized 7-day workout plan and a nutrition/recovery tip
using Google Gemini AI. Users can give feedback to update their plan, and an admin dashboard shows all users
and their plans.

**Tech stack:** FastAPI, Google Gemini (Pro + Flash), SQLite + SQLAlchemy, HTML/CSS + Jinja2, Uvicorn

## Features
- Personalized 7-day workout plan (Gemini Pro)
- Nutrition / recovery tip (Gemini Flash)
- Feedback-based plan update (original and updated plans both stored)
- Admin dashboard at `/view-all-users`

## Project Structure
```
FitBuddy/
├── app/
│   ├── main.py                    # FastAPI app entry point
│   ├── routes.py                  # All routes
│   ├── database.py                # SQLite + SQLAlchemy
│   ├── schemas.py                 # Pydantic models
│   ├── config.py                  # API key / model config
│   ├── gemini_generator.py        # Workout plan (Gemini Pro)
│   ├── gemini_flash_generator.py  # Nutrition tip (Gemini Flash)
│   └── updated_plan.py            # Feedback-based update
├── templates/  (index.html, result.html, all_users.html)
├── static/images/                 # Put gym.jpg here (optional background)
├── requirements.txt
└── .env.example
```

## Setup
```bash
python -m venv fitbuddy-env
fitbuddy-env\Scripts\activate          # Windows   (Linux/Mac: source fitbuddy-env/bin/activate)
pip install -r requirements.txt
copy .env.example .env                 # Linux/Mac: cp .env.example .env
```
Open `.env` and paste your Gemini API key (free from https://aistudio.google.com/apikey).

## Run
```bash
uvicorn app.main:app --reload
```
- App: http://127.0.0.1:8000
- API docs: http://127.0.0.1:8000/docs

## Routes
| Route | Method | Purpose |
|---|---|---|
| `/` | GET | Input form |
| `/generate-workout` | POST | Generate plan + tip, save to DB |
| `/submit-feedback` | POST | Update plan using feedback |
| `/view-all-users` | GET | Admin dashboard |
