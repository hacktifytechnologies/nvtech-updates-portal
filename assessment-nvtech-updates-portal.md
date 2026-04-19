# Assessment — NVTech Work Updates Portal

---

## Question 1 — MCQ

**What information is improperly exposed during the password reset flow?**

- A) The user's hashed password returned in the API response
- B) The OTP sent to the user's registered email address
- C) **The authorized reset token displayed directly in the UI** ✅
- D) The user's session cookie logged in the browser console

> **Answer:** C — The `/forgot-password` page displays the user's reset token (e.g., `NV-ANITA-8821`) directly in the UI without requiring email verification, allowing anyone who knows a valid username to take over the account.

---

## Question 2 — MCQ

**What encoding scheme is used for the `id` parameter in the profile URL, and why does it fail to provide security?**

- A) Base58 — difficult to decode without the right library
- B) ROT13 — obscures the value but is reversible without a key
- C) AES encryption — secure encoding but the key is leaked
- D) **Base64 — trivially reversible and provides no access control on its own** ✅

> **Answer:** D — Base64 is an encoding, not encryption. The value `MQ==` decodes to `1`, `Mg==` to `2`, and so on. The application decodes the ID but does not verify that the requesting user owns the profile, making enumeration trivial.

---

## Question 3 — MCQ

**What Base64-encoded value must be supplied in the `id` parameter to access user ID 5's profile?**

- A) `NA==`
- B) `Mw==`
- C) `RA==`
- D) **`NQ==`** ✅

> **Answer:** D — The integer `5` encoded in Base64 is `NQ==`. Supplying `/profile?id=NQ==` bypasses the authorization check and returns Arjun Kapoor's profile, which contains the confidential project assignment.

---

## Question 4 — Fill in the Blank

**What Base64 value for the `id` parameter reveals the profile containing the confidential project details?**

**Answer:** `NQ==`

> `NQ==` is the Base64 encoding of the integer `5`. Accessing `/profile?id=NQ==` returns Arjun Kapoor's profile including his confidential assignment to the high-priority internal project.

---

## Question 5 — Fill in the Blank

**What is the name of the confidential project discovered by exploiting the IDOR vulnerability on the profile endpoint?**

**Answer:** `Project Helix`

> Arjun Kapoor's profile (accessed via IDOR at `id=NQ==`) reveals his confidential assignment: "Project Helix — Blockchain research, High-priority." This project name is the key piece of intelligence linking to the next challenge in the chain.

---

*Lab target:* `http://localhost:80`
