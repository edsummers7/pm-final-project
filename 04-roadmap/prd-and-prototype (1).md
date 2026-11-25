Link to demo - https://claude.ai/artifact/JmQXZDpgkzstPMn2wcTVnJ

# Spotlight Curated Real, Simplified PRD (StreamLine)

**Author:** Me · **Status:** Draft · **Target:** High-Fidelity Prototype · **Persona:** The Wanderer

## 1. The Big Picture
- **Vision:** To Eliminate the chances our customers walk away by placing in the hand of our users the ability to search through our curated library to find exactly what they want
- **Press release:** Today, StreamLine launched Spotlight, a hand-picked rail at the top of the homepage built for people we call Wanderers: new viewers who are still finding their way around a large library and haven't yet built a viewing habit. Wanderers don't arrive knowing what they want. When a cluttered library doesn't show them something good fast, they search Google or move to a competitor, and most never come back. Spotlight puts a short list of great titles in front of them straight away, so their first search ends inside StreamLine.

Every Spotlight title is chosen by hand, and the best finds carry a Hidden Gem badge so unfamiliar picks are easy to trust. Spotlight is shown only to Wanderers. Power Users, the long-time viewers who already know their way around, see their library exactly as before. StreamLine is measuring the launch against a holdout group to see how much it lifts Month 1 retention.

The Wanderer is defined once, early, as someone who is new and has no habit yet, and Power Users are defined by contrast. If you'd like a more reader-friendly version, I can drop the word "Wanderer" from the press release and just describe those viewers.
- **Success metric:** Month 1 retention of Spotlight-exposed Wanderers vs. holdout (target +10 points)
- **Guardrail:** Power User sessions per week ≥ 4.8 and average session length ≥ 24 min  The primary metric field is short, so if it needs the baseline, add "(Full Library Nov cohort: 63%)". I left the 74-79% Spotlight cohort figures out of the press release, because those weren't a holdout and a launch announcement shouldn't claim them as results.

## 2. The Details
### User stories
- As a Wanderer, I want to see a short hand-picked rail of great titles as soon as I open the homepage, so that I find something to watch without leaving for Google.
- As a Wanderer, I want a Hidden Gem badge on titles I haven't heard of, so that I trust them enough to try one.
- As a Wanderer, I want to start playing a title from the rail in one tap, so that I'm watching before I lose interest.
- As a Wanderer, I want the rail to skip titles I've already watched or can't play, so that every pick is something I can watch right now.
- As a Power User, I want my homepage to stay exactly as it is, so that I can keep finding things in my library as quickly as I do today.
### Screens to build
- 1. Home, Wanderer homepage with the Spotlight rail above the fold: a rail title, 10 to 15 hand-picked tiles, and a Hidden Gem badge on some tiles. A toggle switches between Wanderer, Holdout and Power User views.
- 2. Core, title detail after tapping a tile: artwork, one-line synopsis, Hidden Gem badge if it applies, a Play button, and a back-to-rail control.
- 3. Confirmation, playback started: shows the title playing, with a note that it has been added to Continue Watching. Returning to Home shows the rail without that title.
### Functional requirements
- The system must show one Spotlight rail of 10 to 15 hand-picked titles above the fold on the homepage for users in the Wanderer segment.
- The system must read the rail's title list from a config file, so the list can change without a code change to the tile components.
- The system must not show the rail to Power Users (the top 22% by LTV); their homepage must be identical to today's.
- The system must randomly assign each eligible Wanderer to exposed or holdout on first visit and keep that assignment for the whole Month 1 window.
- The system must remove any title that is unavailable in the user's region or licence from the rail.
- The system must hide the entire rail if fewer than 5 valid titles remain.
- The system must log rail exposure, rail click and playback start per user and per group, so Month 1 retention (exposed vs holdout), Power User sessions per week and average session length can be reported.
- The system must let the rail be turned off through a feature flag, with no deploy.
### Smart behaviors (Situation → Outcome)
- If the user is a Power User → no rail is rendered and the homepage is unchanged
- If the user is a Wanderer in the holdout group → show the standard homepage with no rail, and still log their activity
- If a curated title is unavailable in the user's region → remove it and close the gap in the rail
- If fewer than 5 valid titles remain → hide the whole rail
- If the user has already watched a title → skip it and show the next curated title
- If a title meets the Hidden Gem rule (high quality, low viewcount) → show the badge on its tile
- If the user taps a tile → open the title detail screen and log a rail click
- If the user taps Play → start playback, log playback start, and add the title to Continue Watching
- If Power User sessions per week fall below 4.8 or average session length falls below 24 minutes in the exposed group → flag for review, with the kill switch ready
- If the kill switch is turned on → hide the rail for everyone straight away
### Technical constraints
- No external API calls and no database; React useState only, with the title list hard-coded as sample data.
- No recommendation algorithm, ML or personalisation; the rail is a fixed hand-picked list.
- No real segment calculation or random assignment; the Wanderer, Holdout and Power User views are switched with a toggle.
- No real analytics backend; log events to an on-screen or console event log.
- No CMS or admin UI, and no sheet sync.
- No real streaming; Play only moves to the confirmation screen.
- Homepage only: no rail on search, post-playback or email.
- Placeholder artwork and fictional titles only.
- Exactly 3 screens.

