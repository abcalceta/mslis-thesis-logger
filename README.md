# Stance — a corpus logger for *The Diary That Talks Back*

A small web app that installs to your phone's home screen. It captures flags in about ten
seconds, sets your morning stance and then **locks it**, turns the day's flags into episodes
with a shape, and pushes everything to a private repo you own.

No account, no server of mine, no data anywhere but your phone and your repo.

---

## Setup — about twenty minutes, once

### 1. A private repo for the data

On GitHub, **New repository** → name it something like `thesis-corpus` → **Private**.
Tick "Add a README" so the repo isn't empty. Don't put anything else in it.

This is where your memos will live. Two files per day:

```
days/D-20260924.md     ← readable: the morning table, the flags, the episodes
data/D-20260924.json   ← countable: same thing, structured, for the analysis
```

### 2. A token scoped to exactly that repo

GitHub → **Settings** → **Developer settings** → **Personal access tokens** →
**Fine-grained tokens** → **Generate new token**.

- **Repository access:** *Only select repositories* → pick your data repo, and nothing else
- **Permissions:** *Repository permissions* → **Contents: Read and write**. Nothing else.
- **Expiry:** set a date past your collection window, and put a reminder to rotate it

Copy the token. You only see it once.

### 3. Put the app somewhere your phone can open it

The app holds no data, so it can live in a **public** repo — separate from your data repo.

New repo → `stance-logger` → Public → upload `index.html`, `manifest.json`, `sw.js`, `icon.svg`.
Then **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.

A minute later it's at `https://<you>.github.io/stance-logger/`.

> If you'd rather nothing about this be public, put the app in the private repo too and open it
> from a local copy instead — but you lose home-screen install and offline, which are most of the
> point. Public is fine: there is nothing in these four files except the app itself.

### 4. Install it on your phone

Open that URL on your phone, then:

- **iPhone** — Safari → Share → **Add to Home Screen**
- **Android** — Chrome → ⋮ → **Add to Home screen** / **Install app**

It now opens like an app, full screen, and works with no signal.

### 5. Connect it

Open it → **Setup** → your GitHub username, the data repo name, branch (`main`), and the token
→ **Save settings** → **Test the connection**.

It should say *Connected · private ✓*. If it says the repo is **public**, stop and fix that first.

Then set your **open questions** at the bottom of Setup. These are what you'll be asked about
every morning.

**The test for a good one:** can you finish *"right now I think…"* about it in one line, and would
that line be different in a month? *Having enough energy*, *finishing the thesis* and *doing well at work* all pass — you can say where
you stand on each today. *Diabetes* fails: it's a topic, not a question; you don't hold a reading of
diabetes, you hold one of whether you're managing it.

A question also has to belong to a strand, because its episodes will. With the corpus at PH / MH / CL / E,
*whether I'm good enough at this* is a CL question. The thesis's argument and work tasks still
have nowhere to live, and never will.

---

## Using it

**Morning, before the first strand-relevant chat.** Open → *Morning*. **The check-in comes first**
— six rows, about a minute, and it sets the day. The app computes the status from your Session
Safety Rules §1 and says what follows from it: *no health threads today* on red, *no new diagnosis
or medication topics and a loop cap of 2* on amber. **You can't lock the morning until it's done.**

Red doesn't stop you logging. §1 says a health topic that comes up anyway is logged as a deviation
and *counts as data*, so the app warns rather than blocks — blocking would destroy the observation
the rule exists to capture.

**Focus is a number only and sets nothing.** §1 says those thresholds are yours to agree with your
clinician and there isn't one for focus, so the app doesn't invent one. If you ever set one, put it
in §1 and in the app in the same change.

Then, for each open question,
write one line on where it stands, tick what's true, and the stance falls out — **fixed**,
**loose**, **divided**. Press **Save and lock**.

The six indicators are, in plain terms: *I can't sum it up in one sentence* · *I think two different
things about it* · *what I think has changed recently* · *something outside me could settle it* ·
*I keep going back to it* · *thinking about it does something to me*. None of them mention the LLM,
the conversation, or how anything turned out — that's what stops the whole thing being circular.

