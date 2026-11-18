# CLAUDE.md: Maintainer Brief for interior-reimagine-workflow

Read this whole file before touching anything. It is the complete brief for auditing, reassessing, upgrading and deploying this repo. It is written for Claude Code.

ChatGPT never reads this file. ChatGPT reads only `START-HERE.md` and the style files, or `start-here-bundle.md` when links fail. This file is for maintainers.

Last updated: 18 November 2026, at repo version 1.1.

---

## 1. Your job in this session

Kiian has handed you this repo for a full audit and upgrade. Do all of the following, in order:

1. Audit every file against the constraints in section 6 and the design intent in section 7.
2. Reassess whether the workflow produces accurate, usable images for Singapore property marketing. Use the dry-run cases in section 11.
3. Fix every defect you find.
4. Implement upgrades from section 12 that pass the bar in section 12.
5. Verify with the checklist in section 13.
6. Deploy (section 14).
7. Write the handback report (section 15).

Work without asking questions unless a change would break a constraint in section 6. If you hit one, stop and ask. If Kiian's session prompt sets approval gates, such as an audit report before any change, follow those gates. They win over this paragraph.

---

## 2. What this repo does

It is a prompt engine for ChatGPT image generation. Kiian uploads a photo of a real room in a Singapore home, names the room, picks one or more styles from a library, and picks a mode. ChatGPT produces a photorealistic furnished or renovated version of that exact room.

Core rule: same room, same camera, same fixed positions. New finishes, furniture and styling.

There is no application code apart from `validate.py`, which checks the repo. The "code" is the instruction set in Markdown. Treat every sentence in `START-HERE.md` as executable logic for a model.

---

## 3. Owner and use case

- Owner: Kiian, a Singapore property agent who runs the SG Launch Homes brand on Instagram, TikTok and RedNote.
- Audience for the images: Singapore homebuyers. Main niche is HDB upgraders moving to condos. Also investors, young couples, families and foreign buyers.
- Where images go: listing carousels, social posts, renovation-potential content for old resale units, and client presentations.
- Property types: HDB flats, condos, ECs and landed homes.
- Working style: execution first, short active sentences, no fluff. He wants complete outputs with gaps flagged, not clarifying questions.

Accuracy matters legally. Singapore property ads are regulated by the Council for Estate Agencies (CEA), which requires ads to describe a property accurately. In December 2025 a CEA director said agents should highlight when ad images are AI-enhanced or AI-generated. That is why STAGE mode exists and why every image gets a caption that names AI (START-HERE section 7). Never weaken those rules.

---

## 4. How Kiian runs it today

He opens a new ChatGPT chat, attaches a room photo, and pastes the Full kickoff from `kickoff.md`:

```text
Source of truth: https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/START-HERE.md
Mirror if that fails: https://cdn.jsdelivr.net/gh/kiianlow/interior-reimagine-workflow@main/START-HERE.md
Read it fully and follow it. Start your reply with its version line. If neither link opens, say so and stop. Never guess the rules.

Room: [living room / dining / master bedroom / common bedroom / study / kitchen / bathroom / balcony]
Styles: [01 to 12, comma separated, for example 06 or 01, 02, 06]
Mode: [REVAMP / STAGE]
Property: [HDB / condo / EC / landed], [low / mid / high floor]
Also keep: [optional, for example existing kitchen cabinets]
Also change: [optional, for example remove window grilles (REVAMP only)]
Keep the architecture, dimensions and every fixed fixture exactly where they are.
```

Styles take two-digit numbers, 01 to 12, one or several. Follow-ups in the same chat use the short commands in START-HERE section 14, such as "go", "Next style: 07", "summary" and "Same unit, same Style Lock. Next room: master bedroom."

If you change any field name, the URL, or the style numbering, update `kickoff.md`, and list the new kickoff verbatim in the handback report. Kiian keeps a saved copy of the prompt above.

---

## 5. How it executes at runtime

