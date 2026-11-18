# Campus Stores — my work sample

**Would I keep this product?** Yes, with one change: the desk needs to track *who physically holds each item right now*, not just who signed for it.

## Where to find my work

- **Change:** `app.js` (logic) and `styles.css` (one small `.warn` style).
- **Commit with the change:** see the commit list of this fork. The final commit is the one I submitted.
- **Screenshots:** in `docs/` (before and after the change).
- **Live demo:** `https://shashankkachouli.github.io/campus-stores/` (enable GitHub Pages: Settings → Pages → Deploy from branch → `main`).

## What I did on my shift

> Fill in the bracketed parts from your own run before submitting.

- **3:45 pm pickup:** I issued [PR-04 / SP-02 / AD-__] to Kabir Sen on RQ-214, return by Fri 8 pm. I chose adapter [AD-__] because [reason].
- **7:30 pm return:** Kabir returned the projector and speaker. The adapter was still with Leela Das. I closed the projector and speaker slips and left a Desk book note.
- **Sat 9:00 am:** Leela arrived with an adapter. I had to work out which slip it belonged to and close it.

## One moment the product handles well

**The issue-slip guardrails.** When I tried to issue a second adapter under RQ-214, the app refused: *"The approved quantity of this equipment type is already on loan."* It also blocks units that are in repair, units already out, and equipment that isn't on the request. These checks stop the most common counter mistake, handing out the wrong or an extra item, without slowing down a correct issue.

Because the register is one slip per physical unit (AD-12 and AD-15 are tracked separately), the desk always knows exactly which item left.

## One moment I would change

**Saturday 9:00 am, closing the adapter loan.**

- The slip said the adapter was issued to **Kabir**, but the Desk book said **Leela** had it. The register had no way to record that the item had changed hands, so the truth lived only in free text.
- There are two identical adapters (AD-12 Belkin and AD-15 Anker) in the same bin, C4. **Record return** closed a slip without asking which unit I was holding, so a wrong adapter could have been put back in stock under the wrong slip.
- The return was due Friday 8 pm, but nothing marked it overdue.
- To see what was still out for RQ-214, I had to read separate slips and the Desk book and put the picture together myself.

## The change

1. **Hand over.** Each outstanding slip has a **Hand over** action that records who holds the item now. Slips show *Issued to* and *Now with* separately.
2. **Confirm the unit on return.** **Record return** asks which unit you're holding (model and bin shown). If it doesn't match the slip, the app refuses and says to check the label.
3. **Overdue flag.** Slips past their due time show a red **Overdue** tag.
4. **Request status.** On the request form, each approved item shows `unit · with <person> · OVERDUE`, `Returned` or `Not issued`.
5. **Handover draft.** **Draft from outstanding slips** fills the Desk book note with what is still out, who has it and what is overdue. The person edits it and saves.

## The same job with the change

1. 3:45 pm: issue the projector, speaker and adapter AD-12 to Kabir. The request form shows all three as out, with Kabir.
2. 7:30 pm: Kabir returns the projector and speaker. For each, I pick the unit in my hand and the slip closes. The adapter slip stays open, so I click **Hand over → Leela Das**. The request form now says *AD-12 · with Leela Das*.
3. Before leaving, I click **Draft from outstanding slips** in the Desk book. The note already lists the adapter, who has it and that it is due.
4. Sat 9:00 am: the adapter slip is marked **Overdue** and shows *Now with Leela Das*. When she arrives, I click **Record return** and select the unit from her hand. If it's the wrong adapter, the app stops me. If it's right, the slip closes and the request shows everything as returned.

## What I would keep

- The existing guardrails on issuing, unchanged.
- One slip per physical unit.
- The Desk book as the place for human notes. The draft only adds a starting point.
- The simple, single-screen layout. My additions are inline on the existing rows rather than new pages.

## One observation at a real counter

**How often the person starting a shift has to ask someone, or re-read the Desk book, before they can close the right loan.**

At the real counter I would watch each shift change and count those moments. Today I expect at least one per handover (for example, "who has the adapter?"). If the change helps, that count drops to near zero. I would also tally returns where the unit didn't match its slip. Those should now be caught at the counter instead of discovered later.

## Limits and next steps

- Time in this sample is only three fixed moments, so "overdue" is simple. A real version would use real clocks.
- Hand over records a name but not a reason or time. A real desk might want a timestamp.
- There is no condition check on return (damage, missing parts).
- Slips created before this change just show the original person as the current holder.

## Tools used

I used an AI assistant (Claude) to read the code, find problems and help write the change. I decided what the problem was, which change to propose, and I tested it in the running app myself.

## Run the app

Open `index.html` in a modern browser. Or from the repo folder:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit `http://localhost:8000`. **Restart sample shift** resets the records.

## Source

- `index.html` — desk layout, candidate brief, bundled icons.
- `app.js` — sample records and interactions.
- `styles.css` — desktop and mobile layouts.

Icon license notices are in [third-party/lucide-LICENSE.txt](third-party/lucide-LICENSE.txt).
