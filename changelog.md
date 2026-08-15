8-15-2026:

**Lectio Continua: reading streams now stop instead of looping**

Previously, each stream (Old Testament, Psalms, Wisdom, New Testament) wrapped back to the start once it reached the end of its book list, regardless of the multiplier setting. This caused two problems: a stream would often hit day 365 mid-cycle, cutting off in the middle of a book, and the multiplier itself was being ignored for completion purposes, a stream would finish after a single pass through its books no matter how high the multiplier was set (a 6x New Testament setting was completing in 52 days instead of running six full read-throughs across the year).

**What changed:**

- Each stream now calculates its full target as total chapters × multiplier (e.g., New Testament at 6x = 260 chapters × 6 = 1,560 chapters to read across the year).
- The stream wraps through its book list as many times as needed to hit that target, cycling back to the first book each time it finishes a pass, then stops permanently once the target is reached.
- Once a stream is done, its column shows an em dash for every day after that, rather than restarting or leaving a blank cell.
- Once every stream has reached its target (all four columns would show em dashes), the table stops rendering rows entirely. If the last stream to finish completes on Day 268, the table ends at Day 268, no trailing rows of em dashes.
- The front matter summary for each stream now reads as "X ch/day, complete by Day Y (Nx)" instead of the old "actual vs. target" percentage, since the stream always hits its multiplier target exactly now.
- Also folded into this update: Ecclesiastes and Song of Solomon moved out of the Old Testament stream and into a new "Wisdom" stream alongside Proverbs (and, for the Catholic canon, Wisdom and Sirach). Job stays in the Old Testament stream. All four multiplier fields now default to 1x rather than the old 3/3/12/6 defaults.

**Net result:** any combination of multipliers across the four streams will fit within 365 days, always in whole chapters, and the reader sees exactly as many rows as there are active readings, nothing more.
