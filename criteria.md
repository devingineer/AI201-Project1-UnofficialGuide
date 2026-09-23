# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
<!-- e.g. "One of my questions is about a topic only two documents mention, so
     I expect that one to be hard." -->

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
<!-- Why all five and not four? What about your setup makes that achievable —
     or what would have to go wrong for it not to be? -->

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
<!-- What did your distances look like when you set the cutoff in Milestone 4?
     Was there a clean gap, or did the two groups overlap? -->

---

## 4. Every chunk still names the thing it describes

All 35 chunks drawn from my housing and dining documents (7 buildings × 3 docs,
7 halls × 2 docs) contain the building or hall name. Zero chunks that describe
a specific building are anonymous.

**Why this target:**
<!-- My documents are 183 to 554 characters — every one of the
88 fits inside a single 800-character chunk, so at the default settings
chunking does nothing at all and overlap never fires. That makes "is a sentence
cut in half" the wrong question for this corpus; nothing is cut. The real risk
is the opposite one: if Milestone 3 leads me to chunk *smaller*, the longer
housing documents split, and the building name lives only in the title line, so
the second half becomes an orphan that reads "Machines take $1.50 wash, coin
only" with nothing saying where. That matters more here than in most corpora
because the seven `*_laundry.txt` documents are near-identical templates
differing only in building name and price — an anonymous chunk is not merely
less useful, it is indistinguishable from six wrong answers. 35 of 35 and not a
sampled fraction, because one orphaned chunk is one building I can silently
answer wrong. -->


---

## 5. The source named is the *right* source

For all 5 of my test questions, the document the answer names is one that
actually contains the answer. For the Old Brewhouse laundry question
specifically, the named source is `housing_old_brewhouse_laundry.txt` and not
any of the six other buildings' laundry documents.

**Why this target:**
<!-- Criterion 2 only asks that *a* source appears, and in this
corpus that is close to free — every answer will cite something. It doesn't
catch the failure I actually expect. The seven laundry documents differ by one
building name and a price; the seven dining documents and their `Re:` followups
are nearly as close. Retrieval landing one building off produces an answer that
is fluent, confidently sourced, and wrong about how much I'll pay — and
criterion 2 scores that as a pass. So the thing worth measuring is whether the
citation is correct, not whether it exists.

5 of 5 rather than 4 of 5, because I can't justify budgeting one wrong
attribution. A refusal tells the user to go look it up; a wrong building told
in a confident voice, with a filename attached, tells them not to bother. Those
are not the same kind of miss, and the near-duplicate documents are exactly
where the miss will come from if it comes at all. -->



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
