# Management Assistant

A Socratic tutoring web app for undergraduate business students studying Principles of Management. Built on the [OpenStax Principles of Management](https://openstax.org/details/books/principles-management) textbook (Rice University, CC BY 4.0).

## Overview

Management Assistant guides students through management concepts using the Socratic method — asking questions and prompting critical thinking rather than providing direct answers. Students select a textbook chapter, and the app uses that content as context to support focused, chapter-relevant tutoring.

### Features

- **Chapter-based context**: Students select from 18 chapters; only the relevant chapter is sent as context to keep responses focused and API calls efficient.
- **Socratic tutoring**: The assistant asks guiding questions rather than giving direct answers, encouraging self-directed learning.
- **Study tools**: Study guides, practice quizzes, concept comparisons, business case scenarios, and ethics scenarios.
- **File attachment**: Students can attach drafts or documents for guided feedback.
- **Mobile-friendly**: Responsive design that works on phones, tablets, and desktops.

### What the assistant will do

- Ask guiding questions to help students reason through concepts
- Create study guides, practice quizzes, and concept maps
- Generate realistic business scenarios and case studies
- Prompt students to consider ethical dimensions of management decisions
- Provide feedback on drafts by asking clarifying questions

### What the assistant will not do

- Give direct textbook answers
- Complete assignments, papers, quizzes, or exams
- Discuss or calculate grades
- Generate inappropriate content

## Architecture

The app consists of three parts:

1. **`index.html`** — Single-page frontend (HTML/CSS/JS)
2. **`chapters.js`** — Textbook content for all 18 chapters, loaded as JavaScript
3. **Cloudflare Worker** — API proxy that forwards requests to the Anthropic Claude API

```
Student's Browser          Cloudflare Worker          Anthropic API
┌──────────────┐          ┌─────────────────┐        ┌─────────────┐
│  index.html  │──POST───▶│  worker.js      │──POST─▶│  Claude API │
│  chapters.js │◀─JSON────│  (adds API key) │◀─JSON──│             │
└──────────────┘          └─────────────────┘        └─────────────┘
```

## Textbook

This app is based on [Principles of Management](https://openstax.org/details/books/principles-management) by OpenStax (Rice University), licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

## Model

The app uses Anthropic's Claude (`claude-sonnet-4-20250514` by default). You can change the model in the `sendMessage()` function in `index.html`.
