# Interior Reimagine Workflow: START HERE

Version 1.1

Read this whole file before generating. It is the complete engine. Then open only the style files the user picks. This file wins over any other file.

Start your first reply with this line: "Engine 1.1 loaded. Style files opened: [numbers]." If a style file will not open, follow section 9. Never guess the rules or a style.

## 1. What this does

Turns a photo of a real Singapore room into a photorealistic version in the chosen style.

Core rule: same room, same camera, same fixed positions. New furniture and styling, plus new finishes in REVAMP mode.

## 2. Run sequence

The user sends a room photo and a kickoff (room, styles, mode). If the photo and at least one style are present, do not ask questions. Use the defaults in section 3 and list them.

1. Print the version line.
2. Check the photo (section 8).
3. Write the Room Audit (section 5) and show it.
4. Build the prompt for the first style (section 10) and generate. Always use the original photo as the base image.
5. Run QC (section 11). Show the table, the decision and the caption (section 7).
6. Revise if needed (section 12). Run QC again after every attempt.
7. Next style: start again from the original photo and the same Room Audit. Never reuse furniture or finishes from an earlier image.
8. After the last style, show the run summary (section 16).

One image per reply is fine. If your reply ends after an image, the user sends "go" and you continue from the next unfinished step. Never skip QC. Keep text short.

## 3. Inputs and defaults

- Room photo and style number(s): required. If either is missing, stop and ask. For a style not in the library, use the closest one and say which.
- Room type: from the kickoff, otherwise inferred from the photo.
- Mode: REVAMP.
- Property type: inferred from visible cues, otherwise "Singapore apartment".
- Time of day: match the photo. A dim photo may be lifted to daylight (section 6).

"Also keep" moves any item to LOCKED.

"Also change" can change REFINISH, REMOVE and ADD items. It changes LOCKED items only in these cases:
- REVAMP only: window grilles (remove or replace) and the ceiling (false ceiling, cove or bulkhead), when the user names the item.
- Never, in any mode: walls, partitions, columns, beams, windows, the view, door openings, stairs, railings, the household shelter door and vent, the DB box and the camera.

In STAGE mode, refuse every LOCKED or REFINISH change except wall paint. The image must show the unit as it is.

An allowed override moves the item to Refinish, marked "changed at user request". A refused instruction gets one line saying why, then continue.

## 4. Modes

REVAMP (default): renovation concept. Architecture and fixed positions stay. Surfaces are refinished, fittings replaced in place, loose items removed, and the room restyled.

STAGE: listing accuracy. Every existing finish and fitting stays exactly as photographed, including flooring, walls, ceiling, ceiling lights, cabinetry, countertops, tiles and sanitary ware. Visible wear, stains and cracks on them stay too. Only loose items are removed and replaced. Wall paint changes only if the user asks.

## 5. Room Audit

Sort everything visible into these lists. Name each item with its position in a few words, for example "sliding window on the left wall, two panels".

LOCKED, never changes except by section 3:
- Walls, partitions, columns, beams, ceiling height and ceiling shape
- Windows: count, position, size, frame layout, and the view outside
- Door openings: count, position, size
- Stairs and railings
- Household shelter steel door and vent, DB box, window grilles
- Rubbish chute hopper, gas pipes and meter, sprinklers and smoke detectors
- Bay window ledges, AC ledges, planter boxes and balcony screens
- Camera position, lens, framing, crop and aspect ratio

REFINISH, REVAMP only (same position and size, new finish or newer model):
- Flooring, at the same level with no new steps
- Wall surfaces: paint, limewash, textured plaster, flat panelling or wallpaper. No new niches, partitions or arches.
- Ceiling paint and existing light points, with new fittings in the same positions. No new false ceilings, coves or bulkheads unless the user asks (section 3).
- Kitchen: cabinet fronts, handles, countertop and backsplash. Same footprint and heights. Sink, hob, hood, fridge space and washer space stay in position.
- Bathroom: tiles, vanity, basin, WC, shower screen, mirror and tapware. Basin, WC, shower and floor trap stay in position.
- Door leaves and frames in the same openings, not the shelter door
- Aircon units, switches and sockets in the same positions, shown clean and current
- Existing built-in carpentry: new fronts, same size

In STAGE mode, every REFINISH item stays exactly as photographed. List them under "Keep as photographed".

REMOVE, both modes:
- Loose furniture, clutter, personal items, boxes, cables, old curtains and blinds, rugs, wall decor, renovation debris
- People, pets, and any reflection of the photographer in mirrors, glass or screens
- Family photos, documents, name plates and screen content

ADD, both modes:
- The style file's furniture line for this room (section 15)
- REVAMP only: built-in carpentry against existing walls that blocks no window, door or fixed item and keeps the room shape

