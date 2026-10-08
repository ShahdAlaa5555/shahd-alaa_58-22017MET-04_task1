# Task 1 — Inconsistencies and duplicates

**Name:** Shahd Alaa Ahmed  
**ID:** 58-22017  
**Major / Lab:** <MET> / 04

## Part C — What I did

The file had 39 sign-ups. I first looked at shape, dtypes and `value_counts()`: faculty, club and city had 13, 13 and 9 spellings instead of 5, 5 and 3 (case, spaces, abbreviations such as *Alex*, *Pharma*, *Soccer*, *Debating*, *Chess Club*). I lower-cased and stripped them, then mapped the rest with explicit dictionaries to the canonical values and asserted that nothing else remained. Names got single spaces and Title Case, emails were trimmed and lower-cased. `fee_paid` (yes/Y/TRUE/1/no/N/false/0) became a real boolean through a dictionary. `signed_up_at` mixed `YYYY-MM-DD HH:MM` and `DD/MM/YYYY HH:MM`; slash dates such as 15/09/2026 prove the first number is the day, so I parsed each format explicitly and kept the time. I then removed **3** exact duplicate submissions (39 → 36) and **4** repeated sign-ups for the same student and club (36 → 32), so **32** rows remain, and asserted `student_id + club` is unique. I kept the latest submission because students come back to update the record, usually to mark the fee as paid, so the last one is the current truth; the first one would restore an outdated "unpaid". Order matters: on the raw text, `Chess` and `Chess Club`, or `Music ` and `Music`, are different clubs, so a duplicate check done first finds only **<N>** of the 4 repeated sign-ups and leaves **<4 − N>** wrong rows behind. Finally, two different students are both called Mohamed Adel (61-4844 and 55-2992); I never deduplicated on name or email, only on `student_id` + `club`, so they stay separate.

## Files

- `task1.ipynb` — the cleaning, run top to bottom
- `club_signups.csv` — the original file, unchanged
- `club_signups_clean.csv` — the result (32 rows)
