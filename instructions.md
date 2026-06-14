# DormBattles

An online and offline gaming league for campus squads


## Context

DormBattles is being built for the Fenrir project at Ethara AI as an intern level prototype that proves the core product experience before any real engineering investment. The audience is students who form squads and battle online and offline, plus organizers who record offline lab and classroom results. This milestone is a web based prototype only. It is not a finished platform, not a real game engine, and not a real time multiplayer service. The deployment target is a local machine running the project in a modern desktop browser, and everything runs with no paid service.

## Project description

DormBattles is a browser based gaming league for college and school students. Players sign in, form or join squads, browse supported games, start online sessions, chat with their squad, and climb shared leaderboards. Organizers record offline results with a match report form, and both online and offline results feed the same points system. Each month is a season with a theme, a prize pool, and an automatic reset, so the competition stays fresh. The same product serves a quick online room and a campus lab final without feeling complicated, which keeps it approachable for new players while still rewarding the most active squads.

## 1. Background and why

Campus gaming is usually scattered across chat groups, spreadsheets, and separate lab events. Online matches and offline matches never meet in one place, so there is no shared sense of who is winning the campus. DormBattles brings both into one league. A lab final and an online room count toward the same leaderboard, squads give students a team to play for, and the monthly season keeps the competition fresh. This milestone proves that core experience before any real engineering investment.

## 2. Goals

1. A browse home that lists supported games as store style cards a player can scan quickly.
2. A squad system where a player can create a squad, join a squad, and see squad members.
3. One matches model that stores online results and offline results together.
4. Two leaderboards that actually update, one for players and one for squads.
5. A monthly season model with a theme, a prize pool, and an automatic reset.
6. A simple text chat for squad channels and event channels.
7. Runs on a laptop with one command, no paid hosting, and no online account.

## 3. Live and locally runnable

1. Opens with a single command on a regular laptop.
2. Runs in the latest stable desktop Chrome or Firefox, or as a small local server the README spells out.
3. No paid services, no signup, and no API key the reviewer has to register for.
4. All assets and data sit inside the project folder, with no outside service that could go down.
5. The reviewer can sign in, form a squad, record results, and read the leaderboards in real time.

## 4. Functional requirements

| ID | Area | Requirement |
|---|---|---|
| F1 | Auth | Mock sign in reads accounts from the users data set and supports the player, organizer, and reviewer roles. |
| F2 | Squads | A player can create a squad with a squad name and become the captain. |
| F3 | Squads | A player can join an existing squad from a squad listing. |
| F4 | Squads | A squad details view shows the captain, the members, and the squad total points. |
| F5 | Games | The games page lists every supported game with title, genre, recommended player count, and a casual or ranked tag. |
| F6 | Sessions | A player can start an online session through a simple room or match record for a chosen game. |
| F7 | Offline | An organizer records an offline result with a match report form that captures the game, the season, the squads, the players, the result, and the points. |
| F8 | Matches | Online results and offline results are stored in the same matches data set and are marked with a mode of online or offline. |
| F9 | Leaderboards | The app computes a player leaderboard ranked by total points with wins as the tie breaker. |
| F10 | Leaderboards | The app computes a separate squad leaderboard by summing the points of each squad member. |
| F11 | Seasons | The home page shows the active season theme and prize pool. |
| F12 | Seasons | At the end of the month the active season resets and a new season becomes active with a fresh prize pool. |
| F13 | Chat | A player can post a text message in a squad channel and in an event channel. |
| F14 | Local first | The project runs locally with one command and no paid service. |

## 5. Editable data list

Important call out. The build ships working with the starter data, but our side must be able to swap games, squads, seasons, and match records later without changing the underlying code, the controls, or the layout.

How this should work in practice.

1. The data lives in editable config files. JSON is the default pick, for example data/games.json, data/squads.json, data/seasons.json, and data/matches.json. CSV is fine if the stack prefers it.
2. Each row follows the field shape in section 7.
3. Replacing a row with a different game, squad, or season updates the app on the next reload, with no code change and no rebuild step.
4. Cover art for swapped games is dropped into the assets folder and referenced by a relative path in the config file.
5. Nothing else moves. The leaderboards, the squad pages, the season banner, and the chat all keep working against whatever data sits in the config files.

Rule of thumb. If our side opens a config file, swaps a row, and reloads the page, the app should show the new value with no other steps.

## 6. Non functional requirements

