# DentiBloom AI
*Your dental school, one intelligent workspace.*

A Flutter (Android/iOS) study app for dentistry students with a FastAPI backend and Supabase (Postgres, auth, private storage).

> **Read `docs/STATUS.md` first.** It lists exactly what is implemented, what only works in demo mode, what needs API keys, and what is NOT built yet. This is a foundation plus several working workflows, not a finished product.

## What works today (see STATUS.md for detail)
**Mobile app, no accounts or keys needed (Demo / local mode, data stored on the device):**
onboarding, light/dark theme (saved), bottom navigation, Home dashboard from saved data, Library with search (including transcript text), Lecture Studio (import a `.txt` transcript with optional `[mm:ss]` timestamps, transcript search, edit, bookmarks, notes, flashcard-from-passage), Reviewer editor (add/edit/reorder/delete/duplicate), Flashcards with spaced repetition, Quizzes built from your own decks, Journal (with a patient-identifier privacy reminder), Study Planner, Progress, Casebook (separate, privacy-first, "Not provided" placeholders, no AI), Ask Bloom (local passage search with citations; says so when nothing matches).

**Backend (needs Supabase; AI parts need keys):** versioned `/api/v1` API with JWT verification, ownership-safe CRUD, signed private uploads, long-lecture transcription pipeline (ffmpeg segmentation, overlap-safe merge, resumable retries), grounded "ask the lecture", deterministic case drafts, PDF export, SQL migration with Row Level Security on every table.

**Needs external credentials:** real transcription (STT provider key), AI answers/summaries/reviewer generation (LLM key), sign-in (Supabase project).

## Quick start (Windows 11)
1. Install: [Flutter SDK](https://docs.flutter.dev/get-started/install/windows) (3.27 or newer), Android Studio (for the emulator), [Python 3.11+](https://www.python.org/downloads/), [FFmpeg](https://ffmpeg.org/download.html) (add to PATH), Git.
2. Try the app in Demo mode (no backend):
   ```powershell
   cd mobile
   flutter create . --platforms=android,ios   # generates android/ and ios/ folders (one time)
   flutter pub get
   flutter run
   ```
   On the last onboarding page tap **Explore in Demo mode**.
3. Run the backend tests (no keys needed):
   ```powershell
   cd backend
   python -m unittest discover -s tests -v
   ```
4. Full setup with Supabase and the API: `docs/SETUP_GUIDE.md`.

## Folder map
`mobile/` Flutter app · `backend/` FastAPI + worker logic + tests · `supabase/migrations/` database + RLS · `docs/` guides · `scripts/` helpers.

## Safety notes
- Demo content is always labeled DEMO and is fictional. Simulated output is never presented as coming from your recordings.
- Never put real patient data in the app until your school's approval, privacy, consent and security checks are done (`docs/PRIVACY_AND_SECURITY.md`).
- Not a medical device; it does not replace clinical supervision. Transcription can misrecognize dental terms, accents, and mixed English/Filipino speech. No legal compliance (DPA, HIPAA, GDPR) is claimed.
