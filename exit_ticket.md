# Exit ticket — Day 12

Individual, no slides, about 10 minutes. Write the answer right under each question.

**Name:** Le Tien Binh · **Set:** G04

---

**Question 1 · Choose one.** Many cars' DMS cameras shine their own near-infrared LED light, around 940 nm, onto the driver's face. What is the main reason?

- A. To measure skin temperature and detect a fever
- B. To get a stable face image day and night without dazzling the driver
- C. To get nicer color images for video calls
- D. To let the camera see through every kind of sunglasses

Answer: **B**. The 940 nm LED is invisible to the eye, so the face is lit evenly day and night without dazzling the driver. It does not measure temperature (A), gives no color (C), and does not see through every sunglasses lens (D).

**Question 2 · Number, 2 decimal places.** A DMS camera runs at 30 frames per second. The model estimates the driver's head yaw above 30° continuously from frame 240 to frame 314, **including both frame 240 and frame 314**. For how many seconds was the driver not looking at the road?

Answer: **2.50 s**. Frames 240 to 314 inclusive = 314 − 240 + 1 = 75 frames; 75 / 30 fps = 2.50 s.

**Question 3 · Choose all correct answers.** Which statements are true about cabin data compared with outside-camera data?

- A. You cannot blur the driver's face the way you blur pedestrians, because the DMS model needs the face itself.
- B. At night, cabin images are usually black-and-white infrared, so a clothing-color attribute cannot be labeled.
- C. The OMS camera looks toward the rear of the car, so the seat on the left of the image is the car's right seat.
- D. Objects in a cabin are usually far away and small, with many objects per image.
- E. The cabin scene is fixed, so it needs no separate guideline or QC.

Answer: **A, B, C**. D is false: cabin objects are close to the camera and large, with few per image. E is false: cabins need their own guideline and QC (seat naming by car, left/right by person, IR rules).
