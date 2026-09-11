# Interior Reimagine Workflow

Turns a photo of a real Singapore room into a photorealistic furnished version in a chosen style, run in ChatGPT image generation.

Same room, same camera, same fixed positions. New finishes, furniture and styling.

## How to run

1. Open a new ChatGPT chat and attach the room photo.
2. Paste a kickoff from `kickoff.md`.
3. ChatGPT shows a Room Audit, generates one image per style, and shows a QC table for each.

## Modes

- REVAMP (default): renovation concept. Flooring, walls, cabinet fronts, countertops and sanitary ware get new finishes in the same positions.
- STAGE: listing accuracy. Every existing finish stays. Only furniture and decor change.

## Files

All files sit in the repo root. No folders.

- `START-HERE.md`: the complete engine. The only file ChatGPT must read.
- `kickoff.md`: prompts to paste.
- `STYLE-INDEX.md`: style list with marketing fit.
- `style-01` to `style-12`: the style library.
- `style-template.md`: copy this to add a style.

## Shooting the source photo

- Landscape, from the doorway or a corner so two walls show.
- Phone at about chest height, held level with vertical lines straight.
- Daytime, lights on, curtains open.
- Use the 1x lens where possible. The 0.5x lens bends walls, and the render keeps that distortion.
- One photo per angle.

## Editing rules

- START-HERE wins over every other file.
- Keep every file in the root with a unique name.
- To update a file, upload it with the same name. GitHub overwrites it.
- New styles also need a row in STYLE-INDEX.md and in section 9 of START-HERE.
- Log changes in `CHANGELOG.md`.

## Posting renders

- REVAMP: caption as a renovation concept, not the current condition.
- STAGE: caption as virtually staged for illustration.