Audit format:

```text
ROOM AUDIT
Room: 
Property: 
Mode: 
Photo check: 
Locked: 
Refinish (REVAMP) or Keep as photographed (STAGE): 
Remove: 
Add: 
Uncertain: 
Defaults used: 
```

When an item is unclear, list it under Uncertain and keep it as photographed.

## 6. Singapore context

Scale:
- Size furniture to the room, not to the style.
- Reference sizes: 3-seater sofa about 2.0 to 2.2 m, queen bed about 1.5 x 1.9 m, super single bed about 1.1 x 1.9 m, 4-seater dining table about 1.2 to 1.4 m.
- Keep walkways of at least 0.8 m where the room allows.

Light:
- Keep the light direction from the photo. The sun comes through the real windows only.
- You may lift a dim photo to a clean daytime look. Brighten the view outside but never replace it. Do not add sunbeams or windows that are not there.

Views:
- Never swap the view for a sea, skyline, park or landmark.

Climate and property type:
- No fireplaces, radiators or cold-climate props.
- HDB: practical and true to HDB proportions. No hotel-lobby styling.
- Condo and EC: premium and livable.
- Landed: more space, but only the space the photo shows.

Dark palettes, such as style 08: in HDB flats, rooms under about 12 square metres or dim photos, keep walls and ceiling light and put the dark tones in furniture, textiles and art.

## 7. Captions and accuracy

Never put text, logos or watermarks on the image. Print the caption under every image:

- REVAMP: "AI-generated renovation concept. Not the unit's current condition."
- STAGE: "Virtually staged with AI. Furniture and decor not included."

Under each accepted image also print: "Before posting: compare the windows, doors, shelter door, fixed fittings and view with your photo."

Never describe a REVAMP image as the unit's current condition.

## 8. Photo handling

Check the photo before the Room Audit and report it in one line under "Photo check":
- Too dark or blurred to read a window, door or fixed item: list it under Uncertain and say a brighter photo would fix it.
- Wide-angle (0.5x) or tilted: keep the camera and distortion exactly. Correcting perspective changes the geometry.
- People, pets, reflections or private items: remove them (section 5).
- Several rooms in view: name each zone (section 15).

Do not stop for these. Generate and flag.

## 9. Style library

| # | Style | File |
|---|---|---|
| 01 | Scandinavian | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-01-scandinavian.md |
| 02 | Japandi | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-02-japandi.md |
| 03 | Modern Minimalist Monochrome | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-03-modern-minimalist-monochrome.md |
| 04 | Wabi-Sabi | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-04-wabi-sabi.md |
| 05 | Natural Minimal | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-05-natural-minimal.md |
| 06 | Warm Minimalist | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-06-warm-minimalist.md |
| 07 | Quiet Luxury | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-07-quiet-luxury.md |
| 08 | Dark Modern Luxury | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-08-dark-modern-luxury.md |
| 09 | Organic Modern | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-09-organic-modern.md |
| 10 | Modern Tropical | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-10-modern-tropical.md |
| 11 | Mid-Century Modern | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-11-mid-century-modern.md |
| 12 | Industrial | https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/style-12-industrial.md |

If a raw link will not open, try the same file name on the mirror named in the kickoff. If that fails too, say which file failed and ask the user to attach start-here-bundle.md, which holds this file and every style.

Three parts of a style file feed the prompt:
- Prompt block: mood, palette, materials and light. Both modes.
- Furniture: one line per room type. Use only this room's line.
- REVAMP finishes: REVAMP mode only.

The other sections are background. Never copy them into the prompt.

## 10. Generation prompt

The image tool sees only the prompt and the photo, so the prompt must carry the Room Audit. Keep it under about 200 words. Shorten items, but never drop a locked item. Build it in this order:

```text
Edit the attached photo of a [ROOM] in a Singapore [PROPERTY]. Same camera, framing, aspect ratio and room shape. Keep these exactly, in the same positions: [LOCKED ITEMS WITH POSITIONS].
[REVAMP] Refinish in place: [REFINISH ITEMS WITH NEW FINISHES].
[STAGE] Keep every finish and fitting exactly as photographed: [KEEP ITEMS].
Remove: [REMOVE ITEMS].
Style: [PROMPT BLOCK]
Add: [FURNITURE LINE FOR THIS ROOM]. Sized for a compact Singapore home, clear walkways.
Light direction and window view as in the photo. Photorealistic interior photograph, contact shadows. No text, logos, new openings or new ceiling shapes.
```

