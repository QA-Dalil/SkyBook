# SkyBook Bug Reports

Bug proposals describe observable behavioral defects, not inferred source-code causes. The same adult-minimum defect is linked to both affected test cases. Related datasets for the same constraint share one bug; separate validation constraints retain distinct proposals. Severity reflects the booking impact if this practice behavior were used in a real system, not an actual financial loss during this execution.

| Bug ID | Bug Title | Severity | Affected Story | Affected TC(s) |
| --- | --- | --- | --- | --- |
| BUG-01 | Search accepts identical origin and destination | High | US-1.1 | TC-1.1-02 |
| BUG-02 | Round-trip search accepts return before departure | High | US-1.1 | TC-1.1-04 |
| BUG-03 | Flight search accepts past departure and return dates | High | US-1.1 | TC-1.1-05 |
| BUG-04 | Adult selector permits zero adults and search accepts the booking | High | US-1.1, US-1.2 | TC-1.1-06, TC-1.2-01 |
| BUG-05 | Search accepts more infants than adults | High | US-1.2 | TC-1.2-02 |
| BUG-06 | Price sorting places expensive flights before cheaper flights | Medium | US-2.1 | TC-2.1-01 |
| BUG-07 | Nonstop only filter retains one-stop flights | Medium | US-2.2 | TC-2.2-01 |
| BUG-08 | Passenger details accepts email without a domain | Medium | US-3.1 | TC-3.1-02 |
| BUG-09 | Passenger details accepts a six-digit phone number | Medium | US-3.1 | TC-3.1-02 |
| BUG-10 | Passenger details accepts a future date of birth | High | US-3.2 | TC-3.2-02 |
| BUG-11 | Adult passenger accepts a child-age date of birth | High | US-3.2 | TC-3.2-02 |
| BUG-12 | Passport expiry before departure is accepted | High | US-3.3 | TC-3.3-02 |
| BUG-13 | Two passengers can hold the same seat | High | US-4.1 | TC-4.1-01 |
| BUG-14 | Continue to extras enables before all required passengers are seated | High | US-4.2 | TC-4.2-01 |
| BUG-15 | Negative baggage quantity reduces the booking price | High | US-5.1 | TC-5.1-01 |
| BUG-16 | Baggage control permits twenty bags without a sane upper bound | Medium | US-5.1 | TC-5.1-01 |
| BUG-17 | Repeated SAVE10 application accumulates discounts | High | US-5.4 | TC-5.4-01 |
| BUG-18 | Invalid TEST promo is reported as successfully applied | Medium | US-5.4 | TC-5.4-02 |
| BUG-19 | Removing SAVE10 leaves the discounted total displayed | High | US-5.4 | TC-5.4-03 |
| BUG-20 | Payment completes with cardholder name and ZIP blank | High | US-6.1 | TC-6.1-02 |
| BUG-21 | Payment accepts an expired card | High | US-6.1 | TC-6.1-02 |
| BUG-22 | Payment accepts short, long and nonnumeric CVV values | High | US-6.1 | TC-6.1-02 |
| BUG-23 | Payment completes without fare-rules acceptance | High | US-6.2 | TC-6.2-01 |
| BUG-24 | Start a new booking retains prior trip, cabin and passenger counts | Medium | US-7.3 | TC-7.3-01 |

### Unique bug proposals — FAIL tests only

#### BUG-01 — Search accepts identical origin and destination

Bug ID Placeholder: BUG-01

Bug Title: Search accepts identical origin and destination

Severity: High

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult.

Exact Reproduction Steps:
1. Select Vellamar (VLM) in both From and To.
2. Select One way; keep departure 2026-09-28, 1 Adult and Economy.
3. Click Search flights.

Expected Result:
Block the search and explain that origin and destination cannot be the same.

Actual Result:
VLM→VLM flight results appeared without validation; example VJ 485 $1,158.

Affected Story/Stories: US-1.1

Affected Test Case(s): TC-1.1-02

Evidence:
VLM→VLM flight results appeared without validation; example VJ 485 $1,158.

Recommended Jira Links:
- Bug relates to TC-1.1-02
- Bug relates to US-1.1

#### BUG-02 — Round-trip search accepts return before departure

Bug ID Placeholder: BUG-02

