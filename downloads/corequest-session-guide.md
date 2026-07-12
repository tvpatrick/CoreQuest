# CoreQuest Session — Team Guide

CoreQuest Session is the asynchronous team version of the CoreQuest workshop: each person contributes answers under their own name, colleagues build on each other's attributed notes, and the AI Context Pack is generated with provenance assembled automatically. The session lives in a `.json` file your team owns — nothing is uploaded anywhere.

This guide covers how to run it as a team, including the AI merge prompt for combining parallel sessions.

*Part of the CoreQuest Workshop © Teresa Patrick, licensed under [CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0).*

---

## Two ways to run a team session

### The Relay (recommended)

One session file travels through the team, accumulating answers. No duplicate answers are possible, because each person sees everything written so far — and reading colleagues' attributed answers is often the best prompt for your own.

1. **First contributor:** open the Session page, enter your name and role, fill in the session setup (company, product, selected customer), add your answers, and click **Export session**. Save the file to your team's shared drive.
2. **Each next contributor:** open the Session page, click **Import session file(s)**, select the file from the shared drive, enter your own name, read what's there, add your answers — using *Build on this* wherever a colleague's note sparks yours — and **Export session** again, replacing the file in the shared drive.
3. **Last contributor (or the organizer):** generate the outputs — the AI Context Pack, the marketing first pass, and the AI drafting prompt.

**Naming tip:** keep one canonical file, e.g. `acme-corequest-session-latest.json`. Whoever exports, replaces it. If your shared drive keeps version history (Google Drive, Dropbox, SharePoint all do), you get a full audit trail for free.

### The Fan-out (parallel, faster — needs a merge)

Everyone answers at the same time in their own blank session, and a facilitator combines the results. Faster for busy teams, but it produces overlapping answers: two colleagues will independently make the same point in different words. That's what the merge prompt below is for.

1. **Everyone:** open the Session page fresh, enter your name, fill in the same company/product/customer (agree on these up front), add your answers, and export. Name your file with your initials and the date: `acme-corequest-session-2026-07-15-tp.json`. Put it in the shared folder.
2. **Facilitator:** open the Session page, click **Import session file(s)**, and select *all* the files at once. The tool merges them automatically — every answer, every name. Export the combined file.
3. **Facilitator:** run the combined file through the **AI merge prompt** below to consolidate duplicate points and combine credit. Save the AI's output as `acme-corequest-session-latest.json`.
4. **Facilitator:** import the cleaned file back into the Session page to verify it loads, then generate the outputs — or send it around for one more relay pass so everyone can react to the combined picture.

---

## The AI Merge Prompt

Copy everything in the block below into Claude, ChatGPT, or Gemini, then attach or paste the combined session file (or several files) after it. Save the AI's output as a new `.json` file and import it into the Session page to verify.

```
You are consolidating CoreQuest Session files. Each file is JSON with this schema:

{ "schema": "corequest-session/1", "company": "", "product": "", "customer": "",
  "entries": [ { "id": "", "ws": 1-11, "text": "", "author": "", "role": "", "ts": 0, "buildsOn": "optional id" } ] }

Your task:
1. Combine all entries from all files I provide into one list. Entries with identical "id" values are the same entry — keep one copy.
2. Within each worksheet number ("ws"), find groups of entries that make substantially the same point in different words.
3. For each such group, keep ONE entry:
   - Use the clearest wording from the group. You may lightly combine wording, but never add claims that are not in the originals.
   - Set "author" to credit every contributor in the group, e.g. "Maria Chen (Sales Engineering) & Raj Patel (Product)". Set "role" to "".
   - Keep the "id" and "ts" of the earliest entry in the group.
4. If a removed entry's "id" is referenced by another entry's "buildsOn", change that reference to the kept entry's id.
5. Be conservative: entries on similar topics that make DIFFERENT points are not duplicates — keep both. When unsure, keep both. Never drop a unique insight. Never remove or alter attribution except to combine it as described.
6. For "company", "product", and "customer", use the most complete non-empty values across the files.
7. Output exactly one valid JSON object matching the schema above, in a single code block, with no commentary before or after and no comments inside the JSON.

Here are the session files:
```

**After the merge:** import the cleaned file into the Session page and skim each worksheet. The AI is conservative by instruction, but you are the editor of record — if it merged two answers that were actually different points, the original files are still in your shared folder; nothing is ever lost.

---

## Practical notes

- **Everyone sees everything.** Importing a session shows all prior answers with their authors' names. That's the point: attributed answers prompt better answers, and *Build on this* records the chain of credit.
- **Agree on the selected customer first.** Worksheets 2–6 all focus on one customer from Worksheet 1. In a fan-out, decide who that is before people start, or you'll merge apples and oranges.
- **Your name is your signature.** Use the same name spelling every time you contribute, or the contributor list will count you twice.
- **The file is the truth.** There are no accounts and no server. If the file is deleted from your shared drive and nobody exported a copy, the session is gone — treat `-latest.json` like the working document it is.
- **Import errors** almost always mean the file was edited by hand or the AI merge output wasn't saved as plain JSON. Re-save the AI's code block exactly as given, with a `.json` extension, and try again.
