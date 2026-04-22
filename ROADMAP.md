# 👗 Wardrobe AI — Project Roadmap

> A personal AI-powered outfit assistant that learns your wardrobe and suggests matching outfits based on your style, body type, and the occasion.

**Builder:** Solo CS student, second year  
**Time budget:** ~2–4 hours/week  
**Goal:** Portfolio project + genuine learning in full-stack development and AI

---

## 🏗️ Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Frontend | React (JavaScript) | Industry standard, huge job market |
| Backend | Python + FastAPI | Clean, fast, great for AI work |
| Database | PostgreSQL via Supabase | Free tier, real production database |
| AI | OpenAI API (GPT-4o Vision) | No model training needed at first |
| Frontend hosting | Vercel | Free, deploys from GitHub automatically |
| Backend hosting | Render | Free tier, easy Python deployment |

---

## 🔌 How The Parts Talk To Each Other

The user's browser never talks directly to the database or to OpenAI.  
**Everything goes through the backend.** This keeps API keys secret and gives you full control.

```
[User's Browser]
      │
      │  HTTP requests (JSON)
      ▼
[React Frontend]          ← What the user sees and clicks
      │
      │  REST API calls
      ▼
[FastAPI Backend]         ← Your Python server, the "brain"
      │              │
      ▼              ▼
[PostgreSQL]     [OpenAI API]
(stores clothes,  (reads images,
 users, outfits)   suggests outfits)
```

### Example: Uploading a shirt

```
1. User picks a photo in React
2. React sends it to:  POST /api/clothes/upload
3. FastAPI saves the image to Supabase Storage
4. FastAPI sends the image to OpenAI Vision:
   "What is this clothing item? Return color, type,
    material, and style as JSON."
5. OpenAI returns:
   { "type": "shirt", "color": "navy", "style": "casual" }
6. FastAPI saves that to PostgreSQL
7. FastAPI tells React: "success"
8. React shows the new item in the closet
```

Every feature follows this same pattern. Learn it once, apply it everywhere.

---

## 📋 Version Plan

Each version is a shippable, working product — not just a step toward one.  
**Rule: Deploy and demo each version before starting the next.**

---

### ✅ Version 1 — "It Actually Works"
**Estimated time:** 4–6 weeks at 2–4 hrs/week  
**Difficulty:** ⭐⭐☆☆☆

**What it does:**
- User can add a clothing item (name, color, type) via a form
- Items are saved to a real PostgreSQL database
- Items appear in a list on screen
- User can delete items

**What you learn:**
- React: components, state, forms, fetch
- FastAPI: creating endpoints, receiving data
- PostgreSQL: tables, INSERT, SELECT, DELETE
- How frontend and backend connect (the most important lesson)

**Definition of done:** A deployed URL where you can add and delete clothes. That's it.

---

### ✅ Version 2 — "Real Photos"
**Estimated time:** 3–4 weeks  
**Difficulty:** ⭐⭐⭐☆☆

**What it does:**
- Upload an actual photo of a clothing item
- Photo is stored in Supabase Storage (free)
- Photo is displayed in the wardrobe view

**What you learn:**
- File uploads in React and FastAPI
- Cloud storage (Supabase buckets)
- Handling binary data (images) in an API

**Definition of done:** Upload a photo, see it appear on screen, stored in the cloud.

---

### ✅ Version 3 — "AI Reads The Photo"
**Estimated time:** 3–4 weeks  
**Difficulty:** ⭐⭐⭐☆☆

**What it does:**
- On upload, GPT-4o Vision automatically tags the item
- Tags include: color, clothing type, material, style
- User can correct any wrong tags

**What you learn:**
- Calling AI APIs from your backend
- Prompt engineering (how you phrase questions to AI matters a lot)
- Parsing and validating JSON responses from AI

**Definition of done:** Upload a photo, AI correctly identifies it. No manual typing needed.

> 💡 This is your first real AI feature. Screenshot everything for your portfolio.

---

### ✅ Version 4 — "It Knows You"
**Estimated time:** 2–3 weeks  
**Difficulty:** ⭐⭐☆☆☆

**What it does:**
- Simple profile form: height, body type, skin tone, preferred style
- Profile is saved to the database linked to the user
- No AI here — just a form

**What you learn:**
- Relational database design (linking tables together)
- User data modeling
- More complex FastAPI data structures

**Definition of done:** Fill in a profile, it saves, it loads back correctly.

---

### 🌟 Version 5 — "Suggest Me An Outfit"
**Estimated time:** 4–5 weeks  
**Difficulty:** ⭐⭐⭐⭐☆

**What it does:**
- Button: "Suggest me an outfit"
- Backend sends your wardrobe tags + your profile to GPT-4
- GPT-4 returns a specific outfit combination from your actual clothes
- App highlights those items in your closet

**What you learn:**
- Advanced prompt engineering (combining multiple data sources)
- Context management (sending the right data to the AI)
- Translating AI text output back into UI interactions

**Definition of done:** Click a button, get a real outfit suggestion using your actual clothes.

> 🎯 **This is your portfolio milestone.** This is what you demo to recruiters.  
> Everything after this is a bonus.

---

### Version 6 — "What's The Occasion?"
**Estimated time:** 2–3 weeks  
**Difficulty:** ⭐⭐⭐☆☆

