SmartCare Requirements Specification

1. Problem and Scope
Problem: SmartCare is a small community clinic that currently manages patients, practitioners and appointments using methods such as spreadsheets, paper records and other manual processes.
This has caused a sharp increase in duplicate appointment bookings, difficulty finding patient records, inconsistent appointment status, lacks a manual cancellation process and reliable appointment history.

Scope: The first version (v0.02) is a simple, maintainable software application for a small clinic that supports patient and practitioner appointments. It is not a complex hospital system.

In Scope:
    - Patient record management
    - Practitioner management
    - Appointment management
    - Prevention of duplicate bookings
    - Basic operational reporting
Out of Scope:
    - Online patient self-serve booking portal
    - Online payment processing
    - SMS/Email reminders

2. Stakeholders

| Stakeholder          | Need                                                 | Evidence                                                        |
| Clinic management    | A single maintainable system that produces reliable  | Brief: Management wants a simple software system                |
                         operational reports
| Reception staff      | Quick booking, searching, cancelling and tracking    | Brief: Duplicate bookings, difficulty locating patient records  | 
                         of appointments without creating duplicates or lost
                         records  
| GPs                  | Visibility of their schedules, appointment status    | Brief: Limited visibility of practitioner availability          | 
                         and relevant patient information
| Patients             | Reliable appoinments with no duplicates, easy        | Breif: Duplicate bookings manual cancellation processes         | 
                         cancellation and accurate appoinment history
| IT support           | A simple and easily maintainable system              | Breif: "Does not want a complex hospital information system"    |

3. Functional Requirements
    - FR-01: The system shall allow staff to add a new patent record with a unique patient ID.
    - FR-02: The system shall allow staff to edit an existing patient record
    - FR-03: The system shall allow staff to add and edit GP records
    - FR-04: The system shall allow staff to search for a patient by patient ID or name
    - FR-05: The system shall allow staff to create a new appointment linking one patient, GP, a date and a time and status
    - FR-06: The system shall prevent duplicate appoinment bookings for the same practitioner at the same date and time
    - FR-07: The system shall retain cancelled appoinments in the appointment history
    - FR-08: The system shall allow staff to cancel appointments by changing, changing its status to "cancelled" without deleting the record
    - FR-09: The system shall allow staff to view a patient's full appointment history
    - FR-10: The system shall allow staff to view a GP's schedule and availability for a selected date
    - FR-11: The system shall maintain a consistent appointment status across all views
    - FR-12: The system shall produce basic operational reports, including total appointments, cancellations and booker per GP for a selected period

4. Non-Functional Requirements
    - NFR-01: The system shall remain responsive for the needed time
    - NFR-02: The system shall be usable by reception staff with minimal training, using standard form-based screens with clear labeling
    - NFR-03: The system shall protect patient data with basic access control and shall not expose data beyond what a role requires
    - NFR-04: The system shall retain appointment records and shall not delete data
    - NFR-05: The system shall be designed so that core bsuiness logic is independantly testable from the user interface (Booking, cancellation, duplicate prevention)
    - NFR-06: The system shall be maintainable and modular so that future stages can add features without rewriting or removing existing functionality

5. User Stories
    - US-01: As a receptionist, I want to search for a patient by ID or name, so that I can quickly find the correct patient record
    - US-02: As a receptionist, I want to create an appointment for a patient with a practitioner so that I can book a consultation without double-booking
    - US-03: As a receptionist, I want to cancel an appointment so that the slot is reed and the cancellation is recorded in history
    - US-04: As a GP, I want to view my schedule for a selected date, so that I know which patients I am seeing and when
    - US-05: As clinic management, I want to run a report of appointments and cancellations per practitioner so that I can understand the clinic activity
    - US-06: As a receptionist, I want to view a patient's full appointment history, so that I can answer patient queries accurately

6. Acceptance Criteria
US-02 -- Create appointment (positive)
    GIVEN a patient and a GP exist in the system
    WHEN a receptionist creates an appointment for the patient with the GP on an available date and time
    THEN the appointment is saved with status "Booked" and appears in both the patient history and the GP schedule

US-02 -- Duplicate booking (negative/failure)
    GIVEN a GP already has a booked appointment on 20/09/2026 at 10:00am
    WHEN a receptionist tries to create another appointment for the same GP on the 20/09/2026 at 10:00am
    THEN the system rejects the booking and shows a clear "duplicate booking" message, and no new appointment is created

US-03 -- Cancel appointment (positive)
    GIVEN a booked appointment exists
    WHEN a receptionist cancels the appintment
    THEN the appointment fstatus changes to "cancelled", it remains in history and the slot is freed for new bookings

7. Assumptions and Open Questions
Assumptions:
    - Staff will use a shared desktop application accessed via staff login
    - The data set will be small (hundreds, not millions of records), so a simple local data store is acceptable
    - Each appointment links exactly one patient with one GP at one date/time
Open questions:
    - Are SMS or email reminders required
    - What specific appointment statuses are needed beyond booked, cancelled and completed
    - What is the exact list of fields required on a patient record and a GP record
    - Should reports be exportable as PDF's

8. AI Requirements Review Record
Prompt used: "Act as a software requirements reviewer. Review the SmartCare requirements for ambiguity, inconsistency, missing clarification questions and testability. Do NOT invent new client requirements. For every suggestion, state whether it is based on evidence or is only a question/assumption requiring validation."

| AI suggestion                       | Evidence                     | Reason                                                       | Verification                                     |
| Clarify cancellation status change  | Inferred from brief          | AI correctly distinguished soft vs hard deletion             | FR-07 and FR-08                                  |
| Clarify appointment status values   | Inferred                     | AI flagged missing status taxonomy                           | Added to open questions                          | 
| Make "responsive" measurable        | Inferred from brief          | AI noted "responsive" was vague                              | Reflected in NFR-01                              |
| SMS/email reminders                 | No direct evidence in brief  | Brief does not mention reminders                             | Confirm with management before any future stages | 
| Access control for patient data     | Inferred from brief          | AI noted "securely manage data" was vague                    | Reflected in NFR-03                              |
| Facial recognition login            | No evidence; out of scope    | Small clinic system; biometric auth adds to much complexity  | Not required                                     |
| Online payment                      | No evidence; out of scope    | Brief doesn't mention payment handling                       | Out of scope                                     |