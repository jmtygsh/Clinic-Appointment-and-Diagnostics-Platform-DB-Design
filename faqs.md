# FAQ

## Who are the doctors and what are their specialties?

Doctors are stored in the `doctor` table and linked to the `specialty` table using `doctor.specialty_id`.

Example:

* Dr. Amit Sharma → Cardiology
* Dr. Neha Verma → Dermatology

---

## Which patient booked which appointment?

Appointments are stored in the `appointment` table.

Each appointment links:

* `patient_id` → patient
* `doctor_id` → doctor

This shows which patient booked with which doctor.

---

## What was the appointment status?

Stored in `appointment.status`

Possible values:

* scheduled
* completed
* cancelled
* no_show

This helps track booking outcome.

---

## Did the appointment result in a consultation?

Check the `consultation` table.

If a row exists with matching `appointment_id`, then the appointment became an actual consultation.

If no row exists, it did not result in a visit.

---

## Were any diagnostic tests prescribed?

Check `consultation_test`.

If rows exist for a consultation, then tests were prescribed.

Examples:

* Blood Test
* X-Ray
* ECG

---

## What reports were generated?

Reports are stored in `report`.

Each report links to a prescribed test using:

* `report.consultation_test_id`

This shows completed diagnostic reports.

---

## Can one patient have many visits?

Yes.

Relationship:

* One patient → Many consultations

Stored using:

* `consultation.patient_id`

A patient may visit multiple times over months or years.

---

## Can one doctor attend many patients?

Yes.

Relationship:

* One doctor → Many consultations
* One doctor → Many appointments

Stored using:

* `consultation.doctor_id`
* `appointment.doctor_id`

---

## Can one consultation lead to multiple tests?

Yes.

One consultation can prescribe many tests.

Stored in:

* `consultation_test`

Example:

One visit may require:

* Blood Test
* X-Ray
* Sugar Test

---

## How should payments be connected to visits or appointments?

Payments are stored in `payment`.

Flexible structure:

* `appointment_id` = payment during booking
* `consultation_id` = payment after visit

This supports real clinic billing flow.