## 3. The Logistics
### Features out
- No algorithmic ranking, personalisation or taste-based reordering (A5)
- No AI or hand-written reasons per title (A2)
- No mood filtering (A4)
- No curator profiles or attribution (A7)
- No change to the Power User homepage
- No CMS, approval workflow or admin UI
- No rail on search, post-playback or email (A6)
- No homepage or navigation redesign
- No watch party, offline downloads or advanced filters (A8, A10, A9)
### Edge cases & safety guard
- Title unavailable in the user's region → remove it and close the gap
- Fewer than 5 valid titles remain → hide the whole rail, no empty or broken state
- User already watched a title → skip it and show the next curated title
- Holdout Wanderer → standard homepage with no rail; activity is still logged
- Power User → no rail and an unchanged homepage
- Guardrail breach (Power User sessions per week below 4.8, or average session length below 24 min) → flag for review, kill switch ready
- Kill switch on → rail hidden for everyone immediately
- Safety: never show the rail to a Power User
- Safety: never show a title the user can't play
- Safety: never change a user's holdout or exposed assignment during their Month 1 window
### Decision log
- 1. Removed algorithmic personalisation (A5) and AI reasons (A2) from this release to focus on a hand-picked rail, which needs no model and fits 2 engineers and 1 designer in a 3-week sprint.
- 2. Excluded Power Users from the rail entirely instead of showing it to everyone, to protect the 22% of users with the highest LTV, their 4.8 sessions per week and the 24-minute session guardrail.
### Evals
- Accuracy: 100% of test cases show the right homepage (Wanderer sees the rail; Holdout and Power User do not)
- Time-on-task: a Wanderer reaches playback from the homepage in 3 taps or fewer and under 30 seconds, in at least 4 of 5 test users
- Safety: 0 unavailable titles shown, 0 Power User homepages altered, and the rail hidden whenever fewer than 5 valid titles remain

## MoSCoW scope
- **Must:** One hand-picked rail on the homepage. It has a title and 10-15 titles, reuses the existing tile and carousel components, and sits above the fold for Wanderers. This is the moment-of-misery fix: they see something good before they leave for Google.; Homepage Spotlight rail: one rail of 10 to 15 hand-picked titles above the fold, reusing the existing tile and carousel components; Title list held in a config file, so it can change without a code change; Wanderer-only exposure; Power Users (top 22% by LTV) excluded and their homepage unchanged; Randomised holdout of eligible Wanderers, with assignment fixed for the Month 1 window; Availability filter that removes unlicensed or unavailable titles, and hides the whole rail if fewer than 5 valid titles remain; Instrumentation: exposure, rail click and playback start; Month 1 retention by group; Power User sessions per week; average session length; Feature flag and kill switch, with no deploy needed
- **Should:** Hide titles the user has already watched; Start and end dates per title, for scheduled weekly rotation; Hidden Gem badge on rail tiles (depends on A3); Automated guardrail alerting if Power User sessions per week or session length (24-minute floor) drops in the exposed group; Sheet-to-config sync, so editors update the list without a ticket
- **Could:** Several themed rails (genre or theme); Tests on rail position and title copy; "Not interested" dismiss on a tile; Regional or language-specific curation lists
- **Won't (now):** Algorithmic ranking, personalisation or taste-based reordering (A5); AI-generated or hand-written reasons per title (A2); Mood filtering (A4); Curator profiles or attribution (A7); Any change to a Power User's homepage; A CMS or approval workflow; The rail on search, post-playback or email (A6); Homepage or navigation redesign; Watch party, offline downloads, advanced filter engine (A8, A10, A9)

---
**Builder hook:** Build a working prototype based on this PRD. Use the User Story as the core flow, Functional Requirements as build constraints, and prioritize speed and clarity over visual complexity.