Bug Title: Round-trip search accepts return before departure

Severity: High

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult.

Exact Reproduction Steps:
1. Select Round trip, VLM→HDX, 1 Adult and Economy.
2. Set departure 2026-09-30 and return 2026-09-20.
3. Click Search flights.

Expected Result:
Reject a return date before departure with clear validation.

Actual Result:
Outbound results appeared; itinerary showed Wed, Sep 30 · Return Sun, Sep 20.

Affected Story/Stories: US-1.1

Affected Test Case(s): TC-1.1-04

Evidence:
Outbound results appeared; itinerary showed Wed, Sep 30 · Return Sun, Sep 20.

Recommended Jira Links:
- Bug relates to TC-1.1-04
- Bug relates to US-1.1

#### BUG-03 — Flight search accepts past departure and return dates

Bug ID Placeholder: BUG-03

Bug Title: Flight search accepts past departure and return dates

Severity: High

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult. Execution date 2026-09-07.

Exact Reproduction Steps:
1. Select Round trip, VLM→HDX, 1 Adult, Economy.
2. Set departure 2026-09-01 and return 2026-10-05; search.
3. Return to search; set departure 2026-09-28 and return 2026-09-01; search.

Expected Result:
Reject either past travel date with validation.

Actual Result:
Both searches opened flight results with the past dates retained in the itinerary.

Affected Story/Stories: US-1.1

Affected Test Case(s): TC-1.1-05

Evidence:
Both searches opened flight results with the past dates retained in the itinerary.

Recommended Jira Links:
- Bug relates to TC-1.1-05
- Bug relates to US-1.1

#### BUG-04 — Adult selector permits zero adults and search accepts the booking

Bug ID Placeholder: BUG-04

Bug Title: Adult selector permits zero adults and search accepts the booking

Severity: High

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult.

Exact Reproduction Steps:
1. Use Round trip with valid dates 2026-09-28 and 2026-10-05.
2. Click Adult minus at 1.
3. Observe 0 Adults, then click Search flights.

Expected Result:
Adults must remain within 1–9 and a search must require at least one Adult.

Actual Result:
Adults decreased 1→0; search displayed results and an itinerary with 0 passenger(s).

Affected Story/Stories: US-1.1, US-1.2

Affected Test Case(s): TC-1.1-06, TC-1.2-01

Evidence:
Adults decreased 1→0; search displayed results and an itinerary with 0 passenger(s).

Recommended Jira Links:
- Bug relates to TC-1.1-06, TC-1.2-01
- Bug relates to US-1.1, US-1.2

#### BUG-05 — Search accepts more infants than adults

Bug ID Placeholder: BUG-05

Bug Title: Search accepts more infants than adults

Severity: High

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult.

Exact Reproduction Steps:
1. Use Round trip with valid dates 2026-09-28 and 2026-10-05.
2. Leave Adults at 1 and increase Infants twice to 2.
3. Click Search flights.

Expected Result:
Prevent or reject Infants exceeding Adults.

Actual Result:
The selector showed 1 Adult and 2 Infants; search advanced without validation.

Affected Story/Stories: US-1.2

Affected Test Case(s): TC-1.2-02

Evidence:
The selector showed 1 Adult and 2 Infants; search advanced without validation.

Recommended Jira Links:
- Bug relates to TC-1.2-02
- Bug relates to US-1.2

#### BUG-06 — Price sorting places expensive flights before cheaper flights

Bug ID Placeholder: BUG-06

Bug Title: Price sorting places expensive flights before cheaper flights

Severity: Medium

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult. Six one-way Economy results are displayed.

Exact Reproduction Steps:
1. Search VLM→HDX, one-way 2026-09-28, Economy, 1 Adult.
2. Select Price: low to high.
3. Read all prices from top to bottom.

Expected Result:
Order the six prices numerically as $105, $491, $595, $636, $1,022, $1,350.

Actual Result:
Displayed order was $1,022, $1,350, $105, $491, $595, $636. This description does not infer the sorting implementation.

Affected Story/Stories: US-2.1

Affected Test Case(s): TC-2.1-01

Evidence:
Displayed order was $1,022, $1,350, $105, $491, $595, $636. This description does not infer the sorting implementation.

Recommended Jira Links:
- Bug relates to TC-2.1-01
- Bug relates to US-2.1