1. Recommended stack is plain HTML, CSS, and vanilla JavaScript with no build step. React with Vite is an acceptable alternative kept to one install command and one start command.
2. Runs in the latest stable Chrome and Firefox on a regular laptop.
3. Holds up at common desktop sizes from 1280 by 720 and up, with no severe stretching or clipping.
4. Labels are readable and typography is plain and clean.
5. The mock session and the chat may use browser local storage, with no real backend.
6. All asset files and data files sit inside the project folder, with no outside service.

## 7. Data shape

Each data set is a list of plain rows. Field names are suggestions, so pick what fits the stack. Full example rows are documented in assets.pdf.

Game record

| Field | Type | Notes |
|---|---|---|
| game_id | string | Stable id such as G01. |
| title | string | Full game title. |
| genre | string | One word such as Racing or Strategy. |
| recommended_players | integer | Suggested player count. |
| mode_tag | string | One of casual or ranked. |
| play_modes | string | One of online, offline, or online and offline. |
| cover | asset path | Local image used on the game card. |

Match record

| Field | Type | Notes |
|---|---|---|
| match_id | string | Stable id such as M01. |
| game_id | string | References a game. |
| mode | string | One of online or offline. |
| season_id | string | References a season. |
| squad_id | string | References a squad. |
| player_id | string | References a user. |
| result | string | One of win, draw, or loss. |
| points | integer | 3 for a win, 1 for a draw, 0 for a loss. |

Season record

| Field | Type | Notes |
|---|---|---|
| season_id | string | Stable id such as SE01. |
| month | string | Month and year such as June 2026. |
| theme | string | Season theme such as Monsoon Mayhem. |
| prize_pool | string | Short prize description. |
| start_date | string | Year slash month slash day. |
| end_date | string | Year slash month slash day. |
| status | string | One of active or closed. |

## 8. Content and tone

1. Use eight or more supported games so the browse home reads as a real catalog.
2. Match numbers are mock data. The look stays honest by saying so in the methodology note.
3. Cover art is simple placeholder illustration or stylised cards, with no copying of real box art.
4. Squad names and player names are friendly and student themed.
5. Keep the tone energetic and competitive without any aggressive language.

## 9. Acceptance criteria

### Reviewer walkthrough

A reviewer runs the project locally and follows these ordered steps. Each step must work without errors.

1. Start the local server from the README and open the app. The home page loads and shows the active season.
2. Sign in with a sample user and reach the browse home as that role.
3. Create a squad or join one, then open the squad details view.
4. Open the games page and confirm every supported game shows its card fields.
5. Start an online session for a game and see the new match record.
6. Sign in as an organizer, open the match report form, record an offline result, and find it in the matches list.
7. Open Leaderboards and confirm the player leaderboard and the squad leaderboard both reflect online and offline results.
8. Post a message in a squad channel and in an event channel.
9. Move across all pages with no crash and no missing data.

### Acceptance checklist

| ID | Criterion | Check |
|---|---|---|
| A1 | Locally runnable | The README opens the app on a regular laptop with no paid service and no missing key. |
| A2 | Browse home | The home shows supported games as store style cards with a cover and a name. |
| A3 | Squads | A player can create a squad and join a squad, and the squad details view shows members. |
| A4 | Online session | Starting an online session creates a match record. |
| A5 | Offline recording | The organizer match report form records an offline result. |
| A6 | One matches model | Online and offline results sit in the same matches data set with a mode field. |
| A7 | Player leaderboard | Players are ranked by total points with wins as the tie breaker. |
| A8 | Squad leaderboard | Squads are ranked by the sum of their members points. |
| A9 | Season model | The home shows the active season, and the season resets at the end of the month. |
| A10 | Chat | A player can post a message in a squad channel and an event channel. |
| A11 | Usable at desktop sizes | Common widths from 1280 by 720 and up read clean with no broken labels. |
| A12 | Editable data | Editing a config file and reloading shows the new value with no code change. |

## 10. Open questions

1. Is the starter game list fixed, or do we pick the games from a public friendly list?
2. Should chat history persist across reloads, or reset each session?
3. How many past seasons should the seasons page keep visible?
4. Should the build ship as a folder with index.html, a zipped project, or both?

## 11. Out of scope

1. Real multiplayer or real time networking.
2. Real game engines or real game logic.
3. Payments, ads, or in app purchases.
4. A real backend, a database, or cloud saves.
5. Online hosting or domain setup.

## 12. Delivery shape

The built prototype follows this folder shape so a reviewer can open it without hunting.

```
dormbattles/
  index.html
  src/
  assets/
  data/
    games.json
    squads.json
    seasons.json
    matches.json
    users.json
    channels.json
  README.md
```

The submission for this task is the documentation set inside the geetika folder, which holds overview.txt, scope_of_work.txt, assets.pdf, reference_image.png, instructions.md, and rubrics.txt.
