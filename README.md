# Ummah Quiz Bot

A Telegram quiz bot covering Quran, Seerah, Hadith, and general Islamic knowledge.
Works solo or in a group chat — first correct tap wins the point.

## Setup

1. **Get a bot token:** message [@BotFather](https://t.me/BotFather) on Telegram,
   run `/newbot`, and copy the token it gives you.
2. **Install dependencies:**
   ```bash
   npm install
   ```
3. **Configure environment:** copy `.env.example` to `.env` and fill in:
   - `BOT_TOKEN` — from BotFather
   - `DATABASE_URL` — a Postgres connection string (e.g. from Supabase)
4. **Set up the database:**
   ```bash
   npx prisma migrate dev --name init
   ```
5. **Run the bot:**
   ```bash
   npm start
   ```

## Commands

- `/play` — pick a category and start a 5-question quiz
- `/learn` — get a random fact/question to study, with the answer shown
- `/leaderboard` — top 10 players by total points
- `/privacy` — toggle whether your username shows on the leaderboard (defaults to on)

## Extending it

- **More questions:** just add entries to `src/questions.js` — no code changes needed.
- **Dua Wall:** add a `DuaPost` model to `prisma/schema.prisma` (text, telegramId, ameenCount)
  and commands `/dua <text>` to post anonymously + an inline "🤲 Ameen" button that increments a counter.
- **Global hadith relay:** add a `RelayState` model tracking the current hadith, which country/user
  holds it, and a `/pass` command that rotates it — post progress with a simple text-based world map
  or a Visualizer widget in the companion web app.
- **Weekly leaderboard post:** add `node-cron` and a scheduled job that calls the same query used in
  `/leaderboard` and posts it to your main group automatically.
- **Real-time multiplayer lobby:** currently anyone in the chat can answer at once (fast and simple).
  For strict turn-based play, track a `turnOrder` array in the session and only accept answers from
  the current player.
