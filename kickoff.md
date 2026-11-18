# Kickoff Prompts

Attach the room photo to a new ChatGPT chat, then paste one of these.

## Full

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

## Quick

```text
Source of truth: https://raw.githubusercontent.com/kiianlow/interior-reimagine-workflow/main/START-HERE.md
Mirror if that fails: https://cdn.jsdelivr.net/gh/kiianlow/interior-reimagine-workflow@main/START-HERE.md
Start your reply with its version line. Living room. Styles: 06. REVAMP.
```

## Offline fallback

If neither link opens, attach `start-here-bundle.md` with the photo and paste:

```text
Source of truth: the attached start-here-bundle.md. It holds the engine and every style. Do not fetch any links.
Start your reply with its version line.

Room: 
Styles: 
Mode: 
Property: 
```

## Follow-ups in the same chat

```text
go
```

```text
Next style: 07
```

```text
Same unit, same Style Lock. Next room: master bedroom. [attach photo]
```

```text
Switch to STAGE and keep the existing flooring and cabinets.
```

```text
summary
```

## Next room in a new chat

Paste the Full kickoff, then add the last run summary's Style Lock:

```text
Style Lock: [paste the STYLE LOCK block]
```

## Style numbers

01 Scandinavian, 02 Japandi, 03 Modern Minimalist Monochrome, 04 Wabi-Sabi, 05 Natural Minimal, 06 Warm Minimalist, 07 Quiet Luxury, 08 Dark Modern Luxury, 09 Organic Modern, 10 Modern Tropical, 11 Mid-Century Modern, 12 Industrial
