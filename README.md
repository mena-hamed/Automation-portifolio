# Menna — AI Automation Portfolio

A custom Vue 3 + Vite portfolio for an AI Automation Specialist using n8n.

## Run locally
1. Install Node.js (LTS).
2. Extract the folder and open a terminal in it.
3. Run `npm install`
4. Run `npm run dev`
5. Open the local URL printed by Vite.

## Customize before publishing
- **Portrait:** add `public/images/menna-portrait.jpg` (896 × 1195 px recommended).
- **About / quote:** edit the About section in `src/App.vue`.
- **Experience, education, certificates:** replace the clearly marked placeholder entries in the Experience section.
- **Skills and services:** edit `skillGroups` and `services` in `src/App.vue`.
- **Projects:** edit the `projects` array in `src/App.vue`; replace each `link: '#contact'` with the real repository, case study, or demo URL.
- **Project thumbnails:** the cards use custom mini workflow illustrations for now. You can replace the markup inside `.project-thumb` with `<img>` tags pointing to images in `public/images/`.
- **Contact links:** replace `your.email@example.com`, LinkedIn, and GitHub placeholder URLs in `src/App.vue`.
- **Branding:** change the title and meta description in `index.html`.

## Build for deployment
Run `npm run build`; the production site will be generated in `dist/`.
