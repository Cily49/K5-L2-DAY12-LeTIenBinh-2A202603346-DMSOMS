# TEAM — Day 12

Image set: **G04** · Mode: individual

| Name | Student ID | Labeled all 22 images? | Cross-review with (peer diff) | Disagreement rows resolved |
|---|---|---|---|---|
| Le Tien Binh | 2A202603346 | yes | <peer name, G04> | <n> |

Cases we still disagreed on and asked the coach about (image + object):

- G04 S01, S03, S04, S05, S08 (`_rgb` and `_ir`): a child-like figure sits in a `child_seat` / `infant_seat`. GUIDE §3 says the set has no seated children. Should the child get `person` + `face`? I did not label the child and set the seat's `occupied` accordingly while waiting for the answer.
- <add rows from the peer diff if any remain unresolved>

## Individual

### LeTienBinh-2A202603346
- My part (besides my own 22 images): built and ran a local pre-labeling tool (mentor approved), reviewed all 22 images by hand in CVAT, collected the child-in-seat questions for the coach.
- What I learned today: left/right always follows the person, not the image. On the rotated D## frames the left eye has the larger y. And when I cannot see something, `unknown` is the correct label, not a guess.
