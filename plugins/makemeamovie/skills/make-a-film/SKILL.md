---
name: make-a-film
description: Make a film with Make Me a Movie from a brief; use when the user asks for a video, film, clip or storyboard from Make Me a Movie
---

# Make a film with Make Me a Movie

Make Me a Movie turns a written brief into a short film — storyboard, cast, keyframes, voices,
clips, music, final cut — and seals every shot with a provenance manifest. Every stage costs
credits from the user's account. Follow these steps in order; never skip the approval.

## Steps

1. **Know the account.** Run `get_account` and tell the user the balance, today's remaining
   chat allowance, and which account is connected (its email).
2. **Create the draft.** Run `create_project` with a short title and the user's brief. Pass
   `target_sec`, `aspect` and `speech_mode` only if the user asked for them; otherwise leave
   the defaults (60 s, 16:9, narration). Nothing is generated or charged yet.
3. **Quote it.** Run `quote_film`. Show the user the credits (say it is an estimate), the time,
   and any blockers. Ask for explicit approval of the quoted figure. **Never assume it.** If
   there are blockers, fix them first (`update_project_settings`, a top-up on the web) and
   quote again.
4. **Start.** Only after the user approved the figure, run `start_film` with
   `approved_credits` equal to what they approved. It charges stage by stage as the run
   goes. If it refuses with `[quote_changed]`, show the new figure and ask again.
5. **Wait.** Poll `get_film_status` (with `wait_seconds` up to 45), waiting the
   `poll_after_seconds` it returns; when `poll_after_seconds` is null the film has settled —
   read `phase` (`done`, `failed`, `paused`, or `idle` with no jobs in flight) and act.
   Never run `start_film` again while the phase is `running`. Tell the user the progress
   line each time; do not spam. `paused` ends the wait too: quote again, ask again, and
   `start_film` resumes from what is finished.
6. **On `failed`,** follow `next_action`: `get_film` means a stage failed but an earlier
   finished cut is ready — run `get_film`, hand it over as in step 7, and offer to fix what
   failed; `start_film` resumes a run the service interrupted;
   `fix_then_start_film` means fetch the storyboard with `get_project`, edit what failed
   (`edit_storyboard`, `update_project_settings`), quote again, ask again, resume — nothing
   already paid for is regenerated; `none` means the balance cannot cover the rest: tell the
   user the shortfall and stop.
7. **On `done`,** run `get_film` and hand over the mp4 URL, the manifest URL and the
   provenance line (sources verified, models used).
8. **Share only on request.** Run `share_film` only when the user asks for a public link,
   after telling them the link is public and stays up until they delete the project on the
   website (the only way to take it down), with `confirm_public: true`.
   Send them `message_and_link` as it is.
9. **Prove provenance when asked.** Run `verify_film` by `project_id` and report which
   sources verified.

## Manual control

`write_storyboard`, `edit_storyboard`, `add_character`, `update_character_voice` and
`generate_stage` drive one stage at a time. Each charging tool takes `approved_credits`
and states its price in any refusal; get the user's approval for that figure first. A
storyboard or a portrait that takes too long answers `busy` and finishes on its own —
poll `get_film_status` after the 10 seconds that answer asks for, instead of asking for it
again. `cancel_job` and `stop_film` are the only cancellations.

## Money rules

- Prices when this plugin was published (`get_account` returns the live prices and
  `daily_cap`; use those when they differ): a storyboard is 2 credits, a keyframe 8, a cast
  portrait 5, narration 2 per scene, dialogue 6 per scene, the music bed 10, the final cut 5,
  and a clip 18 per ordered second. Films made from chat are capped per account per day
  (currently 3000 credits).
- Quotes are estimates: clips are billed per ordered second, and a scene whose line runs long
  is ordered longer than planned (up to 15 s, 270 credits, per scene). A line our voice has
  not recorded yet is priced from its words, and its clip is charged for the length the
  recording needs, which can come in above or below the quote.
- A failure refunds in full, automatically — an outage, a timeout, a rejected key, a model
  that withholds the video it made. The one exception to refunds applies only to stages
  started on the website after the author accepted a photoreal-people warning there; chat
  never sends that acceptance.
- Stopping loses running work: jobs already running were billed and are discarded.
- A refused call charges nothing, except a `generate_stage` that says it stopped partway:
  the submissions it names were charged. `[insufficient_credits]` says exactly how many more
  credits are needed. Credits are bought on the Make Me a Movie website, not here.
- There is no unshare: only deleting the project on the website takes a shared film down.
