# A Decade of Us — Vue starter

A simple responsive anniversary website for Vishnu (Bujji), built with Vue 3 and Vite.

## Run locally

```bash
npm install
npm run dev
```

## Personalize

- Edit `src/content.js` for names, messages, memories, and letter.
- Put pictures in `public/photos/`. Set `heroPhoto` and each memory's `photo` to `/photos/your-file.jpg`.
- Edit colors and layout in `src/style.css`.
- Edit sections in `src/App.vue`.
- Run `npm run build` to produce the static website in `dist/`.

Photos are intentionally placeholders. The letter includes starter text for you to replace. No accounts, database, or tracking are included.

## Edit the relationship quiz

The `quiz` array in `src/content.js` controls every question. Three starter questions use the nickname and anniversary details supplied for this site. Replace them or add your own:

```js
{
  question: 'Where did we go on our first date?',
  options: ['Cafe', 'Cinema', 'Park', 'Restaurant'],
  answer: 0, // zero-based: 0 = Cafe, 1 = Cinema, 2 = Park, 3 = Restaurant
  note: 'Add a little message about this memory.'
}
```

Each question needs at least two options and a valid `answer` index. The quiz shows feedback, the correct answer, progress, a final score, and a Play again button. Answers lock after selection to prevent double scoring. There is no timer, backend, or score storage; refreshing starts over. Quiz answers are included in the browser code, so this is a playful personal quiz rather than a secure exam.

The reusable quiz component is `src/components/LoveQuiz.vue`. Remove every item from `quiz` to hide the quiz section.
