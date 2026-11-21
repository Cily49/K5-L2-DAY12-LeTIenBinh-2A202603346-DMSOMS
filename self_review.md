# Self review — Le Tien Binh · G04

## 1. Self-check of 4 scenes

Four images (2 S##, 2 D##) re-read as a stranger would. Each row is an error that `cabin_check` or my own pair check really found on the first `export_final.zip`.

Error types: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (face left/right), `flag` (missing point flag), `ok`.

| Image | Object | Error type | Note | Fixed? |
|---|---|---|---|---|
| S01_rgb | frame_meta | guess | `light = day` on a rendered SVIRO frame; GUIDE §3 says rendered images are `light = unknown`. The same mistake was on all 8 S##_rgb frames | yes |
| S03_rgb | child_seat (both) | guess / wrong_class | `occupied = no` although children are visible, which contradicted S03_ir (`yes`). The seat on the right of the image is a carrier with a handle → changed to `infant_seat` on both frames | yes |
| D01 | face / face13 | flag | `eye_right = open` while all 4 right_eye_* points were flagged as hidden → changed to `unknown` | yes |
| D06 | face / face13 | flag | Both eyes `open` while all 8 eye points were hidden (glasses + head bowed) → both `unknown` | yes |

After the fixes, `cabin_check --expect 22` reports 0 errors and 1 warning (D02). The warning is explained in `check_final.txt`: on the rotated D## frames the left eye has the larger y.

Note: `check_cpA.txt` and `check_cpB.txt` were generated after the session from the final export (`--only S01,S02` and `--only D01,D02`), not during the checkpoints.

## 2. The mistake I repeated most today

Mistake: setting `frame_meta.light` from how bright the scene looked (`day` / `night`) on the SVIRO RGB frames, on all 8 of them.

Why I made it: the renders look like real daytime or night photos, so I judged by eye and forgot the rule that SVIRO frames are computer-rendered and always `light = unknown`.

How I will avoid it next time: fill `frame_meta` first with a short per-dataset checklist (SVIRO: `light = unknown`, `seatbelt` only `not_worn`/`unknown`), and run `cabin_check --only` after the first two frames instead of only at the end. That would have caught the error on S01 before it repeated 7 more times.

## 3. Note on disagreement_log

Peer: Chu Tuan Ngoc (G04), 63 rows in `disagreement_log.csv`.

One row where my peer was right and I was wrong: none. After re-checking each row in CVAT I kept my label on all 63 rows. The rows I looked at most carefully were `infant_seat.facing` on S03/S05 (rear vs front) and `gaze_zone` on D02–D04 (road vs lap), because a different reading of the image was plausible there.

What I learned from the log: two people agreeing only shows consistency, not correctness (RULES §1), so I wrote the guideline section next to every verdict. That way the coach can judge each row against the guideline instead of against either of us.
