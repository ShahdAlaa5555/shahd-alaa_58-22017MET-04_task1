# Task 1 — Inconsistencies and duplicates

**Name:** Shahd Alaa Ahmed  
**ID:** 58-22017  
**Major / Lab:** <MET> / 04

## Part C — What I did

The file had 39 sign-ups. I first looked at shape, dtypes and `value_counts()`: faculty, club and city had 13, 13 and 9 spellings instead of 5, 5 and 3 (case, spaces, abbreviations such as *Alex*, *Pharma*, *Soccer*, *Debating*, *Chess Club*). I lower-cased and stripped them, mapped the rest with explicit dictionaries to the canonical values, and asserted nothing else remained. Names got single spaces and Title Case; emails were trimmed and lower-cased. `fee_paid` (yes/Y/TRUE/1/no/N/false/0) became a real boolean. `signed_up_at` mixed `YYYY-MM-DD HH:MM` and `DD/MM/YYYY HH:MM`; slash dates like 18/09/2026 prove the first number is the day, so I parsed each format explicitly and kept the time. I removed **3** exact duplicates (39 → 36) and **4** repeated sign-ups for the same student and club (36 → 32), leaving **32** rows, then asserted `student_id + club` is unique. I kept the latest submission because students come back to update their record, usually to mark the fee as paid, so the first copy would restore an outdated "unpaid". Order matters: on raw text, `Debate` and `debate club` (Laila), or `Music` and `music` (Ali), look like different clubs. Removing duplicates before fixing spellings found only **2** of the 4 repeated sign-ups and left 34 rows, not 32. Two different students are both named Mohamed Adel (61-4844 and 55-2992); I deduplicated only on `student_id` + `club`, never on name, so they stay separate.

## Files

- `task1.ipynb` — the cleaning, run top to bottom
- `club_signups.csv` — the original file, unchanged
- `club_signups_clean.csv` — the result (32 rows)
