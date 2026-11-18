# Changelog

## 1.1 (18 November 2026)

Audit fixes and upgrades. Engine rules changed, so this is a minor version.

Engine (START-HERE):
- Version handshake. The first reply must print "Engine 1.1 loaded" and the style files opened, so a failed fetch is visible.
- STAGE now reaches the image tool. The prompt carries a "Keep every finish and fitting exactly as photographed" line, and visible wear and stains stay.
- Every style starts from the original photo. No furniture or finishes carry over between styles.
- One image per reply is allowed. The user sends "go" to continue.
- Prompt template trimmed. Prompt block plus one room line replace the old living-room-only block.
- New section 15, Room types: rules for living, dining, bedroom, study, kitchen, bathroom, balcony, service yard and combined rooms.
- New section 16, Run summary, to carry results and the Style Lock into a new chat.
- Photo check before the Room Audit: dark photos, 0.5x lens, people, pets, reflections and combined rooms.
- LOCKED list adds the rubbish chute hopper, gas pipes and meter, sprinklers, smoke detectors, bay window ledges, AC ledges, planter boxes and balcony screens.
- Kitchen and bathroom fixed positions now cover the hood, fridge space, washer space, shower and floor trap.
- Overrides narrowed. Window grilles and the ceiling can change in REVAMP only when the user names them. Nothing LOCKED changes in STAGE.
- QC cut to 6 hard checks and 1 styling check, with fixed decisions: ACCEPT, REGENERATE, EDIT, STOP. Edits count as attempts and get the hard checks again.
- UNCLEAR (photo) no longer blocks ACCEPT when the item was already unclear in the photo. This stops runs burning 3 attempts on a dark window.
- Dark-palette rule for small or dim rooms moved into START-HERE so it reaches the prompt.
- Style Lock gains Mode and wet-area flooring, and now feeds the prompt.
- Captions name AI and print under every image.
- The non-raw GitHub link in section 9 is gone. Fallback is the kickoff mirror, then the bundle.

Styles:
- Prompt blocks are room-neutral, with no furniture, curtains or fixed finishes. Range now 35 to 49 words.
- Furniture sections have one line per room: Living, Dining, Bedroom, Study, Kitchen, Bathroom, Balcony.
- REVAMP finishes gain Ceiling lights and Carpentry lines, plus a wet-area tile in Flooring.
- Template updated to match.

Tools and docs:
- Added `validate.py`. Checks layout, names, links, the three style lists, headings, Prompt block length and words, room lines, dashes, semicolons, version lines and bundle freshness. Builds the bundle with `--bundle`.
- Added `start-here-bundle.md`, the offline fallback.
- kickoff.md: mirror link, version check, offline fallback, "go" and "summary", next room in a new chat, a two-digit style hint.
- README: run steps, failure guide, posting and disclosure rules, optional ChatGPT Project setup, jsDelivr refresh.
- CLAUDE.md committed to the repo and updated.

## 1.0 (maintainer update, 12 November 2026)

- Added CLAUDE.md, the maintainer brief for a full audit and upgrade in Claude Code. No engine or style changes.

## 1.0

- Built from Interior_Reimagine_3Style_Workflow.md.
- Expanded the style library from 3 to 12, each with a Prompt block and REVAMP finishes.
- Added REVAMP and STAGE modes.
- Added the Room Audit: Locked, Refinish, Remove, Add.
- Added Singapore context, evidence-based QC, a 3-attempt revision cap, Style Lock for multi-room sets, and caption lines.
- Flat file layout so GitHub web uploads keep every path.