#### BUG-07 — Nonstop only filter retains one-stop flights

Bug ID Placeholder: BUG-07

Bug Title: Nonstop only filter retains one-stop flights

Severity: Medium

Preconditions:
SkyBook Flight Search is displayed. Unless overridden: VLM→HDX, 2026-09-28, Economy, 1 Adult. Full one-way Economy results are displayed.

Exact Reproduction Steps:
1. Select Departure: earliest.
2. Enable Nonstop only.
3. Inspect each remaining flight’s stops.

Expected Result:
Only zero-stop flights should remain.

Actual Result:
AL 457 and NS 261 remained labeled 1 stop alongside three Nonstop flights.

Affected Story/Stories: US-2.2

Affected Test Case(s): TC-2.2-01

Evidence:
AL 457 and NS 261 remained labeled 1 stop alongside three Nonstop flights.

Recommended Jira Links:
- Bug relates to TC-2.2-01
- Bug relates to US-2.2

#### BUG-08 — Passenger details accepts email without a domain

Bug ID Placeholder: BUG-08

Bug Title: Passenger details accepts email without a domain

Severity: Medium

Preconditions:
Passenger details is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101. Otherwise valid data: Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Exact Reproduction Steps:
1. Replace the valid email with rahaf@, retaining valid phone 0791234567 and all other valid fields.
2. Click Continue to seats.

Expected Result:
Reject email without a valid domain/TLD with clear validation.

Actual Result:
Seat selection opened without email validation.

Affected Story/Stories: US-3.1

Affected Test Case(s): TC-3.1-02

Evidence:
Seat selection opened without email validation.

Recommended Jira Links:
- Bug relates to TC-3.1-02
- Bug relates to US-3.1

#### BUG-09 — Passenger details accepts a six-digit phone number

Bug ID Placeholder: BUG-09

Bug Title: Passenger details accepts a six-digit phone number

Severity: Medium

Preconditions:
Passenger details is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101. Otherwise valid data: Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Exact Reproduction Steps:
1. Keep email rahaf.test@example.com and other identity fields valid.
2. Replace phone with 123456.
3. Click Continue to seats.

Expected Result:
Reject phone numbers shorter than 7 digits with validation.

Actual Result:
Seat selection opened with no phone validation.

Affected Story/Stories: US-3.1

Affected Test Case(s): TC-3.1-02

Evidence:
Seat selection opened with no phone validation.

Recommended Jira Links:
- Bug relates to TC-3.1-02
- Bug relates to US-3.1

#### BUG-10 — Passenger details accepts a future date of birth

Bug ID Placeholder: BUG-10

Bug Title: Passenger details accepts a future date of birth

Severity: High

Preconditions:
Passenger details is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101. Otherwise valid data: Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Exact Reproduction Steps:
1. Enter DOB 2027-01-15 for the Adult passenger; leave other fields valid.
2. Click Continue to seats.

Expected Result:
Reject a future DOB with clear validation.

Actual Result:
Seat selection opened without DOB validation.

Affected Story/Stories: US-3.2

Affected Test Case(s): TC-3.2-02

Evidence:
Seat selection opened without DOB validation.

Recommended Jira Links:
- Bug relates to TC-3.2-02
- Bug relates to US-3.2

#### BUG-11 — Adult passenger accepts a child-age date of birth

Bug ID Placeholder: BUG-11

Bug Title: Adult passenger accepts a child-age date of birth

Severity: High

Preconditions:
Passenger details is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101. Otherwise valid data: Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Exact Reproduction Steps:
1. Identify Passenger 1 as ADULT.
2. Enter DOB 2020-01-15 while retaining other valid fields.
3. Click Continue to seats.

Expected Result:
Reject DOB inconsistent with the selected Adult type (16+ years).

Actual Result:
A DOB corresponding to age 6 was accepted for the Adult and Seat selection opened.

Affected Story/Stories: US-3.2

Affected Test Case(s): TC-3.2-02

Evidence:
A DOB corresponding to age 6 was accepted for the Adult and Seat selection opened.

Recommended Jira Links:
- Bug relates to TC-3.2-02
- Bug relates to US-3.2

#### BUG-12 — Passport expiry before departure is accepted

Bug ID Placeholder: BUG-12

