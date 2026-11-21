# AI usage declaration — Le Tien Binh (2A202603346)

Image set: **G04**. Tool: **Claude (Claude Code, desktop app)** for every row below.

## Part 1 — Questions I asked for reference

| # | What I asked (summary) | How I used the answer | Did I verify it? How? |
|---|---|---|---|
| 1 | Which file defines the labels I must use, and what are the 9 labels and their attributes? | Used it as a map of `labels_cabin_v1.json` and GUIDE §4.1–4.2 before labeling | Read both files myself |
| 2 | Is `person` / `face` only for adults? What to do with the child-like figures in S01, S03, S04, S05, S08? | Did not label the children; collected the cases as a question for the coach | GUIDE.md lines 53, 75–76, 90 |
| 3 | Which part of the guideline says `child_seat` is for an empty seat, and what does `occupied` mean? | Set `occupied` from what each frame shows | GUIDE.md lines 80, 90, 92, 154 |
| 4 | What is `infant_seat`, how is it different from `child_seat`, and how do I choose `facing`? | Changed the carrier in S03 to `infant_seat`; chose `facing` by where the shell opens | GUIDE §4.1, §4.8; checked the shape in CVAT |
| 5 | How do the `occluded` and `outside` flags work on face13 points? | Flagged hidden eye points on D01/D06 and set those eyes to `unknown` | GUIDE §4.6 and the rules in `scripts/cabin_check.py` |
| 6 | How do I label the left and right eye, especially on the rotated D## frames? Is it by the person or by the image? | Labeled left/right by the person; checked that the left eye has the larger y on D## | GUIDE §4.4 rule 2, §4.6; CHECKPOINTS Checkpoint B |
| 7 | What does `gaze_zone` mean and how do I pick a zone (D01, D04)? | Chose the zone myself per frame; `other` when unsure | GUIDE §4.5 |
| 8 | When is `glasses` none / clear / sun / unknown? | Used `unknown` when the eye area was not clear; `clear` for see-through lenses on NIR | GUIDE §4.5 |
| 9 | Do OMS frames need `hand` boxes or full face attributes? | No `hand` on S##; OMS faces are box only, `gaze_zone = other` | GUIDE §4.1 "Used in" column and §4.3 |
| 10 | Do I need separate tasks for RGB and IR? Why are S09–S10 missing from my task? | Kept one task with the 22 core images; skipped the optional S09–S10 | GUIDE Task 0 and RUBRIC "extension" section |
| 11 | How do I edit the project labels safely after the mentor added `occupied = yes`? | Added `"yes"` to the attribute with id 138 in the CVAT Raw tab (kept the ids) | Opened a `child_seat` box afterwards and saw the new value |
| 12 | Why did my push script fail with a 502 error, and where is the terminal password prompt? | Waited for CVAT to finish restarting, then typed the password myself | Re-ran the command; the task was created |
| 13 | What do I still need to do after labeling, and what goes in each submission file? | Followed the order: export → check → peer diff → written files → submit | SUBMISSION.md, CHECKPOINTS.md |

## Part 2 — Other AI help in this lab

| # | What the AI did | How I used it | How I verified it |
|---|---|---|---|
| 1 | Updated `labels_cabin_v1.json` and `scripts/cabin_schema.py` with the mentor's `occupied = yes`; ran `cabin_check` on my exports and pointed out conflicts | Fixed `light` on S##_rgb, eye flags on D01/D06, S03/S04 pairs in CVAT, then re-exported | Re-ran `cabin_check` myself |
| 2 | Drafted `ir_log.csv`, `class_list_v0.md`, `self_review.md`, `TEAM.md`; translated `exit_ticket.md` and the check output into English | Edited the drafts before submitting. Exit ticket answers are my own | Compared each row with my labels and the images |
