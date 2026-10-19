# Rung 3: interactive HTML page

## When

The core of the content is "**change one thing, see how another changes**": how a parameter shapes a curve, how a threshold changes errors, which option wins under which conditions.

With text, the reader can only trust the author. With a slider, the reader sees the change and can try cases the author never mentioned.

LLMs are good at frontend now. A page like this can be built for one act of understanding and then thrown away.

## Step 1: draft first, then choose parameters

1. Write the rung-1 draft that explains the mechanism.
2. From the draft, pick **the one parameter whose change teaches the core intuition**. At most 1–3 parameters; more than that and the reader does not know where to start.
3. Write down a sensible range and default for each. The default should put the plot in an interesting state.

The interaction must teach the core intuition. A control that changes nothing important is decoration — remove it.

## Step 2: page anatomy

Top to bottom, every page has all of these parts:

1. **One-line summary**: what this page should make clear.
2. **Interactive area**: sliders + a live plot. Show the current value and unit next to each slider.
3. **Explanation**: the rung-1 draft, in numbered sections.
4. **Try this**: 2–3 concrete prompts, e.g. "Drag utilization from 90% to 95% and see how many times latency multiplies."
5. **Assumptions box**: visually prominent (colored background). Lists **every** simplification and assumption, which numbers are sample data, and what to check against the real system.
6. **Glossary**: every technical term on the page, one meaning per term, terms matching the draft.
7. **Footer**: generation date, and links to companion documents (older/newer versions, source discussion).

## Step 3: technical requirements

- **One HTML file, zero external dependencies.** CSS and JS inline. No CDN, no web fonts, no images by URL. Plain JS with `<canvas>` or `<svg>`. The page must open offline with a double-click.
- Font stack: system fonts (`-apple-system, "PingFang SC", "Microsoft YaHei", "Segoe UI", sans-serif`). Body max-width ≈ 880px, centered.
- Recompute and redraw **live** while dragging, not on release.
- Works on phones: fluid width, large sliders.
- Color carries meaning: one quantity, one color, in the plot and in the text.
- Demonstrative simulations are labeled **toy model** / 「玩具模型」, with one line on how they differ from the real system.
- Optional: a "copy current parameters" button so the reader can send a setting back to the agent.

## Step 4: deliver

1. Save the file in the working directory with a descriptive name, e.g. `queue-latency-explainer.html`.
2. **A revised approach gets a new file — never overwrite an old page.** Link old ↔ new at the top of each page, so the discussion history survives.
3. Tell the user the path. Open it in a browser if the environment allows.
4. In chat, 2–3 sentences: what the page shows and which slider to move first.

## Self-check

- [ ] Is the page understandable before touching any slider? (The default state must mean something.)
- [ ] Does every slider show its value and unit?
- [ ] Do the axes have names and units?
- [ ] Do terms match the draft and the glossary?
- [ ] Does the assumptions box list every simplification? Is sample data labeled as sample, toy models as toy models?
- [ ] Does the page open with the network off?
- [ ] Is the formula right? Check it once with values you can compute by hand.

## Example prompt

> Make a single-file HTML page on server utilization vs latency: two sliders (utilization, mean service time) and a live latency curve. Below it, explain the model in plain language and give three "try this" prompts.
