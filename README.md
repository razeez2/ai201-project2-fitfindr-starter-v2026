# FitFindr

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, every
> command, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> python app.py listings --full -n 6      # read the data (Milestone 1)
> python app.py fields                    # what you can filter on
> python app.py ask 'vintage graphic tee under $30'
> ```
>
> All three tools are stubs, so that last command will do nothing useful yet.
> That's the starting position.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     This is your submission. Fill each section in as you finish the milestone
     it belongs to — don't leave it all to the end.

     Unit 3 asks for the first five sections. Unit 4 adds the five below them.
     Leave the unit 4 sections alone until then; they're here so you know
     what's coming.

     Everything is pasted as TEXT. No screenshots, no images, no video links.
     A typed block of output gets full credit; a picture of the same output
     gets none.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 3 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Three or four sentences: what a user asks for, and what they get back. -->
The user types what they're looking for in plain language, like "vintage graphic tee under $30, size M". FitFindr pulls the description, size and max price out of that, then searches the thrift listings for the best match. If it finds one, it suggests one or two outfits that pair the item with clothes already in the user's wardrobe. It also writes a short social-media caption (a "fit card") that names the item, its price and the platform. If nothing matches, it stops and tells the user what to change in their search.



---

## Tool Inventory

<!-- Four lines per tool. This is worth 2 points and it's the single most
     common place students lose them.

     "Returns a list" earns NOTHING. The description has to say what is IN
     the list.

     The empty case isn't optional either — it's the thing your loop branches
     on, and if you don't decide it here you'll discover it as a crash in
     Milestone 5. -->



### `search_listings`

- **What it does:** This tool searches the listings file based on an input of description,size, and max_price and returns matches to the user.
- **Inputs:** description (str), size (str), max_price (float)
- **Returns:** list[dict]
- **When it has nothing:** It returns an empty list.

### `suggest_outfit`

- **What it does:** This tool takes a thrifted item and a user's wardrobe and returns outfit suggestions.
- **Inputs:** new_item (dict), wardrobe (dict)
- **Returns:** str
- **When it has nothing:** returns a general suggestion str

### `create_fit_card`

- **What it does:** takes a outfit from suggest_outfit and a new_item and returns a caption that someone would actually post about the outfit.
- **Inputs:** outfit (str), new_item (dict)
- **Returns:** str
- **When it has nothing:** returns a descriptive message (str)

---

## Planning Loop

<!-- Your branch rule, stated as a rule — the condition AND both paths — plus
     the file and function that holds it.

     Like this:
       "If search_listings returns an empty list, put a message in the session
        and stop. Otherwise take the first result and go to suggest_outfit."
        — agent.py::run_agent

     The grader checks your code against what you claim here, so the file and
     function have to be real. -->

**Branch rule:** If suggest_outfit has an empty wardrobe as its argument, ensure that str of a general suggestion is returned. Otherwise, use the current items in the user's wardrobe in the prompt to combine them.

**Where it lives:** `agent.py::run_agent`

**How the query is parsed:** <!-- regex, string splitting, or asking the model — say which -->

**What moves through the session:** <!-- which fields, in what order -->

---

## Sample Run

<!-- Two things go here.

     1. One FULL query and its output, pasted as text.
     2. Your three per-tool terminal tests — the command and what it printed. -->

**One full query**

```
$ python app.py ask 'vintage graphic tee under $30'
  Found:    Y2K Baby Tee — Butterfly Print — $18.0 on depop

  Outfit:   Here are two distinct outfits you can create using your new Y2K Butterfly Baby Tee and your existing wardrobe, playing with the contrast of fitted and baggy silhouettes typical of 2000s streetwear:

### Outfit 1: Effortless Y2K Streetwear (Balanced Proportions)
*This look pairs the ultra-fitted, cropped nature of the baby tee with your relaxed denim for that classic early-2000s model-off-duty vibe.*

*   **Top:** Y2K Baby Tee (Butterfly Print)
*   **Bottoms:** Baggy straight-leg jeans (dark wash)
*   **Accessories:** Brown leather belt (let it peek out) + Black crossbody bag
*   **Footwear:** Chunky white sneakers
*   **Layering (Optional):** Vintage black denim jacket (worn off the shoulders or carried on the arm)

