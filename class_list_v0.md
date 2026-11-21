# Class list v0 — Le Tien Binh · G04

Continued from lecture slide 54. Each class answers: **what does the model need to recognize this for?**

## DMS (driver monitoring)

| # | Class / attribute | Values | What it is for (DMS function) | Visible on IR? |
|---|---|---|---|---|
| 1 | eye_state (per eye) | open / closed / unknown | Drowsiness: eyes closed for too long (PERCLOS), micro-sleep alerts | Yes, unless a lens reflection, dark sunglasses or a bowed head hides the slit (D01, D06) |
| 2 | face13 keypoints | 13 points with occluded / outside flags | Head pose and eye/mouth opening; input for drowsiness and yawning measures | Yes on real NIR; points behind glasses frames or a hand get flags |
| 3 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Distraction: eyes off the road for longer than a time threshold | Partly: head direction is visible, the exact gaze is often uncertain → other |
| 4 | phone | held / mounted / lap | Phone-use distraction warning (calling, texting) | Yes by shape when an edge or screen is visible; not when the hand covers it |
| 5 | hand + on_wheel | side left/right (of the person) · yes / no / unknown | Hands-off-wheel warning; takeover readiness in assisted / automated driving | Yes; the wheel rim is visible in NIR |
| 6 | glasses | none / clear / sun / unknown | Tells the model when eye state is unreliable; adapts IR exposure | Partly: sunglasses can look transparent in NIR, so unknown when unsure |
| 7 | seatbelt (driver) | worn_correct / worn_incorrect / not_worn / unknown | Seat-belt reminder; detect a belt worn under the arm | Yes as a diagonal band, unless dark clothing hides it |
| 8 | person (driver present) | seat = driver | Driver-presence check before engaging assistance features | Yes |

## OMS (occupant monitoring)

| # | Class / attribute | Values | What it is for (OMS function) | Visible on IR? |
|---|---|---|---|---|
| 1 | person + seat | driver / front_passenger / rear_left / rear_middle / rear_right | Occupancy per seat: rear seat-belt reminder, airbag and climate per seat | Yes |
| 2 | child_seat + occupied | seat · yes / no / unknown | Child-presence detection (child left in a parked car); airbag suppression | Yes by shape (high back, wings); not by color |
| 3 | infant_seat + facing | seat · rear / front | Disable the front airbag for a rear-facing carrier; child-presence alert | Yes by shape (carrier handle, low shell) |
| 4 | seatbelt (passenger) | worn_correct / worn_incorrect / not_worn / unknown | Rear seat-belt reminder (a regulatory requirement in many markets) | Partly: dark belts on dark clothes fade in IR |
| 5 | object + type | bag / box / cup / other | Forgotten-item reminder; avoid counting a bag as an occupant | Yes by shape |
| 6 | empty seat count | number per frame (note) | Calibrate occupancy: an empty seat is not an error class | Yes |
| 7 | face (passenger) | box only | Count occupants and attach a seat; future age / attention estimates | Yes |

## 2 escalation questions

Questions for the guideline author because Guideline v1.0 does not answer them. Each has an **example frame**.

1. Question: The guideline says the set has no seated children, but several SVIRO scenes show a child-like figure in a child seat or infant carrier. Should the child get `person` + `face`, and which `seat`? Should `infant_seat` also get an `occupied` attribute, like `child_seat` now has `yes`?
   Example frame: G04 S03_rgb / S03_ir (child in the `rear_right` child seat, baby in the `rear_left` carrier); also S01, S04, S05, S08.
   How I labeled it for now and why: I did not draw `person`/`face` for the child (GUIDE §3: "report to the coach, do not label") and set the seat's `occupied = yes` after the mentor added that value. The infant carrier has no occupancy attribute, so I noted it here.

2. Question: Should `face.gaze_zone` and the eye attributes be filled for rear passengers in OMS frames? The zones (road, mirrors, cluster) describe the driver's field of view, and §4.1 says OMS faces are "box only".
   Example frame: G04 S02_rgb / S02_ir (an adult in `rear_left` looking toward the side window).
   How I labeled it for now and why: I drew the face box, kept `gaze_zone = other` so the model is not taught driver zones on passengers, and filled the eye and glasses attributes only from what is visible in each frame.