**What it does:**
- Dropdown before generating: Casual / Work / Formal / Sport / Date Night
- AI suggestion adjusts to the occasion

**What you learn:**
- Dynamic prompt construction
- User intent handling
- Iterating on an existing feature (more realistic than building from scratch)

---

### Version 7 — "Multiple Users"
**Estimated time:** 4–6 weeks  
**Difficulty:** ⭐⭐⭐⭐☆

**What it does:**
- Sign up and log in with email + password
- Each user only sees their own wardrobe
- Secure sessions with JWT tokens

**What you learn:**
- Authentication and authorization
- Security fundamentals
- One of the most common junior dev interview topics

> ⚠️ This version touches every layer of the app. Take it slow.

---

### Version 8 — "What's The Weather?"
**Estimated time:** 2 weeks  
**Difficulty:** ⭐⭐☆☆☆

**What it does:**
- Calls the free Open-Meteo weather API using the user's city
- Weather context is included in the outfit prompt
- "It's 3°C and raining — here's what to wear"

**What you learn:**
- Third-party API integration
- Chaining multiple data sources into one AI prompt

---

### Version 9 — "Outfit History"
**Estimated time:** 3 weeks  
**Difficulty:** ⭐⭐⭐☆☆

**What it does:**
- Save outfit suggestions you liked
- Mark outfits as favorites
- Option: "Don't suggest things I wore this week"

**What you learn:**
- More complex database queries
- Application state that evolves over time

---

### Version 10 — "Your Own AI Model"
**Estimated time:** 2–3 months  
**Difficulty:** ⭐⭐⭐⭐⭐

**What it does:**
- Replaces GPT API calls with a fine-tuned model you trained yourself
- Model understands fashion matching specifically
- Runs for free (no API costs)

**How to train it cheaply:**

```
Step 1: Get data
  → Download a fashion dataset from Hugging Face
  → Search: "fashion compatibility dataset" or "Polyvore dataset"

Step 2: Format training pairs
  Input:  "navy slim chinos + white oxford shirt + brown loafers"
  Output: "good match — smart casual, works for work or dinner"

Step 3: Fine-tune a small open model (FREE)
  → Use Google Colab (free GPU access)
  → Model: Meta Llama 3 (8B) or Mistral 7B
  → Library: Unsloth (makes fine-tuning fast and cheap)
  → Cost: $0 on free Colab, ~$5–10 on Colab Pro if needed

Step 4: Deploy
  → Test in Colab
  → Host on Hugging Face Spaces (free)
  → Point your backend at it instead of OpenAI
```

**What you learn:**
- The complete ML pipeline: data → training → evaluation → deployment
- Fine-tuning vs. training from scratch
- Open source AI models and the Hugging Face ecosystem

> 🏆 This is what separates your portfolio from everyone else's.

---

## 📚 Free Learning Resources

Work through these in order as you reach each version:

| Topic | Resource | When to use it |
|---|---|---|
| React basics | [react.dev](https://react.dev) official tutorial | Before Version 1 |
| Python + FastAPI | [fastapi.tiangolo.com](https://fastapi.tiangolo.com) docs | Before Version 1 |
| PostgreSQL | [postgresqltutorial.com](https://www.postgresqltutorial.com) | Before Version 1 |
| Connecting frontend + backend | Search "FastAPI React tutorial" on YouTube | Before Version 1 |
| AI APIs | [OpenAI Cookbook](https://github.com/openai/openai-cookbook) on GitHub | Before Version 3 |
| Prompt engineering | [learnprompting.org](https://learnprompting.org) | Before Version 3 |
| Authentication | Search "FastAPI JWT auth tutorial" | Before Version 7 |
| Fine-tuning AI models | [Hugging Face courses](https://huggingface.co/learn) | Before Version 10 |
| Unsloth fine-tuning | [Unsloth GitHub](https://github.com/unslothai/unsloth) | Before Version 10 |

---

## 🚀 Where To Start (Week 1)

```
Day 1 (1 hour):
  [ ] Install Node.js, Python 3.11+, VS Code
  [ ] Create a GitHub repo called "wardrobe-ai"
  [ ] Create a Supabase account, make a free project

Day 2 (1 hour):
  [ ] Follow the React official tutorial (react.dev)
  [ ] Get "Hello World" rendering in your browser

Day 3 (1 hour):
  [ ] Follow FastAPI "first steps" tutorial
  [ ] Get a Python server running locally

Day 4 (1 hour):
  [ ] Connect React to FastAPI with one button
  [ ] Button clicks → React asks FastAPI → FastAPI says "Hello"
  [ ] This single working connection is your foundation
```

> When React and FastAPI talk to each other for the first time, everything clicks.  
> Every feature you ever build is just a more complex version of that same connection.

---

## 📌 Rules To Keep Yourself On Track

1. **Deploy every version** before starting the next one. A live URL is proof of work.
2. **Scope is everything.** When in doubt, do less. A finished small thing beats an unfinished big thing.
3. **Don't skip Version 1** to get to the "cool AI stuff." The boring foundation is what makes everything else work.
4. **Commit to GitHub regularly.** Even broken code. The commit history tells a story to recruiters.
5. **Write a short README update** after each version. Your future self will thank you.

---

*Last updated: April 2026*
