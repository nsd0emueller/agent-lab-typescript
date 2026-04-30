# Repo Instructions

## Mandatory checklist
- [ ] `npm run lint`
- [ ] `npm run build`
- [ ] `npm run test`

## Scope
- Prefer app work in `src/`, plus related config in `vite.config.ts`, `eslint.config.js`, and `.github/workflows/deploy.yml`.
- `workshop/` is excluded by `.copilotignore`; do not edit workshop content unless the user explicitly asks.
- This repo already has scoped instructions for frontend design and Tailwind v4 in `.github/instructions/`.

## Stack
- Vite + React 19 + TypeScript
- Tailwind CSS v4 via `@tailwindcss/vite`
- Vitest + Testing Library with `jsdom`
- Node.js 22 / npm

## Architecture map
- `src/App.tsx` switches between `StartScreen`, `GameScreen`, and `BingoModal` based on game state.
- `src/hooks/useBingoGame.ts` is the main state layer: board generation, square toggling, bingo detection, modal visibility, reset flow, and `localStorage` persistence.
- `src/utils/bingoLogic.ts` contains pure game rules/helpers: `generateBoard`, `toggleSquare`, `checkBingo`, `getWinningSquareIds`.
- `src/types/index.ts` defines domain types such as `BingoSquareData`, `BingoLine`, and `GameState`.
- `src/data/questions.ts` is the source of bingo prompt content.

## Working conventions
- Keep rendering concerns in components, pure rules in `src/utils/`, and state/persistence in `src/hooks/useBingoGame.ts`.
- Reuse shared types from `src/types/index.ts`; avoid redefining domain shapes inline.
- Preserve the 5x5 board and center free-space behavior unless the task explicitly changes game rules.
- If changing persisted state in `useBingoGame`, update validation/versioning logic together.
- Keep changes minimal and consistent with the existing semicolon-based TypeScript style.

## Testing guidance
- Prefer adding or updating tests in `src/utils/bingoLogic.test.ts` when game rules change.
- Test pure logic first; add component tests only when behavior depends on rendering or interaction.
- Keep tests compatible with `src/test/setup.ts` and the `jsdom` Vitest setup in `vite.config.ts`.

## Deployment notes
- `vite.config.ts` sets `base` from `VITE_REPO_NAME`; avoid hardcoded root-relative asset paths.
- GitHub Pages deploys docs at the site root and the built app under `/game/` via `.github/workflows/deploy.yml`.