**Why it works:** The tight baby tee balances out the voluminous baggy jeans. The brown belt adds a nice 90s/Y2K color contrast against the dark wash denim, and the chunky sneakers tie the retro streetwear aesthetic together.

---

### Outfit 2: Edgy Contrast & High-Low Mix
*This outfit leans into the nostalgic butterfly print but adds a tougher, grungier edge using your black outerwear and boots.*

*   **Top:** Y2K Baby Tee (Butterfly Print)
*   **Bottoms:** Wide-leg khaki trousers
*   **Outerwear:** Black cropped zip hoodie (worn open or partially unzipped to show off the tee)
*   **Accessories:** Black crossbody bag
*   **Footwear:** Black combat boots

**Why it works:** Pairing a feminine, playful baby tee with structured khaki trousers creates a cool high-low contrast. Throwing the black cropped zip hoodie over top keeps the midriff-baring Y2K proportions intact while the combat boots anchor the outfit and add a modern, edgy twist.

  Fit card: 🦋 Channeling pure early 2000s model-off-duty energy with this Y2K butterfly baby tee! Rock it oversized with baggy denim or lean into edgy streetwear with combat boots.

Grab this super cute fitted crop top for just $18 on Depop! ✨
```

**The three tools, tested one at a time**

```
$ python -c "from tools import search_listings; print(search_listings('graphic tee', max_price=30))"
[{'id': 'lst_002', 'title': 'Y2K Baby Tee — Butterfly Print', 'description': 'Super cute early 2000s baby tee with butterfly graphic. Fitted crop length. Tag says medium but fits like a small.', 'category': 'tops', 'style_tags': ['y2k', 'vintage', 'graphic tee', 'cottagecore'], 'size': 'S/M', 'condition': 'excellent', 'price': 18.0, 'colors': ['white', 'pink', 'purple'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_006', 'title': 'Graphic Tee — 2003 Tour Bootleg Style', 'description': 'Vintage-style bootleg tee with faded graphic. Slightly boxy fit. 100% cotton, soft and worn-in.', 'category': 'tops', 'style_tags': ['graphic tee', 'vintage', 'grunge', 'streetwear', 'band tee'], 'size': 'L', 'condition': 'good', 'price': 24.0, 'colors': ['black'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_017', 'title': 'Mesh Long-Sleeve Top — Black', 'description': 'Sheer black mesh long-sleeve. Great for layering under a graphic tee or over a bralette. Stretchy material, fits true to size.', 'category': 'tops', 'style_tags': ['y2k', 'grunge', 'goth', 'layering'], 'size': 'S/M', 'condition': 'excellent', 'price': 15.0, 'colors': ['black'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_033', 'title': 'Vintage Band Tee — Faded Grey', 'description': 'Faded grey band-style tee with distressed graphic. Crew neck. Fits boxy. Well-loved but no holes or major damage.', 'category': 'tops', 'style_tags': ['vintage', 'grunge', 'band tee', 'graphic tee', 'streetwear'], 'size': 'L', 'condition': 'fair', 'price': 19.0, 'colors': ['grey', 'charcoal'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_011', 'title': 'Low-Rise Cargo Pants — Khaki', 'description': 'Y2K era low-rise cargo pants. Lots of pockets. Khaki color, slightly distressed at the hems. Great for layering with a long tee.', 'category': 'bottoms', 'style_tags': ['y2k', 'cargo', '2000s', 'streetwear'], 'size': 'W29', 'condition': 'fair', 'price': 27.0, 'colors': ['khaki', 'tan'], 'brand': None, 'platform': 'poshmark'}, {'id': 'lst_012', 'title': 'Oversized Crewneck Sweatshirt — Vintage Navy', 'description': 'Perfectly faded navy crewneck. Genuinely vintage — not manufactured distressed. Ribbed cuffs and hem. No graphics, clean.', 'category': 'tops', 'style_tags': ['vintage', 'basics', 'oversized', 'classic'], 'size': 'XL (fits oversized)', 'condition': 'good', 'price': 20.0, 'colors': ['navy'], 'brand': None, 'platform': 'thredUp'}, {'id': 'lst_015', 'title': 'Vintage Graphic Hoodie — Faded Black', 'description': 'Faded black pullover hoodie with barely-visible vintage graphic on the chest. Cozy interior. Some pilling but adds to the worn-in look.', 'category': 'tops', 'style_tags': ['vintage', 'grunge', 'graphic', 'streetwear'], 'size': 'L', 'condition': 'fair', 'price': 26.0, 'colors': ['black', 'charcoal'], 'brand': None, 'platform': 'depop'}]
```

```
$ python -c "from tools import suggest_outfit; from utils.data_loader import get_example_wardrobe, load_listings; print(suggest_outfit(load_listings()[0], get_example_wardrobe()))"
Here are two distinct outfits you can create using your new Vintage Levi’s 501 Medium Wash jeans and items already in your wardrobe. 

### Outfit 1: Casual & Cool (90s Off-Duty Model)
*This look leans into the classic, effortless appeal of medium-wash vintage denim with a relaxed, streetwear-inspired edge.*

*   **Top:** White ribbed tank top (tucked in to define the waist)
*   **Layer:** Vintage black denim jacket (worn open or draped over the shoulders)
*   **Belt:** Brown leather belt (adds a nice contrast of warmth against the medium-wash denim)
*   **Shoes:** Chunky white sneakers
*   **Bag:** Black crossbody bag

**Why it works:** The white tank and blue denim combo is timeless, while the black denim jacket adds a cool, textured "denim-on-denim" juxtaposition. The brown belt grounds the look, and the chunky sneakers keep it modern and comfortable.

---

### Outfit 2: Cozy Contrast (High-Low Streetwear)
*This outfit plays with proportions by pairing the structured, straight-leg fit of the 501s with an oversized, slouchy layer.*

*   **Top:** Oversized grey crewneck sweatshirt (you can do a half-tuck or let it drape casually)
*   **Shoes:** Black combat boots (let the hem of the 501s break slightly over the tops of the boots)
*   **Accessories:** Black crossbody bag 

**Why it works:** Vintage Levi's 501s have a rigid, authentic structure that looks amazing when paired with something oversized and cozy like the grey crewneck. Tugging the jeans down into the black combat boots creates an edgy, slightly grunge-inspired silhouette that feels very current.
```

```
$ AI201_CACHE=0 python -c "from tools import create_fit_card; from utils.data_loader import load_listings; print(create_fit_card('jeans and white sneakers', load_listings()[0]))"
Effortlessly cool and perfectly worn-in. Snagged these vintage Levi's 501 jeans for $38 on Depop and paired them with crisp white sneakers for the ultimate laid-back weekend vibe. ✨👟
```

---

## How I Used AI

<!-- Two specific moments. What you asked, what came back, what you changed.

     "I used Claude to help me code" is not enough.

     "I gave Claude my search_listings spec. It returned None on no match
     instead of an empty list, so I changed it" is the level we want. -->

**Moment 1**

- *What I asked for:* I gave Claude my draft acceptance criteria and asked it to check whether each one was measurable.
- *What came back:* It said criteria 3 and 4 weren't specific enough to score, and suggested measurable versions: compare ids for state, and compare first sentences for fit cards.
- *What I changed:* I rewrote criterion 3 as "In 4 of 5 runs, the id of session['selected_item'] equals session['search_results'][0]['id'] and the id of the item that reached suggest_outfit." I rewrote criterion 4 as "5 cards for 5 different items share no first sentence." Now I can count both instead of judging them by eye.

**Moment 2**

- *What I asked for:* I asked Claude whether my three tool functions were good, and had it give me tests to run on each one from the terminal.
- *What came back:* One `python -c` command per tool. These are the three commands in the Sample Run section above, including `search_listings('graphic tee', max_price=30)` and a `create_fit_card` test run with `AI201_CACHE=0` so the cache doesn't hand back an old caption.
- *What I changed:* I changed the function lines, claude was giving a wrong line for suggest_outfit function where it wasnt using (generate) prompt and instead was just hard coding a description, so I added that. I then used the tests it gave me to verify the outputs were as expected for every tool.

<!-- ═══════════════════════ UNIT 4 — THE TEST ═══════════════════════

     Don't fill these in during unit 3.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Run Log — Before

<!-- Five criteria, five tries each, in this exact format.

     Five, because your criteria are written out of five. Mark each try PASS
     or FAIL, count the passes, and read that count against your target — a
     row targeting 4 of 5 with three PASS cells is MISSED (3/5).

     `python run_eval.py --label before` runs everything and writes the table
     into results/. Paste it here and fill in the verdicts. -->

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. Matching query completes all three tools and returns a fit card | At least 4/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 2. Impossible query stops before suggest_outfit and names what to change | 5/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 3. Selected-item ID matches the first search result and the item passed to suggest_outfit | At least 4/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 4. Five cards for five different items share no first sentence | 5 different items, 5 unique first sentences | PASS | PASS | PASS | PASS | PASS | MET (5/5 distinct items and openings) |
| 5. Empty wardrobe returns a non-empty outfit suggestion | At least 4/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |

Evidence for criteria 1, 2, 3, and 5: `results/run_2026-10-13_2328_before.md`. All five state-check tries recorded first=lst_002, selected=lst_002, passed=lst_002, with match=True.

Criterion 4 was tested separately with caching off; the full commands and output are saved in [results/criterion4_manual_before.txt](results/criterion4_manual_before.txt). Its Try columns represent one card per different item, in this order: butterfly (lst_002), 501 (lst_001), denim jacket (lst_007), floral dress (lst_013), and flannel (lst_003). All five caption openings are distinct. The butterfly caption's formatting label, "Caption:", is excluded from the comparison. Three captions start with "Two ways to style", but their complete first sentences differ, which meets the original criterion.

**Real output from one try**, pasted as text, naming the file and function
that produced it:

```

```

---

## Verdicts and Diagnoses

<!-- MET or MISSED per criterion against LAST UNIT's target, plus a sentence on
     how you decided.

     Then, for every miss: which of the four places it happened — a tool, the
     loop's branch, the session, or the model's output — AND the mechanism.

     Not a diagnosis:  "The fit card was bad."
     A diagnosis:      "The fit card criterion missed on 2 of 5 items. Both had
                        an empty brand field. My prompt puts the brand in the
                        first sentence, so the card opened with a blank and read
                        like a fragment. The tool worked; the prompt assumed a
                        field that isn't always there."

     Look for a pattern. Three misses on the same tool is one problem, not
     three. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Matching query completes all three tools and returns a fit card | At least 4/5 | MET (5/5) | Each matching-query try called search, outfit suggestion, and fit-card creation and returned a non-empty fit card. |
| 2 | Impossible query stops before the second tool and names what to change | 5/5 | MET (5/5) | Every impossible-query trace showed an empty search followed by a stop, with no outfit or fit-card call. The message suggested changing price, size, or keywords. |
| 3 | Selected-item ID matches the first result and the item passed to suggest_outfit | At least 4/5 | MET (5/5) | Every state-check try logged first=lst_002, selected=lst_002, passed=lst_002, and match=True. |
| 4 | Five cards for five different items share no first sentence | Five distinct items and five unique first sentences | MET | The five manual runs selected lst_002, lst_001, lst_007, lst_013, and lst_003. Their complete first sentences were all different, excluding the formatting label "Caption:". |
| 5 | Empty wardrobe returns a non-empty outfit suggestion | At least 4/5 | MET (5/5) | Every empty-wardrobe try returned non-empty general styling advice and completed without a crash. |

**Diagnoses**

None of the five criteria missed its original target in these tests, so there is no observed miss to diagnose. The earlier uncertainty for criteria 3 and 4 came from the test setup: the trace did not expose the IDs, and the fit-card scenario repeatedly selected the same item. Logging the IDs and running five distinct items supplied the missing evidence.

Some targets were permissive. Criterion 3 allows one state mismatch even though the loop directly passes the selected item, and criterion 5 only checks that advice is non-empty, not that it is useful. I would tighten criterion 4 in a future test: require five different opening phrases as well as different full first sentences. Three of the five cards began with "Two ways to style", so the current target allows repetitive phrasing even though all five sentences are technically unique. The step involved is `create_fit_card`, and the pattern is in the model's output: the prompt requests a short caption but does not constrain repeated opening phrases. This is a quality limitation, not a miss against the original criterion.

**Opposite-verdict review:** The strongest argument for calling criterion 4 MISSED is that three openings use the same phrase and therefore sound repetitive. However, the original criterion compares full first sentences, not opening phrases, and those sentences differ. MET is supported by the stated target. These results establish success on the tested queries; they do not establish that every possible query will pass. No original criterion was revised.


---

## Loop Trace

<!-- One full run, printed step by step, with the MCP call visible in it.

     `python app.py ask '...' --trace` once you've added the trace.step()
     calls in Milestone 2.

     Worth pasting BOTH the happy path and the empty-search path. The empty
     one should be visibly shorter, because it stops. If your two traces are
     the same length, your branch isn't working — and this is the fastest way
     anyone will ever find that out. -->

**Happy path**

ython app.py ask 'vintage graphic tee under $30' --trace
[1] search_listings(via MCP)
      in:  dict with keys: description, size, max_price
      out: 10 items: Y2K Baby Tee — Butterfly Print, Graphic Tee — 2003 Tour Bootleg Style, Vintage Band Tee — Faded Grey … +7 more
[2] suggest_outfit
      in:  dict with keys: new_item, wardrobe
      out: Here are two distinct outfits you can create using your new Y2K Butterfly Baby Tee and your existing wardrobe,…
[3] create_fit_card
      in:  dict with keys: outfit, new_item
      out: 🦋 Channeling pure early 2000s model-off-duty energy with this Y2K butterfly baby tee! Rock it oversized with b…

```

```

**Empty search**

python3 app.py ask 
'spacesuit' --trace
[1] search_listings(via MCP)
      in:  dict with keys: description, size, max_price
      out: [] (empty)

  No listings matched 'spacesuit'. Try a higher max price, a different size, or fewer keywords.

0 model calls this session

```

```

**On the MCP move:** <!-- what changed in your code, and whether anything
behaved differently afterwards. If the rewire didn't work, say exactly where it
broke — the error text and the last thing that worked. That earns the point in
full. -->



---

## The Improvement

<!-- What you changed, why your diagnosis pointed at it, and the after-run in
     the same table format. One change, measured properly.

     `python run_eval.py --label after` -->

**What I changed:**

I rewrote only the non-empty-outfit prompt in `tools.py::create_fit_card`. It now asks for one two-to-four-sentence caption without a heading, with an opening based on the item's color, texture, print, or silhouette. It explicitly avoids generic openings such as "Two ways to style", "Channeling", and "Serving". Search, outfit suggestions, the planning loop, and the original acceptance criteria are unchanged.

**Which failure it was meant to fix:**

Milestone 4 found a quality limitation in the model's output: three of five manual captions opened with "Two ways to style". All five met the original unique-first-sentence criterion, but the repeated phrase made captions for different items sound similar. This prompt change targets that pattern.

### Run Log — After

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. Matching query completes all three tools and returns a fit card | At least 4/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 2. Impossible query stops before suggest_outfit and names what to change | 5/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 3. Selected-item ID matches the first search result and the item passed to suggest_outfit | At least 4/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 4. Five cards for five different items share no first sentence | 5 different items, 5 unique first sentences | PASS | PASS | PASS | PASS | PASS | MET (5/5 distinct items and openings) |
| 5. Empty wardrobe returns a non-empty outfit suggestion | At least 4/5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |

Full evaluation evidence: [results/run_2026-10-14_0001_after.md](results/run_2026-10-14_0001_after.md), produced by `python run_eval.py --label after` with caching off. Criterion 4 uses a separate repeat of the same five manual queries as the before test; full sessions and traces are saved in [results/criterion4_manual_after.json](results/criterion4_manual_after.json). Its Try columns correspond to butterfly (lst_002), 501 (lst_001), denim jacket (lst_007), floral dress (lst_013), and flannel (lst_003). The full runner's wool-sweater scenario returned no matches, so it could not establish criterion 4 by itself; that scenario is not counted as a successful caption test.

**Caption opening evidence from the five manual after runs**, produced by `tools.py::create_fit_card` through `agent.py::run_agent`:

| Item ID | First sentence |
|---|---|
| lst_002 | This fitted, cropped baby tee features a nostalgic butterfly graphic and a soft texture that screams early 2000s. |
| lst_001 | Featuring a structured rigid silhouette with light fading at the knees, these vintage medium-wash Levi's 501 jeans offer the ultimate off-duty model aesthetic. |
| lst_007 | Featuring structured shoulders and a versatile blank-canvas light wash, this $42 cropped denim jacket from Poshmark anchors two contrasting streetwear-inspired looks. |
| lst_013 | This muted floral silk slip dress features a delicate midi silhouette with adjustable straps and a subtle, weightless drape. |
| lst_003 | This oversized red and black plaid flannel shirt features a classic relaxed silhouette and soft, lived-in texture. |

**Did it help, and how do I know:**

It reduced the specific repeated opening: on the same five manual queries with caching off, "Two ways to style" went from 3/5 captions before to 0/5 after, while all five original criteria remained MET.

| Measure | Before | After |
|---|---|---|
| Criterion 1 passes | 5/5 | 5/5 |
| Criterion 2 passes | 5/5 | 5/5 |
| Criterion 3 passes | 5/5 | 5/5 |
| Criterion 4 distinct items / distinct first sentences | 5 / 5 | 5 / 5 |
| Criterion 5 passes | 5/5 | 5/5 |
| Manual captions opening with "Two ways to style" | 3/5 | 0/5 |

This is a small sample of model outputs, not a guarantee. The new captions still share templates such as "This ... features" and "Featuring ...", and sound more like product descriptions. Some full-evaluation captions also added unsupported details: a butterfly tee was described as having a "soft ribbed texture" or a "shimmering butterfly graphic", neither specified by its listing. The change helped the diagnosed phrase repetition, but did not solve every caption-quality problem.

<!-- If it made things worse, say that. Honestly reported, that earns full
     credit and is more interesting than one that worked. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped where
     you did. "I ran out of time" is fine if it's true. Pretending nothing is
     left is not. -->

No original acceptance criterion is still missed in the scored after tests. Caption quality remains limited by repeated sentence structures and occasional invented material details. A future prompt experiment would require using only listing-supported details and test factual accuracy as well as varied openings. I stopped after one prompt change to keep this milestone's comparison attributable to one improvement. The wool-sweater scenario also needs a query that selects an existing item if criterion 4 is to be tested entirely by `run_eval.py`; the documented manual tests supplied that evidence here.



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 3

       [ ] criteria.md has five numbered criteria, each with a target
       [ ] Each criterion has a reason underneath it
       [ ] All five unit 3 sections above have real content
       [ ] Tool Inventory: all three tools, inputs WITH TYPES, a specific
           return value, and the empty case
       [ ] Planning Loop names the branch rule and agent.py::run_agent
       [ ] Sample Run: one full query plus the three per-tool tests, as text
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN, you submit the same one
           next unit

     SUBMISSION CHECKLIST — unit 4

       [ ] mcp_server.py exists with one tool registered
           (or a written record of exactly where the rewire broke)
       [ ] Run Log — Before, five criteria, five tries each
       [ ] Real output pasted underneath, naming file and function
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, naming a place AND a mechanism
       [ ] Loop Trace, with the MCP call visible in it
       [ ] All three failure modes triggered and handled
       [ ] One improvement, with Run Log — After in the same format
       [ ] What's Still Broken
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository. Your commit history is what
     shows your criteria existed before your results did.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**