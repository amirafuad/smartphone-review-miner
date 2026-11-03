# Smartphone Review Miner

A web app that reads smartphone customer reviews (Indonesian or English) and tells you whether each review is positive, negative or mixed, and which phone features people are happy or unhappy about.

It is a modern, interactive rebuild of my undergraduate thesis, *User Review and Mining Application for Smartphone Products*, which used the Naïve Bayes algorithm for review classification.

**Live demo:** _add your GitHub Pages / Vercel / Netlify link here_

## Features

- Classifies every review as positive, negative, mixed or unclear, with a probability score
- Detects phone features (battery, camera, screen, performance, price, design, audio, delivery and service) and shows the positive/negative split for each
- Highlights the words that influenced the result, so the model's decision is visible
- Handles negation in both languages ("tidak bagus", "not good", "no lag")
- Results update as you type; everything runs in the browser, no server and no data leaves the page
- Responsive layout with light and dark mode

## How it works

1. **Tokenising.** Lowercase, remove filler words, and let a negation word flip the next two words.
2. **Naïve Bayes.** `P(class | words) ∝ P(class) × ∏ P(word | class)` with add-one (Laplace) smoothing, trained on ~100 short labelled reviews at page load.
3. **Feature-level sentiment.** Reviews are split into clauses (commas, "tapi", "but", "and"). A clause that mentions a feature is classified on its own.

The classifier is written from scratch in plain JavaScript (no ML library).

## Tech

React 18 (loaded from a CDN), htm for JSX-like templates, plain CSS with light/dark theme tokens. Single `index.html`, no build step.

## Run it

Open `index.html` in a browser. To publish it free: push this folder to a GitHub repository, then enable **Settings → Pages → Deploy from branch**.

## Limitations and next steps

- The training set is small, so slang, sarcasm and rare words are often misread
- Ideas: let users correct a label and retrain, import reviews from CSV, add a chart of sentiment over time, migrate to Next.js with TypeScript