1. ChatGPT fetches `START-HERE.md` through the raw URL, or the jsDelivr mirror if raw fails. Both return plain text. GitHub page URLs return mostly site navigation, which wastes context and causes skipped rules. Never use them as a fallback.
2. ChatGPT prints "Engine X.Y loaded" and the style files it opened. This handshake is how Kiian sees a failed fetch.
3. ChatGPT opens only the style file(s) named in the kickoff, using the raw links in START-HERE section 9. If both links fail, Kiian attaches `start-here-bundle.md`.
4. ChatGPT checks the photo, writes a Room Audit, builds an image prompt, and calls its image tool with the photo as the base image.
5. The image tool sees only the prompt and the photo. It never sees this repo. Every lock must be carried inside the generated prompt. This is the most important fact about the system.
6. ChatGPT runs QC against the photo, revises if needed, then moves to the next style from the original photo. If its reply ends after an image, Kiian sends "go".

Implications:
- Keep START-HERE self-sufficient. Any rule that lives only in another file will be ignored.
- Each extra fetch is a point of failure. Today a run needs two fetches: START-HERE plus one style file.
- Generated image prompts must stay under about 200 words. Longer prompts dilute the locks. Only the Prompt block, one room line and (REVAMP only) the REVAMP finishes go into the prompt.

---

## 6. Hard constraints

Do not break any of these. If an upgrade needs one broken, propose it in the handback report instead.

1. Repo name stays `interior-reimagine-workflow` under `kiianlow`. Branch stays `main`. The repo stays public. Every raw link and Kiian's saved kickoff depend on this.
2. Flat layout. Every file sits in the repo root. No folders. Kiian sometimes updates through GitHub's web uploader, which flattens folders. The sister repo broke twice from this. Even if you deploy with git push, keep it flat.
3. Every file name is unique and lowercase with hyphens, except the existing uppercase files: START-HERE.md, README.md, CHANGELOG.md, STYLE-INDEX.md, CLAUDE.md.
4. START-HERE.md wins over every other file. If you change a rule, change it in START-HERE first.
5. Every link in START-HERE uses the raw format: `https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/<file>`. Every one must return HTTP 200 after deploy.
6. The style list exists in three places that must match exactly in numbers and names: START-HERE section 9, STYLE-INDEX.md, and the "Style numbers" line in kickoff.md.
7. Every style file keeps these headings in this order: Prompt block, Mood, Palette, Furniture, Textiles and window treatments, Lighting, Greenery and decor, REVAMP finishes, Avoid, Marketing fit. START-HERE depends on "Prompt block", "Furniture" and "REVAMP finishes" by name.
8. Prompt blocks stay under 70 words. Current range is 35 to 49.
9. LOCKED items never change in any mode: walls, partitions, columns, beams, ceiling height and shape, window count, position, size and frames, the view outside, door openings, stairs, railings, household shelter door and vent, DB box, window grilles, and the camera. The only exceptions are the user overrides in START-HERE section 3: window grilles and the ceiling, in REVAMP only, when the user names them.
10. Captions stay mandatory and name AI. REVAMP is an AI-generated renovation concept. STAGE is virtually staged with AI.
11. No invented views, no added windows or openings, no new false ceilings unless the user asks.
12. Writing style in all repo files: plain English, short active sentences, no em dashes, no semicolons, no hype words. Kiian reads these files too.

---

## 7. Design decisions and why

Keep these unless testing shows they fail. If you change one, say why in the handback report.

