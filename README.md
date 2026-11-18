# Interior Reimagine Workflow

Turns a photo of a real Singapore room into a photorealistic furnished version in a chosen style, run in ChatGPT image generation.

Same room, same camera, same fixed positions. New finishes, furniture and styling.

Current engine: version 1.1.

## How to run

1. Open a new ChatGPT chat and attach the room photo. Use a model with web access. A Thinking model is likely to follow the rules more closely (untested).
2. Paste the Full kickoff from `kickoff.md`.
3. Check the first line of the reply. It must say "Engine 1.1 loaded". If it shows another version or no version, the rules did not load. Start again or use the offline fallback.
4. ChatGPT shows a Room Audit, then one image per style, each with a QC table, a decision and a caption.
5. If a reply stops after an image, send `go`.
6. At the end, ChatGPT prints a run summary. Keep it. Its Style Lock carries the look to the next room.

## Modes

- REVAMP (default): renovation concept. Flooring, walls, ceiling lights, cabinet fronts, countertops and sanitary ware get new finishes in the same positions.
- STAGE: listing accuracy. Every existing finish stays, including wear and stains. Only furniture and decor change.

## Files

All files sit in the repo root. No folders.

- `START-HERE.md`: the complete engine. ChatGPT reads it first, then only the style files named in the kickoff.
- `kickoff.md`: prompts to paste, including the offline fallback.
- `start-here-bundle.md`: the engine and every style in one file. Built by `validate.py`. Attach it when links fail.
- `STYLE-INDEX.md`: style list with marketing fit.
- `style-01` to `style-12`: the style library.
- `style-template.md`: copy this to add a style.
- `validate.py`: checks the repo and rebuilds the bundle.
- `CLAUDE.md`: maintainer brief for audits and upgrades in Claude Code. ChatGPT does not read it.

## Shooting the source photo

- Landscape, from the doorway or a corner so two walls show.
- Phone at about chest height, held level with vertical lines straight.
- Daytime, lights on, curtains open.
- Use the 1x lens where possible. The 0.5x lens bends walls, and the render keeps that distortion.
- No people, pets or private items in the frame. Check mirrors for your reflection.
- One photo per angle.

## When a run fails

- Wrong or missing version line: the rules did not load. Use the offline fallback in `kickoff.md`.
- A window, door or wall keeps moving after 3 attempts: reshoot brighter, on the 1x lens, from a spot where every window frame is clear. Or try a simpler style such as 05 or 06.
- An "UNCLEAR (photo)" result: the photo is too dark or blurred at that spot. Check that item by eye before posting.
- Any edit you ask for can shift geometry. Compare windows and doors with the photo again after every edit.

## Posting renders

ChatGPT prints a caption under every image. Use it on every post.

- REVAMP: "AI-generated renovation concept. Not the unit's current condition."
- STAGE: "Virtually staged with AI. Furniture and decor not included."

Before posting:
- Compare windows, doors, the shelter door, fixed fittings and the view with your photo, side by side.
- Label the image itself, for example with a small "AI concept" or "Virtually staged" tag added in Canva. A caption can be cropped away when the image is shared.
- Never use a REVAMP image as a listing photo of the unit's condition. Use it for renovation-potential content.
- Where possible, show the original photo next to the render.

CEA expects agents to disclose AI-enhanced or AI-generated images in ads. Check the current CEA guidance or ask your agency for exact wording.

## Optional: ChatGPT Project (untested)

To skip the fetch on every chat, create a ChatGPT Project, upload `start-here-bundle.md` as a project file, and set the project instructions to "Follow start-here-bundle.md for every chat." Then the kickoff only needs the Room, Styles, Mode and Property lines. Re-upload the bundle after every update. The version line shows if the project copy is stale.

## Editing rules

- START-HERE wins over every other file.
- Keep every file in the root with a unique name.
- To update a file, upload it with the same name. GitHub overwrites it.
- New styles also need a row in STYLE-INDEX.md, in section 9 of START-HERE and in the "Style numbers" line of kickoff.md.
- After any change, run `python3 validate.py --bundle` and then `python3 validate.py`. Upload the rebuilt `start-here-bundle.md` too.
- After a change, the jsDelivr mirror can serve the old version for up to 12 hours. Open https://purge.jsdelivr.net/gh/kiianlow/interior-reimagine-workflow@main/START-HERE.md to refresh it.
- Log changes in `CHANGELOG.md`.