Bug Title: Passport expiry before departure is accepted

Severity: High

Preconditions:
Passenger details is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101. Otherwise valid data: Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Exact Reproduction Steps:
1. Set passport expiry to 2026-09-20 for outbound travel 2026-09-28.
2. Click Continue to seats.

Expected Result:
Prevent continuation and display passport-expiry validation.

Actual Result:
Seat selection opened without expiry validation.

Affected Story/Stories: US-3.3

Affected Test Case(s): TC-3.3-02

Evidence:
Seat selection opened without expiry validation.

Recommended Jira Links:
- Bug relates to TC-3.3-02
- Bug relates to US-3.3

#### BUG-13 — Two passengers can hold the same seat

Bug ID Placeholder: BUG-13

Bug Title: Two passengers can hold the same seat

Severity: High

Preconditions:
Seat selection is displayed for CJ 101, VLM→HDX 2026-09-28, Economy, with Test User (Adult) and Test Child (Child); an Infant is on lap.

Exact Reproduction Steps:
1. Select available seat 1A for Test User.
2. Select the Test Child tab.
3. Click map seat 1A already assigned to Test User.

Expected Result:
A seat must not be assigned to more than one passenger.

Actual Result:
Both tabs displayed 1A and the UI reported 2/2 seated.

Affected Story/Stories: US-4.1

Affected Test Case(s): TC-4.1-01

Evidence:
Both tabs displayed 1A and the UI reported 2/2 seated.

Recommended Jira Links:
- Bug relates to TC-4.1-01
- Bug relates to US-4.1

#### BUG-14 — Continue to extras enables before all required passengers are seated

Bug ID Placeholder: BUG-14

Bug Title: Continue to extras enables before all required passengers are seated

Severity: High

Preconditions:
Fresh Seat selection for 1 Adult, 1 Child, 1 Infant, CJ 101, VLM→HDX 2026-09-28, Economy; zero seats assigned.

Exact Reproduction Steps:
1. Observe Continue disabled at 0/2 seated.
2. Assign seat 1A to the Adult only.
3. Inspect Continue before seating the Child.

Expected Result:
Continue must remain disabled until both Adult and Child have seats.

Actual Result:
Continue became enabled at 1/2 seated; the Child still had no seat.

Affected Story/Stories: US-4.2

Affected Test Case(s): TC-4.2-01

Evidence:
Continue became enabled at 1/2 seated; the Child still had no seat.

Recommended Jira Links:
- Bug relates to TC-4.2-01
- Bug relates to US-4.2

#### BUG-15 — Negative baggage quantity reduces the booking price

Bug ID Placeholder: BUG-15

Bug Title: Negative baggage quantity reduces the booking price

Severity: High

Preconditions:
Extras is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult+1 Child+1 Infant; Adult/Child seats 1A/1C. All meals None, baggage 0, insurance off, no promo. Total $2,958; Fares $2,913, taxes $45.

Exact Reproduction Steps:
1. Click baggage minus at quantity 0.
2. Inspect quantity and price.

Expected Result:
Baggage must not fall below 0 or create a negative charge.

Actual Result:
Quantity became −1, Extra baggage became −$35 and total fell from $2,958 to $2,923.

Affected Story/Stories: US-5.1

Affected Test Case(s): TC-5.1-01

Evidence:
Quantity became −1, Extra baggage became −$35 and total fell from $2,958 to $2,923.

Recommended Jira Links:
- Bug relates to TC-5.1-01
- Bug relates to US-5.1

#### BUG-16 — Baggage control permits twenty bags without a sane upper bound

Bug ID Placeholder: BUG-16

Bug Title: Baggage control permits twenty bags without a sane upper bound

Severity: Medium

Preconditions:
Extras is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult+1 Child+1 Infant; Adult/Child seats 1A/1C. All meals None, baggage 0, insurance off, no promo. Total $2,958; Fares $2,913, taxes $45.

Exact Reproduction Steps:
1. Increase baggage repeatedly.
2. Reach 20 and inspect the quantity and total.

Expected Result:
Enforce a sane maximum per passenger.

Actual Result:
Twenty bags were selectable for two seat-holding passengers (plus one lap Infant); baggage $700 and total $3,658. No maximum was reached; values above 20 were not tested.