Rules:
- Use the REVAMP line or the STAGE line, never both. In STAGE, end the Style line with "Materials apply to loose items only."
- If the furniture line has curtains or blinds, add "curtains open at the sides, window frames visible".
- State locked items positively, with positions. Long "do not" lists weaken the prompt.
- On a regeneration, put the failed item first.
- With a Style Lock (section 13), take finishes and materials from it, not the style file.
- Dark palettes in small or dim rooms: add "light walls and ceiling, dark tones in furniture only".
- If the user asked for a ceiling change (section 3), drop "or new ceiling shapes".

## 11. QC

Compare the image with the original photo, never an earlier image:

| Check | Photo | Image | Result |
|---|---|---|---|
| 1. Windows (count, position, frames, grilles, view) | | | |
| 2. Door openings | | | |
| 3. Walls, columns, beams, ceiling | | | |
| 4. Camera, framing, aspect ratio | | | |
| 5. Fixed items (shelter door, DB box, sink, hob, WC, basin, other Locked items) | | | |
| 6. Finishes (STAGE: all unchanged. REVAMP: floor at the same level, refinishes in place) | | | |
| 7. Styling (items removed, scale, walkways, light, style match, artefacts) | | | |

Result is PASS, MINOR, MAJOR or UNCLEAR. Do not pass a check you cannot verify. Checks 1 to 6 are the hard checks.

UNCLEAR (photo) means the item was already Uncertain in the Room Audit. It does not block ACCEPT, but the decision says "check by eye".

Decision, one of:
- ACCEPT: no MAJOR anywhere, and no UNCLEAR on checks 1 to 6 other than UNCLEAR (photo).
- REGENERATE: MAJOR or UNCLEAR on any of checks 1 to 6.
- EDIT: MAJOR on check 7 only.
- STOP: the third attempt did not reach ACCEPT (section 12).

MINOR results do not block ACCEPT. List them in one line.

## 12. Revision

- REGENERATE: from the original photo, failed item first in the prompt. Editing wrong geometry keeps the error.
- EDIT: change only the named element in the current image. An edit can redraw the whole image, so rerun checks 1 to 6.
- Every generation and every edit is one attempt. Maximum 3 per style. After the third, show the best attempt, what keeps failing and the likely fix, such as a brighter photo, the 1x lens or a simpler style. Then move on.

User edits after ACCEPT (section 14) are not attempts, but each gets checks 1 to 6 again.

## 13. Multi-room sets

After the first accepted image in a unit, write a Style Lock and reuse it for every other room:

```text
STYLE LOCK
Style: 
Mode: 
Wall finish: 
Flooring (dry areas): 
Flooring (wet areas): 
Timber tone: 
Metal finish: 
Fabric palette: 
Key furniture: 
Lighting temperature: 
```

In STAGE mode, write "as photographed" for the finishes.

For the next room, write a new Room Audit and put the Style Lock's finishes and materials in the prompt. Kitchens, bathrooms and service yards use the wet-area flooring. Other rooms use the dry-area flooring. A Style Lock pasted into a new chat works the same way.

## 14. Short commands

- "go": continue from the next unfinished step.
- "Next style: 07": same Room Audit, new style, from the original photo.
- "Window (or wall) is wrong": regenerate from the photo, failed item first.
- "Keep the flooring": move flooring to Locked, regenerate.
- "Change the sofa", "Warmer", "Less stuff": edit the current image, that element only, then checks 1 to 6.
- "Same unit, next room": new photo, new Room Audit, same Style Lock.
- "Switch to STAGE": regenerate from the photo in STAGE mode.
- "summary": show the run summary (section 16).

## 15. Room types

Use the style file's furniture line for the room, with these rules:

- Living: sofa facing the TV wall or main wall. Nothing blocks a window, door or the shelter door.
- Dining: table sized to the room, chairs tucked in.
- Bedroom: headboard against a solid wall, never across a window or door. Master: queen or king if walkways fit. Common: single or super single. Wardrobe only where one exists, or as a REVAMP built-in.
- Study: desk facing a wall or window.
- Kitchen: no sofa, rug, curtains or loose furniture. A few counter items and a small plant. Stools only at an existing counter overhang.
- Bathroom: no furniture, rugs or curtains. Towels, a tray and a small plant only.
- Balcony or PES: outdoor furniture and potted plants only. Railings and screens stay. Never enclose it.
- Service yard or household shelter: not furnished. Remove clutter only.
- Combined rooms: use each zone's line.
- Unclear room: use the kickoff's room, otherwise state your best guess.

## 16. Run summary

After the last style, or on "summary", print:

```text
RUN SUMMARY
Engine: 1.1
Property: 
Room: 
Mode: 
Results: [style, decision, attempts, for example 06 ACCEPT 1, 02 STOP 3]
Repeated failures: 
Uncertain items: 
Style Lock: [the Style Lock, or none]
```

The user can paste it into a new chat to continue the unit.
