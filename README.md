# PulsePath: AI-Based Public Health Competency Recommender

PulsePath is a responsive React/Vite college project that helps public-health students understand their current competencies, compare them with a target career, and turn the highest-value gaps into a learning roadmap.

## Features

- Guided profile setup with education, interests, career goals, and skill levels
- 20-question competency assessment across six public-health domains
- Dashboard with overall score, progress bars, bar chart, radar chart, strengths, and focus areas
- Career explorer with six public-health career paths and competency requirements
- Transparent, career-aware recommendations based on current score, required level, career relevance, and interest context
- Roadmap builder with priority labels and Not Started, In Progress, and Completed status
- Responsive sidebar workspace layout for desktop and mobile
- Local persistence with `localStorage`, so progress works without a backend or external API

## Technology

- React + Vite
- JavaScript
- Recharts for data visualizations
- Lucide React for icons
- Responsive CSS with a Tailwind-compatible project configuration
- Browser `localStorage` for sample-data persistence

## Installation

Requirements: Node.js 18+ and npm.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite. To make a production build:

```bash
npm run build
npm run preview
```

## Recommended Flow

1. Open **Profile** and save a learner profile.
2. Complete the 20-question **Assessment**.
3. Review the resulting **Dashboard** scores.
4. Select a target career in **Career Explorer** or the recommendation page.
5. Add recommended competency gaps to the **Learning Roadmap**.
6. Click roadmap status circles to cycle through Not Started, In Progress, and Completed.

## Recommendation Algorithm

The recommendation engine is deliberately transparent and runs entirely in the browser.

1. Each assessment answer contributes `100` for a correct answer and `0` for an incorrect answer within its competency. The competency score is the average of those answers.
2. Scores are labelled Beginner (`0–39`), Intermediate (`40–69`), or Advanced (`70–100`).
3. Each career defines a required score for the competencies most relevant to that role.
4. For every required competency, the gap is calculated as:

	`gap = max(0, required competency score - current competency score)`

5. Recommendations are sorted by the largest positive gap. Career requirements provide the relevance weighting, and the selected profile career/interests provide the user context used to explain the recommendation.
6. Priority is assigned as High for gaps of 35 points or more, Medium for gaps of 18–34 points, and Low for smaller positive gaps.

The app ships with sample baseline data so every screen is useful immediately. Saving a profile and completing the assessment replaces the sample values with the learner's local results.