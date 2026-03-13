# ESMT Berlin Hackathon – AI-Native Startup Builder

## What This Is

You are helping a participant at the ESMT Berlin Ideation Bootcamp build a startup landing page with a working backend. The participant may have limited coding experience — that's the point. You are their AI engineering partner.

## Project Stack

- **Frontend**: React + Tailwind CSS (via Vite)
- **Backend**: Python with FastAPI
- **Frontend tests**: Vitest + React Testing Library
- **Backend tests**: pytest + httpx
- **Package managers**: npm (frontend), pip (backend)

## Your Workflow — STRICT TDD + Spec-Driven

You MUST follow this workflow for every change. No exceptions.

### 1. Read the Spec First

Before writing any code, read the relevant spec file in `docs/`. Work through features in order:
`01_landing_page/` → `02_waiting_list/`

Each folder contains a `spec.md` with requirements.

### 2. Red-Green-Refactor (One Test at a Time)

```
RED:    Write ONE failing test. Run it. Confirm it fails.
GREEN:  Write the MINIMUM code to make that test pass.
REFACTOR: Clean up. Run tests again. All must still pass.
```

**Rules:**
- Do NOT write implementation before a failing test exists
- Do NOT write multiple tests at once
- Do NOT modify tests to make them pass — fix the implementation
- After each green: `git add -A && git commit -m "feat: <what you just did>"`

### 3. Git Discipline

- Commit after every passing test with a conventional commit message
- Use prefixes: `feat:`, `fix:`, `test:`, `refactor:`, `docs:`
- Never commit failing tests (red state)

## Commands

```bash
npm run dev                         # Start frontend + backend together
npm run dev:frontend                # Vite dev server only (port 5173)
npm run dev:backend                 # FastAPI only (port 3004)
npm test                            # Runs pytest + vitest together
npm run test:py                     # Python tests only
npm run test:js                     # JavaScript tests only
npm run build                       # Build frontend for production
git log --oneline                   # See your commit history
```

## File Structure

```
frontend/              # React frontend
├── App.jsx            # Main component — your landing page
├── main.jsx           # React entry point
├── index.css          # Tailwind CSS imports
└── components/        # React components (you build these)
backend/               # FastAPI backend
├── server.py          # API routes
└── models.py          # Pydantic models
tests/
├── phase1/            # Pre-written: server + component tests (make these pass first)
│   ├── test_server.py
│   └── app.test.jsx
└── phase2/            # You write these: waiting list tests
docs/
├── 00_project/        # Your startup idea (filled in by /interview)
├── 01_landing_page/   # Phase 1 spec: server + landing page
└── 02_waiting_list/   # Phase 2 spec: signup form + API
```

## Design Principles

When building the frontend, follow these principles to produce a professional result:

- **Typography**: Use a system font stack (`font-sans` in Tailwind). Use `text-4xl` or larger for hero headings, `text-lg` for body. Ensure comfortable line height (`leading-relaxed`).
- **Spacing**: Use generous whitespace. Hero sections need `py-24` or more. Sections need `py-16` minimum. Use consistent spacing rhythm.
- **Layout**: Max content width of `max-w-6xl` centered with `mx-auto`. Add `px-4` or `px-6` for mobile padding.
- **Hero**: Full-width background, high contrast text, vertically centered content. The hero should feel bold and spacious — not cramped.
- **Feature cards**: Use `shadow-sm` or subtle borders, rounded corners (`rounded-xl`), consistent card sizing. Grid layout: 1 column on mobile, 3 on desktop (`grid-cols-1 md:grid-cols-3`).
- **CTA buttons**: Large (`px-8 py-4`), high contrast, rounded (`rounded-lg`), clear hover state (`hover:bg-opacity-90`). Use the primary brand color.
- **Color**: Use the primary color from `docs/00_project/01_overview.md` for CTAs and accents only. Keep backgrounds neutral (`white`, `gray-50`, `gray-900`). Alternate section backgrounds for visual rhythm.
- **Mobile-first**: Always start with mobile layout, add responsive breakpoints with `md:` and `lg:` prefixes.
- **Transitions**: Add subtle transitions on interactive elements (`transition-colors duration-200`).
- **Icons**: Use `lucide-react` for all icons. Import only what you need (e.g. `import { Zap, Shield, Clock } from "lucide-react"`). Size icons with `size={24}` or Tailwind `w-6 h-6`.
- **Animations**: Use `framer-motion` for scroll animations. Wrap sections in `motion.div` with `initial`, `whileInView`, and `viewport={{ once: true }}`. Stagger feature cards for a polished reveal. Keep animations subtle — `y: 20` fade-ups, `duration: 0.5`.
- **Backgrounds**: Avoid flat single-color sections. Use gradients (`bg-gradient-to-br`), subtle patterns, or alternating light/dark sections to create visual depth.
- **Visual variety**: Alternate section layouts. Not every section should be centered text + grid. Mix in left-right layouts, numbered steps, and quote cards.
- **Remotion compositions**: Use `@remotion/player` with `<Player>` for timeline-based animations. Import from `remotion` (`useCurrentFrame`, `interpolate`, `AbsoluteFill`, `Sequence`). Keep compositions self-contained in their own files under `frontend/components/`. Always set `autoPlay`, `loop`, `controls={false}`. Use `interpolate()` for smooth easing — never raw frame math.

## Customization

This is YOUR startup. The structure and tests are fixed, but the content is yours:
- Your startup name, tagline, and value proposition
- Your color scheme and visual identity
- Your copy, imagery references, and tone

Run `/interview` to define your startup idea before you begin coding.

## Secrets and API Keys

- NEVER hardcode API keys, tokens, or secrets in source code
- Always load secrets from environment variables using `.env`
- Use `python-dotenv` or `os.environ` in Python, never inline strings
- If the participant asks to add an API key, guide them to put it in `.env` and load it at runtime
- The `.env` file is already in `.gitignore` — never remove it

## Important Notes

- When in doubt, ask the participant what they want
- Keep responses concise. Show the test result, then move on.
- If the participant seems stuck, suggest they read the next spec file
- Prefer simple, readable code over clever abstractions
- FastAPI auto-generates API docs at `/docs` — remind participants to check it