- Two modes. REVAMP refinishes surfaces and replaces fittings in the same positions. STAGE keeps every finish and swaps only loose items. Kiian wants full renovation concepts, but a listing image must represent the unit as it is. One mode cannot do both.
- STAGE carries an explicit keep list into the image prompt, and visible wear stays. The image tool never sees the mode name, so the prompt must say what to keep.
- Room Audit with four lists: Locked, Refinish, Remove, Add. It forces the model to name fixed items with positions before styling. Without it, models move windows and resize rooms.
- Positions are stated positively in the image prompt, for example "sliding window on the left wall, two panels". Long "do not" lists weaken image prompts.
- Prompt blocks are room-neutral: mood, palette, materials and light only. Furniture comes from one room line per room type, and fixed finishes come only from REVAMP finishes. This stops sofas in bathrooms and finish changes leaking into STAGE. `validate.py` enforces it.
- Every style starts from the original photo. Later styles never inherit furniture from earlier images.
- Regenerate vs edit. Geometry errors get regenerated from the original photo, because editing a broken image keeps the broken geometry. Styling errors get edited in place. Edits may redraw the whole image, so every edit gets the hard checks again.
- Three attempts per image, then stop and report. Edits count as attempts. This prevents endless loops that burn Kiian's ChatGPT usage.
- Evidence-based QC with 6 hard checks and 1 styling check, and an UNCLEAR result. Models grade their own work too kindly. Counting windows and openings against the photo makes failure visible. UNCLEAR (photo) does not block ACCEPT when the photo itself is unreadable, because no number of attempts can fix that.
- One image per reply is allowed, with "go" to continue. ChatGPT's image tool may end the reply after an image (unverified user reports).
- Keep the camera even if the photo is tilted or shot on a 0.5x lens. Correcting perspective changes geometry.
- Style Lock for multi-room units, so a listing carousel looks like one home. It feeds the prompt and travels to a new chat through the run summary.
- Singapore context: furniture sized for compact homes, equatorial light, no cold-climate props, HDB fixed features (household shelter, DB box, grilles, rubbish chute), HDB styled practically rather than like a hotel. Dark palettes keep walls light in small or dim rooms.
- Defaults instead of questions. Kiian wants output, so missing inputs get defaults that are listed in the chat.

---

## 8. File map

| File | Read by | Role |
|---|---|---|
| START-HERE.md | ChatGPT | The complete engine. 16 sections, under 2,500 words. |
| style-01 to style-12 | ChatGPT | Style library. One file per style. |
| start-here-bundle.md | ChatGPT, when links fail | Engine plus all styles in one file. Generated. Never edit by hand. |
| kickoff.md | Kiian | Prompts he pastes into ChatGPT, including the offline fallback. |
| STYLE-INDEX.md | Kiian, maintainers | Style list with mood and marketing fit. |
| style-template.md | Kiian, maintainers | Blank style file for adding styles. |
| validate.py | Maintainers | Repo checks. `--bundle` rebuilds the bundle. |
| README.md | Humans | How to run, modes, photo tips, failure guide, posting rules, editing rules. |
| CHANGELOG.md | Humans | Version history. |
| CLAUDE.md | Claude Code | This brief. |

START-HERE sections: 1 What this does, 2 Run sequence, 3 Inputs and defaults, 4 Modes, 5 Room Audit, 6 Singapore context, 7 Captions and accuracy, 8 Photo handling, 9 Style library, 10 Generation prompt, 11 QC, 12 Revision, 13 Multi-room sets, 14 Short commands, 15 Room types, 16 Run summary.

Styles: 01 Scandinavian, 02 Japandi, 03 Modern Minimalist Monochrome, 04 Wabi-Sabi, 05 Natural Minimal, 06 Warm Minimalist, 07 Quiet Luxury, 08 Dark Modern Luxury, 09 Organic Modern, 10 Modern Tropical, 11 Mid-Century Modern, 12 Industrial.

---

## 9. History