Affected Story/Stories: US-5.1

Affected Test Case(s): TC-5.1-01

Evidence:
Twenty bags were selectable for two seat-holding passengers (plus one lap Infant); baggage $700 and total $3,658. No maximum was reached; values above 20 were not tested.

Recommended Jira Links:
- Bug relates to TC-5.1-01
- Bug relates to US-5.1

#### BUG-17 — Repeated SAVE10 application accumulates discounts

Bug ID Placeholder: BUG-17

Bug Title: Repeated SAVE10 application accumulates discounts

Severity: High

Preconditions:
Extras is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult+1 Child+1 Infant; Adult/Child seats 1A/1C. All meals None, baggage 0, insurance off, no promo. Total $2,958; Fares $2,913, taxes $45.

Exact Reproduction Steps:
1. Enter SAVE10 and click Apply.
2. Record discount and total.
3. Click Apply twice more, recording each change.

Expected Result:
Apply the valid promo exactly once, regardless of repeated clicks.

Actual Result:
Discount progressed $291→$583→$874; total $2,667→$2,375→$2,084.

Affected Story/Stories: US-5.4

Affected Test Case(s): TC-5.4-01

Evidence:
Discount progressed $291→$583→$874; total $2,667→$2,375→$2,084.

Recommended Jira Links:
- Bug relates to TC-5.4-01
- Bug relates to US-5.4

#### BUG-18 — Invalid TEST promo is reported as successfully applied

Bug ID Placeholder: BUG-18

Bug Title: Invalid TEST promo is reported as successfully applied

Severity: Medium

Preconditions:
Extras is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult+1 Child+1 Infant; Adult/Child seats 1A/1C. All meals None, baggage 0, insurance off, no promo. Total $2,958; Fares $2,913, taxes $45.

Exact Reproduction Steps:
1. Enter TEST.
2. Click Apply.
3. Inspect message, promo indicator and total.

Expected Result:
Reject invalid TEST with a clear error and no applied promo.

Actual Result:
UI displayed TEST applied and Promo code applied!, plus Promo TEST −$0.00. Total remained $2,958.

Affected Story/Stories: US-5.4

Affected Test Case(s): TC-5.4-02

Evidence:
UI displayed TEST applied and Promo code applied!, plus Promo TEST −$0.00. Total remained $2,958.

Recommended Jira Links:
- Bug relates to TC-5.4-02
- Bug relates to US-5.4

#### BUG-19 — Removing SAVE10 leaves the discounted total displayed

Bug ID Placeholder: BUG-19

Bug Title: Removing SAVE10 leaves the discounted total displayed

Severity: High

Preconditions:
Extras is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult+1 Child+1 Infant; Adult/Child seats 1A/1C. All meals None, baggage 0, insurance off, no promo. Total $2,958; Fares $2,913, taxes $45.

Exact Reproduction Steps:
1. Apply SAVE10 once; observe total $2,667.
2. Click ✕ beside SAVE10.
3. Inspect the remaining breakdown and total without changing other controls.

Expected Result:
Remove the discount and restore total $2,958.

Actual Result:
The promo line disappeared but Total stayed $2,667 while the remaining lines summed to $2,958.

Affected Story/Stories: US-5.4

Affected Test Case(s): TC-5.4-03

Evidence:
The promo line disappeared but Total stayed $2,667 while the remaining lines summed to $2,958.

Recommended Jira Links:
- Bug relates to TC-5.4-03
- Bug relates to US-5.4

#### BUG-20 — Payment completes with cardholder name and ZIP blank

Bug ID Placeholder: BUG-20

Bug Title: Payment completes with cardholder name and ZIP blank

Severity: High

Preconditions:
Practice Payment is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult, seat 1A, no extras, total $1,067. Valid baseline: Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C checked unless specified.

Exact Reproduction Steps:
1. Leave Name on card and Billing ZIP / postal code blank.
2. Enter valid card number, expiry 08/29 and CVV 123; accept T&C.
3. Click Pay now.

Expected Result:
Require cardholder name and ZIP and show validation when blank.

Actual Result:
Booking confirmed BK-70-65 at $1,067 with both fields blank.

Affected Story/Stories: US-6.1

Affected Test Case(s): TC-6.1-02

Evidence:
Booking confirmed BK-70-65 at $1,067 with both fields blank.

