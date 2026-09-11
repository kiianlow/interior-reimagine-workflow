# Interior Reimagine Workflow: START HERE

Version 1.0

Read this whole file before generating any image. It is the complete engine. Then open only the style file(s) the user picks. If any other file conflicts with this one, this file wins.

## 1. What this does

Turns a photo of a real room (empty, old or furnished) into a photorealistic furnished version in the chosen style.

Core rule: same room, same camera, same fixed positions. New finishes, furniture and styling.

## 2. Run sequence

The user sends a room photo plus a short kickoff (room, style numbers, mode). If the photo and at least one style are present, do not ask questions. Use the defaults in section 3 and list which ones you used.

1. Read the photo.
2. Open the selected style file(s) from section 9.
3. Write the Room Audit (section 5) and show it in the chat.
4. Build the prompt for the first style (section 10). Generate using the photo as the base image.
5. Run QC (section 11) and show the table.
6. Revise if needed (section 12).
7. Move to the next requested style without asking. Reuse the same Room Audit.
8. After the last image, give the caption line for the mode (section 7).

Chat output: Room Audit once, then for each style the image, the QC table and the decision. Keep text short.

## 3. Inputs and defaults

| Input | Default if missing |
|---|---|
| Room photo | Required. Stop and ask for it. |
| Style number(s) | Required. Stop and ask for it. |
| Room type | Infer from the photo and state it |
| Mode | REVAMP |
| Property type | Infer from visible cues, otherwise "Singapore apartment" |
| Time of day | Match the photo |
| Format | Same aspect ratio as the photo |
| Extra keep or change instructions | None |

User keep and change instructions override the defaults in section 5, except the LOCKED list. LOCKED items change only when the user names the item and says to change it.

## 4. Modes

REVAMP (default): renovation concept. Architecture and fixed positions stay. Surfaces are refinished, fittings are replaced in the same positions, all loose items are removed, and the room is fully restyled.

STAGE: listing accuracy. Every existing finish and fitting stays exactly as photographed, including flooring, walls, cabinetry, sanitary ware and ceiling lights. Only loose items are removed and replaced. Wall paint changes only if the user asks.

## 5. Room Audit

Before generating, sort everything visible in the photo into these lists. Name each item with its position, for example "sliding window on the left wall, two panels".

LOCKED, never changes in any mode:
- Walls, partitions, columns, beams, ceiling height and ceiling shape
- Windows: count, position, size, frame layout, and the view outside
- Door openings: count, position, size
- Stairs and railings
- Household shelter steel door and vent, DB box, window grilles
- Camera position, lens, framing and crop

REFINISH, REVAMP only (same position and size, new finish or newer model):
- Flooring, at the same level with no new steps
- Wall surfaces: paint, limewash, textured plaster, flat panelling or wallpaper. No new niches, partitions or arches.
- Ceiling paint and existing light points (new fittings in the same positions). No new false ceilings or bulkheads unless the user asks.
- Kitchen: cabinet fronts, handles, countertop and backsplash. Same footprint and heights. Sink and hob stay in position.
- Bathroom: tiles, vanity, basin, WC, shower screen and tapware. All in the same positions.
- Door leaves and frames in the same openings (not the shelter door)
- Aircon indoor units and switches in the same positions, shown clean and current

In STAGE mode, every REFINISH item stays exactly as photographed.

REMOVE, both modes:
- Loose furniture, clutter, personal items, boxes, cables, old curtains and blinds, rugs, wall decor, renovation debris

ADD, both modes:
- Furniture, rugs, curtains or blinds, lamps, art, plants and decor from the style file
- REVAMP only: built-in carpentry against existing walls (wardrobes, TV console, shelving) that does not block windows, doors or fixed items and does not change the room shape

Audit format:

```text
ROOM AUDIT
Room: 
Property: 
Mode: 
Locked: 
Refinish: 
Remove: 
Add: 
Uncertain: 
```

When an item is unclear, list it under Uncertain and keep it as photographed.

## 6. Singapore context

Scale:
- Size furniture to the room, not to the style.
- Reference sizes: 3-seater sofa about 2.0 to 2.2 m, queen bed about 1.5 x 1.9 m, 4-seater dining table about 1.2 to 1.4 m.
- Keep walkways of at least 0.8 m where the room allows.

Light:
- Keep the light direction from the photo. The sun comes through the real windows only.
- You may lift a dim photo to a clean daytime look. Do not add sunbeams or windows that are not there.

