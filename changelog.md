# 8-22-2026:
## Lectio Continua — Print Layout Cleanup
**Added**
- New **Completed Date** fill-in line on the front-matter card, alongside a renamed **Start Date** (previously "Started on"), sitting side by side under one rule.

**Changed**
- Printed plan no longer includes the "Choose Your Pace" section (heading, intro copy, canon/multiplier controls) — screen view unaffected.
- Printed plan no longer includes the "One Year, Your Pace" heading or the "This plan completes on Day X" line, now redundant with Completed Date.
- Front-matter print card trimmed to **title, Start Date, and Completed Date only**; the chapters-per-track breakdown (Canon, History, Psalms, Wisdom, Prophets, New Testament) stays visible on screen but is hidden in print.
- Front-matter title and subtitle sized down for print (screen view unchanged).
- Day column in the printed table now matches the reading cells — same font, weight, size, and color — instead of standing out in bold Playfair Display. Header row stays bold as the per-page anchor.
- Canon toggle buttons relabeled from "Catholic — 73 Books" / "Protestant — 66 Books" to **73 Book** / **66 Book**; front-matter's screen-only Canon field updated to match.

**Fixed**
- Table rows splitting across page breaks mid-checklist. Root cause was `border-collapse: collapse` silently defeating `page-break-inside: avoid` in Chrome/WebKit. Switched print table to `border-collapse: separate` and added the modern `break-inside: avoid` alongside the legacy property.

**Unchanged**
- Reading-plan generation logic, chapter-count data, and the synchronize toggle behavior — this pass was print/display only.
  
---

# 8-16-2026:

## Lectio Continua — Five-Track Overhaul

**Added**
- Split the single "Old Testament" track into two: **History**, **Prophets**, **Psalms**, and **Wisdom**. 
- New **Synchronize** option (checked by default) that makes all five tracks — History, Psalms, Wisdom, Prophets, New Testament — finish on the same day. Day 1 and the final day always carry a reading from every track; shorter tracks pick up occasional off days as they stretch to match the longest one.
- Plan output now shows a single "This plan completes on Day X" line reflecting whichever track naturally runs longest.

**Changed**
- Reading-plan controls reorganized: History, Wisdom, and Prophets are grouped together, with Psalms and New Testament below.
- Front-matter print card now lists chapters/day per track instead of completion dates, keeping the printed card focused on daily pace rather than a moving target.
- Intro copy updated to describe all five tracks and the new sync behavior.
- Plan table gained a Prophets column (7 columns total including checkbox and day).

**Unchanged**
- Whole-chapter ceiling-division pacing logic (the mechanism, not just default) — when synchronize is turned off, tracks still run at a fixed pace and go quiet with an em dash once done, exactly as before.
- Catholic (73-book) / Protestant (66-book) canon toggle and all chapter-count data.

---

# 8-15-2026:

## Lectio Continua: reading streams now stop instead of looping

Previously, each stream (Old Testament, Psalms, Wisdom, New Testament) wrapped back to the start once it reached the end of its book list, regardless of the multiplier setting. This caused two problems: a stream would often hit day 365 mid-cycle, cutting off in the middle of a book, and the multiplier itself was being ignored for completion purposes, a stream would finish after a single pass through its books no matter how high the multiplier was set (a 6x New Testament setting was completing in 52 days instead of running six full read-throughs across the year).

Clarified language throughout describing a 365 day plan.  It will often be the case that you complete the read-through before 365 days have passed.  This plan is then one that will result in completion of your plan within a 365 day time box but not necessarily take the entire year to complete.

**What changed:**

- Each stream now calculates its full target as total chapters × multiplier (e.g., New Testament at 6x = 260 chapters × 6 = 1,560 chapters to read across the year).
- The stream wraps through its book list as many times as needed to hit that target, cycling back to the first book each time it finishes a pass, then stops permanently once the target is reached.
- Once a stream is done, its column shows an em dash for every day after that, rather than restarting or leaving a blank cell.
- Once every stream has reached its target (all four columns would show em dashes), the table stops rendering rows entirely. If the last stream to finish completes on Day 268, the table ends at Day 268, no trailing rows of em dashes.
- The front matter summary for each stream now reads as "X ch/day, complete by Day Y (Nx)" instead of the old "actual vs. target" percentage, since the stream always hits its multiplier target exactly now.
- Also folded into this update: Ecclesiastes and Song of Solomon moved out of the Old Testament stream and into a new "Wisdom" stream alongside Proverbs (and, for the Catholic canon, Wisdom and Sirach). Job stays in the Old Testament stream. All four multiplier fields now default to 1x rather than the old 3/3/12/6 defaults.

**Net result:** any combination of multipliers across the four streams will fit within 365 days, always in whole chapters, and the reader sees exactly as many rows as there are active readings, nothing more.
