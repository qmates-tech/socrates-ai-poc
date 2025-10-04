### Goal
We have to build a  webapp to simplify the registration of Socrates Italy conference events.
Link: https://www.socrates-conference.it/ . The application will let the user register by filling the booking form with proper data (see the examples below). The app will serve 3 kinds of users: hotel backoffice user, event organizer user, and participant user with different behaviours.

### Constraints and Rules
- language typescript backend-frontend
- use next.js
- avoid to use “any” reserved word
- prefer async await
- use sqlite
- use self explained names
- This webapp is a POC (proof of concept), so prefer concrete solutions with something hazard coded rather than flexible and generic abstractions.



### Quality standards and Design Rules
- Copy the style from the actual website
- **Self-Documenting Code:** Prioritize **descriptive names** for variables, functions, and classes. 
- **SOLID Principles:** Ensure the code strictly adheres to:
    * **Single Responsibility Principle
    * **Open/Closed Principle
    * **Liskov Substitution Principle
    * **Interface Segregation Principle
    * **Dependency Inversion Principle
- **Design Principles:**
    * **KISS:** Keep It Simple, Stupid.
    * **Separation of Concerns:** Clearly separate domain logic, application logic, and infrastructure. Default to a **Clean/Hexagonal Architecture**.
* **Single Level of Abstraction:** Functions and methods should do one thing and operate at a single level of abstraction.

### How we work - development process
We implement features step by step. Each development cycle implements only one feature. Each feature has a working solution and the automated tests to certify them: follow the criteria below.
Before writing any code, your primary goal is to **understand the requirements**.

* **Question Everything:** Actively question the request to uncover ambiguities, edge cases, and missing details.
- limit the assumption you make, only when there is ambiguity ask for clarifications. 


### Example of use cases (and acceptance criteria)
#### Scenario Availability check (guest user)
The user accesses the conference website and opens the registration page.
The system shows available rooms and event slots with the current remaining capacity.
If the maximum registrations limit is reached, the system blocks further attempts and shows a “No availability” message.
Acceptance criteria:
- Guest sees the total available slots for the event.
- Guest sees the available hotel room options.
- If no slots are available, the system prevents proceeding to booking.
#### Scenario Registration / Request booking (guest user)
The user fills the booking form with personal details (name, surname, email, phone), selects event slot and hotel room type.
The system validates mandatory fields and checks availability.
Upon success, the system saves the booking as “pending payment” and triggers three confirmation emails:
To the participant (booking summary, payment info).
To the hotel desk (new pending booking).
To the event organizer (updated participants count).
Acceptance criteria:
- User cannot confirm booking with missing mandatory fields.
- User receives confirmation email.
- Hotel desk and event organizer receive notification.
- Booking is marked “pending payment” until backoffice updates it.
####Scenario Set availability (event organizer)
Event organizer logs into backoffice.
Organizer sets the maximum number of registrations allowed for the event.
Organizer updates availability for specific workshops or sessions.
System applies changes immediately and reflects them in guest availability check.
Acceptance criteria:
- Organizer can modify event capacity.
- Capacity updates are immediately visible to guest users.
- Once limit is reached, system blocks new bookings automatically.
#### Scenario Register payment (hotel backoffice user)
Hotel backoffice user logs into hotel backoffice.
User sees the list of pending bookings.
User selects a booking and marks it as “paid”.
System updates booking status and triggers an email to the participant confirming payment.
Event organizer also receives updated participant status.
Acceptance criteria:
- Backoffice user can change booking status from pending to paid.
- Participant receives payment confirmation email.
- Organizer is notified of confirmed participant.
#### Scenario Cancel booking (participant user)
Participant logs in with their booking reference.
Participant requests cancellation.
System updates booking status to “cancelled” and frees the slot if within allowed cancellation window.
Emails are triggered to participant, hotel backoffice, and event organizer.
Acceptance criteria:
- Cancellation not allowed after event start date.
- Slot becomes available again if cancelled before deadline.
- All parties notified of cancellation.
