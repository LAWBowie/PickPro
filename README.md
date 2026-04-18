# PickPro MVP

High-fidelity prototype for a white-label fantasy player-props product aimed at sportsbook operators and investors.

## What is included

- Next.js app-router structure with a dark sportsbook-style UI
- Football and Rugby match lobby with player prop cards
- 2-5 leg slip builder with multiplier and payout logic
- Simulated wallet, placed slips, and settlement engine
- Player detail modal with last-5 trend chart
- Leaderboard and operator dashboard with line editing
- LocalStorage persistence for repeat demos
- Plugin-ready embed mode with operator theming and host page messaging hooks

## Run locally

1. Install Node.js 20+
2. Install dependencies:

```bash
npm install
```

3. Start the app:

```bash
npm run dev
```

4. Open `http://localhost:3000`

## GitHub V1 flow

If you want this to live as a simple `V1` snapshot on GitHub, you can do both source control and free hosting from the same repo.

### 1. Create the repo and push `V1`

```bash
git init
git add .
git commit -m "PickPro V1"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/pickpro-v1.git
git push -u origin main
```

### 2. Turn on GitHub Pages

This repo is configured to export as a static Next.js site and deploy through GitHub Actions.

In GitHub:

1. Open `Settings`
2. Open `Pages`
3. Under `Build and deployment`, set `Source` to `GitHub Actions`
4. Push to `main` again if needed, or run the `Deploy GitHub Pages` workflow manually

Your demo URL will be:

```text
https://YOUR-USERNAME.github.io/pickpro-v1/
```

If you use a different repo name, the URL path changes to match that repo.

### 3. Make later versions

When you want a new branch of the product:

- keep this repo as `V1`
- clone it into a new repo such as `pickpro-v2`
- make changes there without disturbing the live `V1` demo

## Embed mode

You can run the app in white-label embed mode by passing query params:

```bash
http://localhost:3000/?embed=1&operator=hollywoodbets
```

Supported operator presets:

- `default`
- `demo`
- `hollywoodbets`

## Host integration API

The embedded app posts state updates to the parent window using `postMessage`:

```ts
{
  type: "pickpro:state",
  embedded: true,
  operator: "hollywoodbets",
  wallet,
  slips,
  metrics
}
```

The host can control parts of the experience by posting messages into the iframe:

```ts
{ type: "pickpro:set-balance", balance: 2500 }
{ type: "pickpro:set-sport", sport: "Football" }
{ type: "pickpro:set-operator", operator: "demo" }
```

## Notes

- This is intentionally demo-first and uses mock data plus client-side state.
- Match data, settlement results, and wallet state are seeded for operator demos.
- The operator tab lets you tweak lines and add placeholder matches without a backend.
