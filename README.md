Teach stack:
Frontend:  React (JavaScript)
Backend:   Python + FastAPI
Database:  PostgreSQL (via Supabase — free)
AI:        OpenAI API (GPT-4o Vision)
Hosting:   Render (free tier for backend), Vercel (free for frontend)


Conversation:
[User's Browser]
      ↓  HTTP requests (fetch/axios)
[React Frontend]
      ↓  REST API calls (JSON)
[FastAPI Backend]
      ↓                    ↓
[PostgreSQL DB]     [OpenAI API]
(stores clothes,    (tags images,
 users, outfits)     suggests outfits)


 Example:
 1. React sends the image file to:
   POST /api/clothes/upload

2. FastAPI receives it, saves the image to storage,
   then sends it to OpenAI Vision API:
   "What type of clothing is this? Return color,
    type, material, and style as JSON."

3. OpenAI returns:
   { "type": "shirt", "color": "navy blue",
     "material": "linen", "style": "casual" }

4. FastAPI saves that JSON to PostgreSQL
   in your clothes table.

5. FastAPI returns success to React.

6. React shows the tagged item in the user's closet.


