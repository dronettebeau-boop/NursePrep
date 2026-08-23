# NursePrep — $0 Cloudflare + Gemini Free Tier Build

This version removes Render and OpenAI API usage.

## Architecture
- Cloudflare Workers Static Assets hosts the full app.
- `/api/*` runs through the same Cloudflare Worker.
- Gemini's free API tier powers:
  - syllabus analysis
  - syllabus-only free-response problem generation
  - answer checking
  - handwritten-work image analysis
- Each course syllabus and current problem are saved in the user's browser.

## Cost
Cloudflare Workers has a free plan.
Gemini has a free API tier for eligible models/accounts.

This design is intended to run at $0 as long as usage stays within both providers' free-tier limits and the Gemini project remains on the free tier.

## Important privacy tradeoff
Google states that content submitted through the Gemini free tier may be used to improve its products. Do not upload material you are not comfortable sending under the free-tier data terms.

## Deploy
1. Create a free Cloudflare account.
2. Create a free Google AI Studio / Gemini API key. Keep the project on the Free tier; you do not need to enable paid billing just to use the Free tier.
3. Install Node.js on a computer.
4. In this folder run:
   npm install
5. Log into Cloudflare:
   npx wrangler login
6. Save your Gemini key as a Cloudflare secret:
   npx wrangler secret put GEMINI_API_KEY
7. Deploy:
   npm run deploy
8. Cloudflare gives you a `workers.dev` URL.
9. Open that URL in Safari and use Share → Add to Home Screen.

## Current app rules
- Each course has its own page.
- No generic built-in question bank.
- No syllabus = no practice.
- Questions are free response only.
- Work Scanner accepts a photo of handwritten work.
- Current problem and typed response autosave in browser storage.

## Supported syllabus uploads
- PDF
- TXT / Markdown / CSV
- Images of syllabus pages
- Pasted text

For DOCX, export it to PDF or paste the text.
Cloudflare deployment enabled.