**If you reword an indicator here, reword it in the Coding Framework too, in the same commit.**
A codebook that describes different prompts from the ones you actually answered isn't a record of
what you did.

It really does lock. There is no edit button, by design. If the day changes your mind, that goes
in the evening note or the weekly review as a *finding*. Not as a correction.

**Through the day.** Something lands → open the app → tap the strand, one phrase, **Save flag**.
The time is stamped for you. Two taps and a sentence.

Describe **the move, not a diagnosis**: *reframed what I said in different words — I went back to
it twice*, rather than naming a condition or a clinical term. You're recording what happened in
the exchange, and the flag is how you find the episode again later.

The strands are **PH** physical health (diabetes, the knee, sleep, blood pressure), **MH** mental
health (mostly the diagnosis question), **CL** career life (the woes of working and studying —
capability, belonging, keeping up) and **E** everyday life.

**CL is the feeling, never the job.** *"Am I actually any good at this"* is CL. How to format a
report isn't data at all. And the standard for writing it up is **unidentifiable, not just
unnamed** — in a field this small, *"my boss"* is one person. Clean that at export, never by
watching your words while you're actually talking; that would be staging. The line between PH and MH is
**what the episode is about**, not which conditions get mentioned: how you read your body, or how
you read your mind. When it's honestly both, tick **crossover** and keep going — those are
interesting on their own, not a filing failure.

Never type a marker into the conversation itself. The model would respond to it.

**Evening.** Open → *Evening*. Your flags are listed. Add an episode for each thing you actually
worked on, pick the strand and which open question it belongs to — the stance is copied from this
morning and shown greyed out, because it isn't yours to change now. Tick the four shape indicators
from **your opening move**, not from how it went. Write what was worked on and whether a meaning
moved.

If a thing wasn't in the morning note, leave the question as *none of them* — the episode is
tagged `T0-absent` and you set stance from the episode's first message instead. Those get checked
separately at analysis.

**Push** whenever. It queues offline and pushes when there's signal. Nothing is lost if you don't.

---

## For the ethics application

Something like this, adjusted to your board's wording:

> Corpus memos (T0 morning notes, in-the-moment flags, T1 evening notes) are recorded on the
> researcher's own mobile device and transmitted directly to a private version-controlled
> repository under the researcher's sole control. No third-party analytics, accounts or
> intermediary services are involved. Access is limited to the researcher via a scoped
> credential restricted to that single repository. Commit timestamps are generated by the
> repository host and constitute the audit trail for protocol adherence — specifically, they
> evidence that T0 stance codings were recorded prior to, and not revised after, the
> interactions they describe. Conversation transcripts themselves are exported, segmented and
> redacted separately and are not handled by this application.

Two things to be straight about with them:

- The repository host is a third party (GitHub, i.e. Microsoft). Your memos sit on their
  servers, encrypted at rest, in a private repo. That is ordinary research practice, but
  **say it** rather than letting them discover it.
- The audit-trail argument only works *because* the timestamps come from outside your control.
  A local-only repo would have timestamps you could forge. That's the trade: the thing that
  makes the evidence good is the thing you have to disclose.

---

## Things to know

- **The token sits in your phone's browser storage.** Clear site data and you re-enter it. It is
  never sent anywhere except GitHub. Treat it like a password: if the phone is lost, revoke it.
- **Entries live on the phone until you push.** They survive closing the app and restarting the
  phone. They do not survive clearing site data, so push at least every few days. *Setup →
  Download everything as JSON* is your belt-and-braces backup.
- **Thresholds are adjustable in Setup** — currently 2 for *loose*, 4 for *divided*, 2 for
  *open-ended*. These are not piloted. Run a week of real mornings first; if everything comes out
  the same level, move them here rather than rebuilding anything. Every JSON file records the
  thresholds in force when it was written, so a change mid-study is visible rather than silent.
- **It doesn't touch transcripts.** Exporting, segmenting at 60-minute gaps and redacting third
  parties are separate jobs, deliberately.
