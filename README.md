# Deep Dive

A quiz where every good answer takes you deeper. Original game; no accounts.

- **Today's descent:** the same 7 questions for everyone on a pack, chosen from the UK date. The pack's questions are dealt out day by day, longest-rested first, so the whole bank comes round before anything repeats.
- **Free dives:** unlimited practice.
- **All packs:** a round that mixes every pack, one question from each in turn.
- **Six kinds of question:** name a rare answer, closest number, bet on it, put in order, a short written answer, and clue by clue (the fewer clues you need, the more it scores).
- **Party:** one screen hosts (a laptop or TV), everyone plays on their own phone with a 4-letter code or the QR. The host's screen keeps the answers, times each question and scores; phones get each question without its answer.
- **Scoreboard:** today's and the deepest-ever dives per pack, with no logins.

## Two pages

- `index.html` is the **live** game. It changes only when a test build is approved.
- `test/index.html` is the **test** page, at the same address with `/test/` on the end. New builds land here first. It shows a "Test version" band, and its scoreboard and party rooms are separate from the live game's.
- Both use the same `lib/` folder.

## How it works

- `index.html` is the whole game: page, engine, scenes and the built-in packs. `lib/` holds MQTT.js (MIT licence), QRCode.js (MIT licence) and KaTeX with its fonts (MIT licence, for maths), shipped beside the page so it works where those websites are blocked.
- Parties and the scoreboard travel through three public MQTT brokers over secure WebSockets (shiftr.io, EMQX, HiveMQ). Every message goes through all three and duplicates are dropped. Scores are kept on the brokers as retained messages, one per pack, player and day.
- **What passes through those public servers:** the names people type, their answers during a party, and their scores. Nothing else. Use first names or nicknames. Anyone who knew the topic names could post a fake score, so treat the board as a family board.

## Hosting on GitHub Pages

1. Create a public repository and upload `index.html`, `README.md` and the `lib` folder.
2. Settings → Pages → deploy from the main branch, root folder.
3. The game is then at `https://<account>.github.io/<repository>/`.

Packs are added in the page (Add a pack) from the spreadsheet template, or built in when the page is rebuilt from source.