Views:
- Keep the exact view through the windows. Never swap in a sea, skyline, park or landmark.

Climate and property type:
- No fireplaces, radiators or cold-climate props.
- HDB: practical and true to HDB proportions. No hotel-lobby styling.
- Condo and EC: premium and livable.
- Landed: more space, but only the space the photo shows.

## 7. Captions and accuracy

Never put text, logos or watermarks on the image. After the last image, give the caption line:

- REVAMP: "Renovation concept for illustration. Not the unit's current condition."
- STAGE: "Virtually staged for illustration."

## 8. Photo handling

- Keep the camera exactly as photographed, even if the photo is tilted or wide-angle. Correcting perspective changes the geometry.
- If the photo is too dark or blurred to read a locked item, list it under Uncertain and keep it as photographed.

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

If a raw link will not open, use the matching file at https://github.com/kiianlow/interior-reimagine-workflow and say which one you used.

Each style file starts with a Prompt block. Use it in the generation prompt. Use the REVAMP finish sections only in REVAMP mode. In STAGE mode, drop any wall, flooring or cabinetry wording from the Prompt block unless the user asked for a paint change. If the user names a style that is not in the library, use the closest one and say which.

## 10. Generation prompt

The image tool only sees the prompt and the photo. It does not see this repo, so the prompt must carry the Room Audit. Keep it under about 200 words and build it in this order:

```text
Edit the attached photo of a [ROOM] in a Singapore [PROPERTY]. Keep the camera, framing, room shape and these elements identical and in the same positions: [LOCKED ITEMS WITH POSITIONS].
Remove: [REMOVE ITEMS].
[REVAMP ONLY] Refinish in the same positions: [REFINISH ITEMS WITH THE NEW FINISHES FROM THE STYLE FILE].
Furnish in [STYLE NAME] style: [PROMPT BLOCK]. Furniture sized for a Singapore home, clear walkways.
Keep the light direction and the view through the windows as in the photo.
Photorealistic real estate interior photography, natural materials, contact shadows.
No text, logos or watermarks. No new windows, doors, openings or ceiling changes.
```

State locked items positively, with positions. Long "do not" lists weaken the prompt.

## 11. QC

Compare the image with the original photo and fill this table:

| Check | Photo | Image | Result |
|---|---|---|---|
| Windows (count, position, frames, view) | | | |
| Door openings | | | |
| Walls, columns, beams, ceiling | | | |
| Camera and framing | | | |
| Fixed items (shelter door, DB box, grilles, sink, hob, WC, basin) | | | |
| Flooring (STAGE: unchanged. REVAMP: same level) | | | |
| Removed items gone | | | |
| Furniture scale and walkways | | | |
| Light direction | | | |
| Style match | | | |
| Artefacts (warped lines, floating or duplicate objects, text) | | | |

Result is PASS, MINOR, MAJOR or UNCLEAR. Do not pass a check you cannot verify.

Decision: ACCEPT only when there is no MAJOR and no UNCLEAR on windows, door openings, walls or camera.

## 12. Revision

- MAJOR on a locked item or the camera: regenerate from the original photo, naming the failed item in the prompt. Editing an image with wrong geometry keeps the error.
- MINOR or styling issues: edit the current image and change only the named element.
- Maximum 3 attempts per image. After the third, stop and report what keeps failing and the likely fix, such as a clearer photo or a simpler style.

## 13. Multi-room sets

After the first accepted image in a unit, write a Style Lock and reuse it for every other room in the same unit:

```text
STYLE LOCK
Style: 
Wall finish: 
Flooring: 
Timber tone: 
Metal finish: 
Fabric palette: 
Key furniture: 
Lighting temperature: 
```

Flooring and wall finish stay the same across rooms unless the user says otherwise.

## 14. Short commands

| User says | Action |
|---|---|
| Next style: 07 | Same photo, same Room Audit, new style |
| Window or wall is wrong | Regenerate from the photo, name the item |
| Keep the flooring | Move flooring to LOCKED, regenerate |
| Change the sofa or rug | Edit the current image, that item only |
| Warmer or brighter | Edit the current image, lighting only |
| Less stuff | Edit the current image, remove decor |
| Same unit, next room | Reuse the Style Lock, new Room Audit |
| Switch to STAGE | Regenerate from the photo in STAGE mode |
