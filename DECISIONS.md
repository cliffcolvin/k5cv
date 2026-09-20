# DECISIONS

Running log of intent and decisions for the k5cv site. Newest first.

## 2026-09-20 — Pulled "Who Signs for the Machine?" back to draft

**Decision:** `content/posts/AI-ML/who-signs-for-the-machine.md` set to
`draft = true` one day after publishing, on Cliff's instruction. The file stays
in the repo unchanged otherwise, ready for revision.

**Consequence handled:** the live responsibility-gap post carried a parenthetical
link to the CPCO post (a sentence added during conversion, not part of Cliff's
paper). Removed it so the live post does not point at a 404. Restore the
sentence when the CPCO post republishes. The CPCO post's own link to the
responsibility-gap post is untouched; it only matters once that post is live
again.

**Consequences not handled:** the URL was live for about a day. Search engines
and RSS readers may hold a cached copy until they recrawl; nothing on the site
side can shorten that.

## 2026-09-19 — Added "The Responsibility Gap in Enterprise AI" as a draft

**Decision:** New post `content/posts/AI-ML/the-responsibility-gap-in-enterprise-ai.md`,
a near-verbatim conversion of Cliff's paper of the same name (PDF now kept at
`Atlas/Writing/Paper - The Responsibility Gap in Enterprise AI.pdf` in the vault).
`draft = true`; Cliff flips it.

**Why:** Cliff asked for the paper as a separate k5cv post and for a hard check
that neither thought-leadership piece carries anything IBM-specific. The paper's
own text is the deliverable, so the conversion changed as little as possible.

**What changed from the paper:** (1) "My boss, Lino, and I" became "My boss and
I": no colleague names in public posts. (2) One parenthetical cross-link added at
the FinOps-for-AI paragraph pointing to "Who Signs for the Machine?", and that
post now links back here and summarizes this frame (accountability stays human,
operational responsibility can move to the machine) instead of citing outside
philosophy. (3) Markdown structure only: TOML front matter, the deck line as the
italic subtitle, `##` headers, a blockquote for the 1979 quote, bullets for the
leader questions, straight quotes. Every sentence of the paper is otherwise
present, verified by a sentence-level diff against the PDF text.
(4) Later the same day, on Cliff's direction: the three-reasons passage in
section 2 was expanded rather than reordered. It now states that the list runs
from easiest to see to most important, adds a Girard beat to the incentives
reason (same objective function pointed at the same scarce object; the deepest
reason is the hardest to see because nobody experiences their own desire as
borrowed; incentive conflicts arrive dressed as misunderstandings), and extends
the machine paragraph with the flip: a machine's objective is written down, so
"which objective did this action serve, and who owns it" can be a field in the
record. Reordering incentives to first was considered and rejected because the
list climbs into the "agents inherit... contradictions" paragraph, and that
handoff depends on incentives landing last. (5) An italic postscript asks
readers what he is missing, in his words ("I am certain this is not the whole
picture... where I am concentrated most right now"), and names X and GitHub as
reply channels because the site has no comment system.

**Kept on purpose, per Cliff:** the 1979 IBM training-manual quote and his
original link to IBM's public article on it. It is public, and it is the hinge
for "FinOps decisions are management decisions."

**Consequences:** Both posts pass a grep for internal names, products, customers,
and meeting content; the only "IBM" occurrences are the 1979 quote and its two
follow-on sentences. Not build-verified locally (no Hugo). Both posts carry the
same date.

**Published 2026-09-19 (later the same morning), on Cliff's instruction:** both
posts flipped to `draft = false`, cross-links changed from site-relative paths to
absolute `https://k5cv.com/posts/ai-ml/...` URLs, and the CPCO post's closing
softened from "I'd love to be shown someone who's further along" (read as a
challenge) to an invitation for feedback in Cliff's words. Commits `b7129c3` and
`e5f53d7`, pushed to `main`. The push had to go over SSH
(`git@github.com:cliffcolvin/k5cv.git`): `origin` is HTTPS and the `gh` keyring
token is invalid, so `git push origin main` fails until `gh auth refresh` or the
remote is switched to SSH. Remote left as-is.

## 2026-09-19 — Added "Who Signs for the Machine?" as a draft

**Decision:** New post `content/posts/AI-ML/who-signs-for-the-machine.md`, the
public rewrite of the vault draft "GPU Efficiency - Cost per Correct Outcome".
Committed with `draft = true`; Cliff flips it when he has read it.

**Why:** Cliff asked for a public-consumption version that keeps his voice and
story-first structure, and that positions him as a thought leader on cost per
correct outcome without reading as a break from his employer's direction on
tokenomics. The rewrite therefore treats tokenomics as the necessary
visibility layer (the FinOps "Inform" phase) and stacks the new vocabulary on
top of it rather than against it.

**What changed from the vault draft:** the five GPU "taxes" and the
saturation-versus-utilization material were cut (they are flagged in the post
as a separate future post; the paper in the vault still holds them). Kept: the
47x-versus-4x spread and the "spraying plausible values" finding, both already
sanitized. Added: the successful/correct distinction (CPSO and CPCO as two
columns of one ledger), the three-part contract, the five first-principle
quantities, the execution/delegation vocabulary, the autonomy rule for pulling
a human in, the FinOps ROI framing, and the responsibility-gap section.

**Consequences:** No employer, product, customer, or colleague is named; "I
work in FinOps" and "I lead a team of engineers" are the only work references,
both already public on the site. Not build-verified locally; Hugo is still not
installed on this machine, and the post uses only Markdown features the
existing AI-ML posts already use (TOML front matter, headers, bold, a fenced
code block).

## 2026-08-05 — Added the Faith category

**Decision:** New category `content/posts/Faith/`, opened with "At Peace in the
Storm" (Mark 4, written the day of a family member's surgery). Published live.

**Why:** Cliff asked for it by name. It is the first explicitly religious writing
on the site; the reflective essays that touch on his higher power have lived in
`Random` until now, and this gives that material a home.

**Consequences:** The post names two living relatives and one of their medical
situations. That was raised with Cliff before publishing, including the point that
the quoted relative answered a personal question rather than giving a quote for
publication, and he chose to publish as written. Noting it here because the
`k5cv-family-audience` rule would otherwise read as though the case was missed.

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
