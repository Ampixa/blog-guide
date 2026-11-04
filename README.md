# Writing for ampixa.com/blog

The house guide for anyone writing for the Ampixa Labs blog, people and agents alike. It says how to write
a post so it is worth reading. Drafts are submitted for review; nobody publishes directly. The reference post is
[Yak](https://ampixa.com/blog/yak-an-open-lossless-nepali-first-tokenizer/): when in doubt, look at what it does.

Rule of thumb: **a reader who only looks at the title, the TL;DR, the figures and the captions should
leave with the whole result.** Prose explains; it does not carry the result alone.

## 1. Before you write

- Have the artifact first. For a release that is the repo, model card or dataset. For an experiment or a
  lesson, the post itself can be the artifact: the method, the full code that produced every number, and
  that code's raw output, all in the post. Do not create a separate repo or gist just to have a link.
  No artifact of either kind, no post: save it as an idea until there is one.
- Know your one-sentence result. If you cannot say it with a number in it, you are not ready.
- Check the claim survived a control. A number with no baseline or random control is an anecdote.

## 2. Structure (in this order)

1. **Front matter** (section 6). Header links, glyph, summary, social image.
2. **TL;DR** paragraph starting `**TL;DR.**`: the result, the 2–3 key numbers in bold, and the main limit.
3. **Hero image** with one italic caption line.
4. **A hook the reader can feel**: one concrete example before any method. Yak shows a Nepali sentence
   cut into 17 tokens vs 5. Show the thing, then explain it.
5. **Sections as questions** (`## How many tokens does Nepali cost?`). Each section answers one question,
   opens with the answer, then shows the evidence (figure or table), then the caveat.
6. **How it was built / measured**: short, with the one messy detail that proves it is real.
7. **What this is not**: bullets. Every limit you know about. This section is mandatory.
8. **Where this sits**: prior work, linked.
9. **Reproduce / Get it**: code that actually runs, then links, licence. In a self-contained post, print
   the whole script in a collapsible `<details>` block with its raw output underneath, and run that exact
   script end to end before submitting.

Length follows the result: a release can be 14 minutes, a lesson 4–6. A 2-minute wall of prose with no
figure is never right.

## 3. Do

- **Links are links.** `[Petrov et al. (2023)](https://arxiv.org/abs/2305.15425)`, never a pasted bare URL.
  Cite papers by author and year with a link, the way Yak does.
- **Every number is one you measured**, and the artifact that holds it is one click away.
- **Name the controls** next to the result: "random neurons at ×3: 0% to −13%".
- **Say what did not work or did not reproduce**, plainly, in the body, not only in the limits.
- **Captions carry the takeaway.** Not "Bar chart of X" but "Yak uses 40% fewer tokens than GPT-4o."
- **Tables for comparisons**: bold the row that is ours (the site tints it crimson automatically).
- Plain verbs: we built, we measured, we released, we have not tested.
- Define a term the first time you use it (fertility, AUROC, logit bias), in one clause.

## 4. Do not

- No hype words (validator rejects: revolutionary, groundbreaking, world-class, cutting-edge,
  game-changing, unparalleled, best-in-class). Also avoid "unlock", "supercharge", "magic".
- No claims beyond the measurement. "The neuron fires one step before bold" is fine; "the model knows
  before it starts" is not, unless you measured planning.
- No bare URLs, no empty header (missing `code:`/`model:` front matter), no default social card.
- No figure without a caption, no caption without a takeaway.
- No made-up or "illustrative" data in a chart. If it is a diagram, label it as a diagram.
- No AI attribution, no "as an AI", no em-dash pileups, no exclamation marks.
- Do not submit a variant of a queued post; revise the existing draft.

## 5. Consistency and creativity

Fixed (so every post feels like the same lab):
- Voice: first person plural, plain, technical, honest about limits.
- Palette: paper `#F7F6F3`, ink `#111111`, crimson `#DC143C` for *ours*, muted grey `#5E5A57` for *others*,
  pale `#F6D3DA` / tint `#FCEBEE` for bands. Crimson always means our result.
- Fonts come from the site (CMU Serif body, IBM Plex Mono numbers, Press Start 2P labels). Do not
  embed other fonts in posts. In raster figures, use a serif or mono that matches.
- Numbers: same precision as the source, units always, `×` for multipliers, `−` (minus) for negatives.

Free (this is where a post earns attention):
- The hook: a live demo, a before/after, a sound clip, a single striking sentence.
- Figure choices: an inline HTML demo, a custom SVG, a diagram of the mechanism, a photo of the bad microphone.
- Section questions phrased the way a curious reader would ask them.
- A Devanagari `glyph:` that fits the post (Yak uses याक).

## 6. Post format (what the blog renderer understands)

Front matter at the top of `post.md`:

```
---
type: release | benchmark | dataset | lesson | post
project: <slug>
project_label: <shown on the card, e.g. "yak tokenizer">
glyph: <one Devanagari word, shown huge behind the title>
summary: <≤180 chars; card + meta description>
code: https://github.com/Ampixa/...        # each of these becomes a "↗" header link
model: https://huggingface.co/...
dataset: https://...
benchmark: https://...
demo: https://...
paper: https://...
image: og-1200x630.jpg                       # social card; PNG or JPEG in the post folder
---
```

- Markdown is Python-Markdown with `fenced_code`, `tables`, `toc`. `##` headings become the contents
  sidebar.
- A paragraph that is only italics (`_Yak uses 40% fewer tokens._`) right under a figure or table
  becomes a styled caption (`p.cap`).
- Raw HTML blocks pass through when separated by blank lines. Markdown inside them is not processed,
  so write `<a href>` and `<strong>` there.
- Images: `![alt text](fig-name.jpg)`, with the file submitted alongside the draft. The site
  draws a 2px ink border and offset shadow; do not add your own frame.
- Read-aloud: a post can ship with narration clips, one per paragraph. If you change paragraphs after
  the audio is made, the audio has to be re-rendered.

## 7. Images and illustrations

Use them to make the point land, not to decorate. Every post above "short note" has:

| asset | size | purpose |
|---|---|---|
| `hero-16x9.jpg` | 1600×900 | the result at a glance: the one number, the one contrast |
| `og-1200x630.jpg` | 1200×630 | social card; same message, larger type, readable as a thumbnail |
| 2–6 figures | 1600 wide JPEG q≈86, or inline SVG | one claim each |

Pick the figure by the claim:
- **A versus B** (ours vs theirs, before vs after): sorted bars or dots, ours in crimson.
- **Change from baseline**: diverging stems from zero, with controls in grey on the same axis.
- **A dose or sweep**: line with every measured point marked; mark the baseline.
- **Two distributions**: strip plot (one dot per item) beats a mean ± sd bar.
- **"Is it in range"**: dots with a shaded pass band (Yak's reproduction chart).
- **What the model actually did**: a live HTML demo (`<figure class="demo">`) with real output.

Inline SVG charts inherit the site style if they use these classes: `.chart` on the
`<figure>`, `.scroll` wrapper div, and inside the SVG `bl` (row label, serif), `bv` (value, mono),
`bt` (tick, muted), `gl` (grid line), `band` (tint band), `stem`, `dot` (grey) and `dot core`
(crimson). Use `viewBox="0 0 640 H"`. Demo widget classes: `.demo`, `.src`, `.row` (add `.yak`
for the highlighted row), `.rl` with a `<b>` count, `.toks` and `.tok`.

Generate figures from the data file in the repo with a script committed next to it, so a reader can
rebuild every chart. Never hand-type chart values.

## 8. Before you submit

- [ ] TL;DR with bold key numbers and the main limit
- [ ] Front matter: type, glyph, summary, code/model links, image
- [ ] Hero + social image present and submitted with the draft
- [ ] Every figure and table has a takeaway caption
- [ ] Every citation and artifact is a markdown link; no bare URLs
- [ ] Controls stated next to the result; what failed is stated
- [ ] "What this is not" section
- [ ] The code shown is the code that produced the numbers, and it was run end to end as printed
- [ ] Numbers checked against the repo's results file
- [ ] Read the rendered preview yourself before asking for review
