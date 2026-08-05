# DECISIONS

Running log of intent and decisions for the k5cv site. Newest first.

## 2026-08-05 — Edited live posts for a family audience

**Decision:** Made targeted edits to four posts ahead of Cliff sharing the site
with family. Changes:

- `2025-year-in-review.md`: removed his daughter's name, age, and the "eight
  hours away" distance (a named minor plus location on a public site, and the
  detail also implied the split-household arrangement); replaced the specifics of
  his mother's Alzheimer's diagnosis and memory loss with "a hard season with my
  mom's health"; changed the puppy's description from `"asshole"` to "menace".
- `validation.md`: "My therapist recently asked me" became "I was recently asked"
  (mental-health disclosure); "if I got laid off tomorrow" became "if the work
  simply went away tomorrow" (reads as personal job anxiety at a named employer);
  rewrote the line about his wife never willingly reading his essays, which could
  scan as a dig at her.
- `buffalo-wings-for-king-thamus.md`: warmed the crossword anecdote about his
  mother. The punchline was that she wasn't really listening, which lands
  differently on a site that also discloses her health.
- `conscious-living-and-joy.md`: em dashes replaced per Cliff's standing writing
  rule.

**Why:** The filter applied was Cliff's own framing, "drama and anxieties," plus
third-party privacy. Not all personal detail.

**Deliberately left alone:** the weight-loss numbers, the finances, Rascal's
death, Taryn's name, the family photos, and the IBM/Kubecost mentions. Those are
personal but not drama, and several are things he's proud of. Cutting them would
have gutted the year in review rather than cleaned it.

**Consequences:** Every edit is a softening, not a deletion, so each post still
makes its original argument. Prior wording remains in git history and possibly in
search-engine caches.

## 2026-08-05 — Removed the electrical theory series and its Electrical category

**Decision:** Deleted all three electrical-engineering posts, the `Electrical/`
category (including its `_index.md`), and the nine diagram images the series
used. Removed:

- `content/posts/Electrical/shockingly-common-sense.md`
- `content/posts/Electrical/beyond-not-dying.md`
- `content/posts/Random/a-shocking-holiday.md`
- `static/`: `ohms-law.jpg`, `American-Wire-Gauge-AWG-Chart-.jpg`, `circuit.jpg`,
  `switchmiswire.png`, `zap.png`, `kcl.jpeg`, `kvl.jpeg`, `series.png`,
  `parallel.png`

**Why:** Cliff is about to publish a post he'll share with family, so the site
needed to read as a personal blog for that audience rather than a mixed personal
/ engineering-tutorial site. The EE series was the largest off-tone block.

**Note on scope:** `a-shocking-holiday.md` lived under `Random/`, not
`Electrical/`, but it was part 1 of the same three-part series (the other two
reference it by number). Removing the folder alone would have orphaned a series
opener whose sequels no longer existed. Cliff confirmed including it.

**Alternatives:** Setting `draft = true` instead of deleting was offered and
rejected in favor of a full delete plus images. Git history preserves everything
if the series is ever revived.

**Consequences:**

- The `Electrical` category disappears from the homepage post table and the
  category listing. `Ham/` remains as a pre-existing empty category (it had no
  posts before this change either).
- Verified before deleting: those nine images were referenced only by the three
  removed posts, and no remaining content links to the electrical posts. No
  dangling references.
- Not build-verified locally; Hugo isn't installed on this machine. The change is
  deletions with no remaining references, and the GitHub Actions workflow builds
  from source on push, so tracked `public/` build output being stale does not
  affect the deployed site.
- The removed posts stay reachable via git history and may persist in search
  engine caches and archive.org for some time.