Recommended Jira Links:
- Bug relates to TC-6.1-02
- Bug relates to US-6.1

#### BUG-21 — Payment accepts an expired card

Bug ID Placeholder: BUG-21

Bug Title: Payment accepts an expired card

Severity: High

Preconditions:
Practice Payment is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult, seat 1A, no extras, total $1,067. Valid baseline: Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C checked unless specified.

Exact Reproduction Steps:
1. Replace expiry with 01/20 while retaining otherwise valid payment fields.
2. Accept T&C and click Pay now.

Expected Result:
Reject an expiry in the past with clear validation.

Actual Result:
Booking confirmed BK-70-28 at $1,067.

Affected Story/Stories: US-6.1

Affected Test Case(s): TC-6.1-02

Evidence:
Booking confirmed BK-70-28 at $1,067.

Recommended Jira Links:
- Bug relates to TC-6.1-02
- Bug relates to US-6.1

#### BUG-22 — Payment accepts short, long and nonnumeric CVV values

Bug ID Placeholder: BUG-22

Bug Title: Payment accepts short, long and nonnumeric CVV values

Severity: High

Preconditions:
Practice Payment is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult, seat 1A, no extras, total $1,067. Valid baseline: Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C checked unless specified.

Exact Reproduction Steps:
1. In separate valid bookings, enter CVV 12, 12345, and abc respectively.
2. Keep card, name, expiry 08/29 and ZIP valid; accept T&C.
3. Click Pay now for each dataset.

Expected Result:
CVV must be exactly 3–4 numeric digits; reject each invalid dataset.

Actual Result:
All three completed: 12→BK-70-67; 12345→BK-70-22; abc→BK-70-49; each $1,067.

Affected Story/Stories: US-6.1

Affected Test Case(s): TC-6.1-02

Evidence:
All three completed: 12→BK-70-67; 12345→BK-70-22; abc→BK-70-49; each $1,067.

Recommended Jira Links:
- Bug relates to TC-6.1-02
- Bug relates to US-6.1

#### BUG-23 — Payment completes without fare-rules acceptance

Bug ID Placeholder: BUG-23

Bug Title: Payment completes without fare-rules acceptance

Severity: High

Preconditions:
Practice Payment is displayed for VLM→HDX, one-way 2026-09-28, Economy, CJ 101, 1 Adult, seat 1A, no extras, total $1,067. Valid baseline: Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C checked unless specified.

Exact Reproduction Steps:
1. Enter all valid payment values.
2. Leave I agree to the Fare Rules and Terms & Conditions unchecked.
3. Click Pay now.

Expected Result:
Block payment until acceptance.

Actual Result:
Booking confirmed BK-70-08 at $1,067 while checkbox had remained unchecked.

Affected Story/Stories: US-6.2

Affected Test Case(s): TC-6.2-01

Evidence:
Booking confirmed BK-70-08 at $1,067 while checkbox had remained unchecked.

Recommended Jira Links:
- Bug relates to TC-6.2-01
- Bug relates to US-6.2

#### BUG-24 — Start a new booking retains prior trip, cabin and passenger counts

Bug ID Placeholder: BUG-24

Bug Title: Start a new booking retains prior trip, cabin and passenger counts

Severity: Medium

Preconditions:
Completed booking BK-70-82: VLM→HDX, 2026-09-28, One-way, Business, 1 Adult+1 Child, seats 3A/3B, baggage 1, Vegan/Vegetarian meals, insurance on, valid payment.

Exact Reproduction Steps:
1. Click Start a new booking.
2. Inspect search fields before selecting anything.
3. Observe trip type, cabin and passenger counts.

Expected Result:
Clear previous booking selections so the user starts a fresh booking.

Actual Result:
One-way, Business, 1 Adult and 1 Child remained selected; VLM→HDX and 2026-09-28 also remained. Identity, seats, extras and payment were cleared.

Affected Story/Stories: US-7.3

Affected Test Case(s): TC-7.3-01

Evidence:
One-way, Business, 1 Adult and 1 Child remained selected; VLM→HDX and 2026-09-28 also remained. Identity, seats, extras and payment were cleared.

Recommended Jira Links:
- Bug relates to TC-7.3-01
- Bug relates to US-7.3