- Origin: a single file, `Interior_Reimagine_3Style_Workflow.md`, with three styles (Scandinavian, Japandi, Modern Minimalist Monochrome). It allowed only furniture and decor changes and locked the flooring and cabinetry. That contradicted Kiian's goal of revamping everything renovatable, which is why REVAMP mode was added.
- Version 1.0, September 2026: rebuilt in Claude.ai as this repo. Expanded to 12 styles, added modes, Room Audit, Singapore context, QC, revision cap, Style Lock and captions.
- Uploaded 11 September 2026, commit 6f24bd3. Verified then: public, 18 files, all in root, every raw link returned 200.
- 12 November 2026: CLAUDE.md written locally. It was not pushed until version 1.1.
- Version 1.1, 18 November 2026: two-stage audit in Claude Code (read-only report, then approved fixes). STAGE keep list in the prompt, room-neutral Prompt blocks with room lines, room-type rules, version handshake, photo check, narrowed overrides, tighter QC, AI captions, run summary, validate.py and the offline bundle.
- No field-test results have been reported back yet. Treat real-world performance as unproven.

Lessons from the sister repo `kiianlow/interior-render-workflow` (floorplan to render), which went through the same build:
- The web uploader flattened folders and left 29 duplicate files in the root. The engine pointed to stale copies, so edits never took effect.
- Folder links returned 404 after flattening.
- Fix in both repos: flat layout, raw links, one self-sufficient START-HERE.

---

## 10. Known gaps and open questions

Status after version 1.1. Investigate the open ones.

1. Untested in the field. No QC tables or failure reports exist yet. OPEN. Needs real photos run in ChatGPT.
2. Raw URL fetching in ChatGPT is not guaranteed. CLOSED in 1.1 with a version handshake, a jsDelivr mirror and `start-here-bundle.md`. A ChatGPT Project setup is documented in README but untested.
3. Multi-style runs in one chat may drift. MITIGATED in 1.1: every style starts from the original photo and carries no earlier furniture. Needs a field test.
4. Edit-in-place may shift geometry. MITIGATED in 1.1: every edit counts as an attempt and gets the hard checks again. Still unverified in ChatGPT.
5. STAGE finish leakage. CLOSED in 1.1: Prompt blocks carry no finish words (enforced by validate.py), and the prompt has an explicit STAGE keep line.
6. Style 08 in small or dim HDB rooms. CLOSED in 1.1: the rule now lives in START-HERE sections 6 and 10.
7. Kitchens and bathrooms. CLOSED on paper in 1.1: fixed positions now cover sink, hob, hood, fridge and washer spaces, basin, WC, shower and floor trap, and room lines carry no furniture there. Needs a field test.
8. Rooms with no clear type. CLOSED in 1.1: section 15 covers combined rooms, balconies, service yards and unclear rooms.
9. People, pets and reflections. CLOSED in 1.1: section 5 REMOVE list and section 8 photo check.
10. Style list in three places. CLOSED in 1.1: validate.py checks they match.
11. Singapore context is duplicated with the sister repo. OPEN. Both copies were checked by hand in 1.1. A shared file would need a cross-repo fetch, which adds a failure point.
12. Kickoff style placeholder. CLOSED in 1.1: "Styles: [01 to 12, comma separated, ...]".
13. ChatGPT may end its reply after each image. MITIGATED in 1.1 with the "go" command. Unverified.

---

## 11. Reassessment: dry-run cases

You cannot run ChatGPT image generation. Do paper dry runs instead. For each case, walk through START-HERE as ChatGPT would, write the Room Audit and the final image prompt it would produce, then check them against the constraints. Fix any rule that produces a wrong or ambiguous result.

1. Empty new HDB BTO living room, style 06, REVAMP, mid floor.
2. Old 1990s resale HDB kitchen with dated cabinets, style 02, REVAMP.
3. Condo bathroom, style 07, STAGE.
4. Furnished, cluttered condo master bedroom, style 04, STAGE.
5. Living room photo shot on a 0.5x lens with leaning walls, style 01, REVAMP.
6. Dim evening photo where the window frame is hard to read, style 08, REVAMP.
7. One living room, styles 01, 02 and 06 in one run.
8. Kickoff naming an unknown style, "Coastal".
9. Kickoff with no style.
10. Landed home living room with stairs, style 10, REVAMP.
11. HDB room with window grilles and the household shelter door visible, "Also change: remove window grilles". Check the override rule in START-HERE section 3 resolves this cleanly.
12. Next room in the same unit, using the Style Lock.

