# GVR Draft Lottery

A casino-style slot machine that reveals fantasy football draft order one name at a
time, counting down from the last pick to pick #1. Single HTML file, zero
dependencies — double-click `index.html` and share your screen.

Built at a fixed **432 × 768 (9:16)** stage that scales to fill any window, so it
frames correctly for a vertical phone recording.

## Setting your league

Two options:

1. **In the app** — hit the gold **EDIT** button on the machine, type one name per
   line, then **SAVE & RESET**. Nothing to install, works mid-draft-night.
2. **In the file** — edit the `NAMES` array at the top of the `<script>` block in
   `index.html`.

Names of 6 characters or less read best on the reel (9 is the hard cap). The app
works with any roster size from 2 up, not just 12 — the pick countdown, the board,
and the final screen all follow the list length.

## How it runs

- Each **SPIN** picks a winner at random from the names still in the pool, so there
  are never repeats.
- The reel scrolls fast, decelerates, overshoots slightly, and settles.
- On landing: the winning name flashes gold, the cabinet shakes, confetti fires,
  and the panel reads `PICK #12 → NAME`.
- The draft board below fills in as picks are assigned.
- After the last pick, a full draft order summary appears (pick 1 at the top) with
  **COPY LIST** to paste into the family group chat.

`SPACE` or `ENTER` also spins, so you can drive it without the cursor on screen.
**SFX** toggles the synthesised reel clicks and win chime.

## Running it on a phone

It works in mobile Safari and Chrome — the stage scales to fit whatever screen it
lands on. Two ways to get it there:

- **GitHub Pages** (easiest): repo *Settings → Pages → Deploy from branch*, pick
  this branch and `/ (root)`. Open the resulting URL on the phone and bookmark it.
- **Send yourself the file** — AirDrop, email, or a message. On Android, open it
  from Files in Chrome. On iOS, opening a local `.html` from the Files app is
  unreliable, so the hosted URL is the better route.

For a clean recording with no browser chrome in frame, use **Add to Home Screen**
and launch from the icon — the meta tags in the file make it open standalone. On
Android you can also double-tap the backdrop for true fullscreen (iPhone Safari
has no Fullscreen API, so Add to Home Screen is the way there).

Two phone-specific notes: the iPhone's ring/silent switch mutes WebAudio, so flip
it to ring if you want the reel clicks in the recording; and hold the phone
portrait — landscape shrinks the machine to fit the short edge.

## About the reel landing

The winner is chosen *before* the animation starts, and the strip is built with
that name at a known index. The animation is a `requestAnimationFrame` tween to
that index's exact pixel offset — `(winIndex - 1) * CELL_H` — and the final frame
assigns that offset literally rather than letting an easing curve approximate it.
The reel cannot drift or stop between two names.

One thing to keep in sync if you edit the CSS: `CELL_H` in the script must equal
the `.cell` height rule. Everything else (window height, payline position, the
arrow markers) is derived from it.