- **One phone.** There's no sync between devices; the repo is the merge point, and two phones
  writing the same day would overwrite each other.

---

## If something breaks

| What you see | What it means |
| --- | --- |
| *Not found — check the name, or the token's repo scope* | The token isn't scoped to that repo, or the name is wrong |
| *Token rejected* | Expired or revoked — generate a new one |
| *Connected — but this repo is PUBLIC* | Stop. Make it private before you log anything real |
| *Pushed 2, then: Write … 409* | Someone (you, elsewhere) changed the same file. Push again |
| App won't open with no signal | The service worker needs one online visit first |

Built 24 September 2026 · **v2.6**. Strands PH / MH / CL / E with crossover tagging · plain-language
indicators · an open-question register that opens, closes and reopens rather than adds and deletes ·
the §1 safety check-in, which gates the lock · and a seed migration for installs that already hold an
older question list.

**100 automated checks** across flag capture, every stance / shape / check-in threshold boundary, the
morning lock and its persistence, `T0-absent`, the question register, the written output, UTF-8
round-tripping, and upgrading an install that already has data.
threshold boundary, the lock and its persistence, `T0-absent` handling, the written output, and
UTF-8 round-tripping.

---

## Adding an open question later

You will. Life doesn't hold still for a collection window, and a design that can't take a new
open question is broken. But there's a trap in it, so the app makes you do two things.

**Every new question needs a reason, written at the moment you open it.** Not later. The app
won't let you past without one.

The reason matters because there are two ways a question gets added, and they are not the same:

- **Your life changed.** A result came back, a decision arrived, something became live. Expected,
  fine, and the addition is itself data — *when* something became an open question is worth knowing.
- **The data looked good.** You had three interesting exchanges about your mum, noticed the
  recursion, and added it so it'd be tracked. That is **selecting on the outcome** — the same
  error as re-coding a morning stance after reading the transcript, wearing a different hat.

You often can't tell which one you're doing in the moment, and that's exactly why the reason is
recorded *before* analysis rather than reconstructed after. The second kind is still allowed —
write it down honestly and report it. A reader who can see all the additions with their reasons
can judge for themselves. A reader who can't, can't.

**Questions are never deleted.** When one settles, you **close** it — dated, with a reason — and
it keeps appearing in your morning note for another four weeks (adjustable in Setup).

That's deliberate. "It settled" is not a reason to stop looking; it's the *claim your delayed
check exists to test*. Your own working hunch is that what feels settled at the end of a chat
often doesn't hold days later. Delete the question at the moment it closes and you've thrown away
the only case where you could have seen that.

If it does come back, **reopen** it. The app asks what reopened it and appends that to the
question's history rather than overwriting it. A question that reopens is a finding, not a
mistake in your list.

**Nothing back-dates.** Adding a question today doesn't create morning entries for last week.
Episodes about it from before it was on the list stay tagged `T0-absent`, coded from the
episode's first message — which is honest, and the tag means you can check at analysis whether
those episodes behave differently.

**Renaming is safe.** Questions carry an internal id, so episodes stay attached to the right
question even if you reword it.

**The register travels with the data.** Every day's JSON carries the full list — every question,
when it opened, why, when it closed, why, and any reopenings. Your denominators are reconstructable
from the files alone, which is what you want when you're writing Chapter 4 in November and can't
remember what you were thinking in October.

---

## If the app shows old open questions

The app keeps your list in the browser's storage, so whatever it saved the **first** time you
opened it is what it keeps using — a later version's starting set won't overwrite it.

**From v2.1 it fixes itself:** open the app, and if you haven't yet locked a morning, the list is
quietly moved to the current starting set. You'll see a short "open questions updated" message.

If it doesn't, **Setup → Reset to the starting set**.

**Once you've locked your first morning, neither of these will touch the list**, and that's
deliberate — from that point the register is study data, and questions close rather than
disappear. After that, change the list the ordinary way: open new ones with a reason, close the
ones that no longer apply.