Record each case in the handback report as PASS or FIXED, with one line on what changed.

---

## 12. Upgrade backlog

Only implement an upgrade if it improves accuracy, cuts Kiian's steps, or reduces failed runs, and it keeps every constraint in section 6.

Done in 1.1: validate.py, the offline bundle, multi-style handling, the style number hint, room-type notes.

Open:
1. Field-test intake. When Kiian sends back QC tables or run summaries, record the failures here and fix the rules they point to.
2. Test the ChatGPT Project route in README. If it works, make it the main path and shorten the kickoff.
3. If field tests show prompts over 200 words drop locks, trim the section 10 template further.

Do not add: new folders, extra required fetches, a different AI tool, or features that need a paid service.

---

## 13. Verification checklist

Run all of these before deploying and paste the results into the handback report.

1. `python3 validate.py --bundle`, then `python3 validate.py`. It must print PASS. It covers file names, flat layout, START-HERE links, the three style lists, style headings, Prompt block length and words, room and finish lines, dashes, semicolons, hype words, version lines, the START-HERE word cap and bundle freshness.
2. File count and names match the file map you report.
3. No folders exist apart from `.git`.
4. Every raw link in START-HERE returns 200 after deploy:
   ```bash
   grep -o 'https://raw.githubusercontent.com[^ |)]*' START-HERE.md | sort -u | while read u; do echo "$(curl -s -o /dev/null -w '%{http_code}' "$u") $u"; done
   ```
5. The jsDelivr mirror and the bundle raw link return 200 and show the new version line.
6. START-HERE stays under 2,500 words. Report the count.
7. Version number in START-HERE matches the newest CHANGELOG entry.

---

## 14. Deploy

1. Bump the version in START-HERE line 3, in the handshake line, and in the run summary block. Update README "Current engine" and the "Last updated" line here. Use 1.x for rule or feature changes, 1.x.y for fixes only.
2. Add a CHANGELOG entry with every change.
3. Run `python3 validate.py --bundle`, then `python3 validate.py`.
4. Commit with a message such as `v1.2: audit fixes and upgrades`, and push to `main`. Stage files by name so no `.DS_Store` gets committed.
5. If you cannot push, produce a zip of the repo root with no folders inside, and tell Kiian to upload the files through Add file, Upload files, then commit.
6. After the push, run check 4 in section 13 against the live repo. Raw GitHub can cache for a few minutes. Retry once if a link returns 404 right after the push.
7. Refresh the jsDelivr mirror by opening `https://purge.jsdelivr.net/gh/kiianlow/interior-reimagine-workflow@main/START-HERE.md`, then confirm check 5.

---

## 15. Handback report

End the session with a report Kiian can paste back into Claude.ai. Write it to `HANDBACK.md` in your working directory. Do not commit it to the repo. Use this structure:

```text
REPO: kiianlow/interior-reimagine-workflow
VERSION: [new version]
COMMIT: [hash]
DATE: [date]

KICKOFF PROMPT (current, verbatim):
[the full prompt Kiian should paste from now on]

FILES: [count] files, all in root
[list]

CHANGES:
- [one line each]

DRY RUNS (section 11):
- [case number]: PASS / FIXED, [one line]

GAPS CLOSED:
- [gap number from section 10]: [how]

GAPS STILL OPEN:
- [gap number]: [why, and the suggested next step]

DESIGN DECISIONS CHANGED:
- [decision]: [why]

VERIFICATION:
[results of section 13 checks]

NEXT STEPS FOR KIIAN:
- [for example: run one real test with a kitchen photo and send the QC table back]
```

Also update section 9 of this file with a one-line history entry for this session, and the "Last updated" line at the top.
