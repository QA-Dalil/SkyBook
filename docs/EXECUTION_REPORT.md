# SkyBook — Complete Manual QA Execution Report

Execution date: 2026-09-07 (Asia/Riyadh)

Live URL: [SkyBook Practice Booking](https://claude.ai/code/artifact/5028f8a7-4747-4b7e-b07f-a4dddf65807c)

Scope: the 37 test cases in the supplied attachment supersede the earlier 43-case placeholder. IDs, titles, stories, preconditions and expected results are preserved below. Actions used the live rendered UI, accessibility representation of that UI, and screenshots. No source code, hidden application data, answer keys, Ground crew access, Jira, or Xray were inspected or modified.

The page explicitly identifies itself as a fictional QA practice environment and states that no real card is charged or seat booked. All identity values entered were synthetic QA data. Currency is reported exactly using the displayed $ symbol; no currency code is assumed. Dates below use YYYY-MM-DD to avoid ambiguity.

Independence: fresh reloads and explicit UI resets were used when needed. Otherwise the prior test’s modified fields, passengers, filters, seats, extras or promo were restored before the next relevant check. A temporary tab loss before TC-6.1-02 required rebuilding its setup; it did not interrupt the two bookings of TC-7.1-01. The unique-code case used one uninterrupted session without reload between A and B. No unobserved test is counted as passed.

## 1. EXECUTION SUMMARY

- Total Test Cases: 37
- PASS: 16
- FAIL: 20
- BLOCKED: 1
- Check: 16 + 20 + 1 = 37
- Unique proposed bugs: 24

TC-6.3-01 is BLOCKED because the displayed aggregate fare and tax lines do not expose the individual Child fare or a tax-scaling basis. Its visible arithmetic check passed. No child overcharge or hidden tax calculation is asserted.

## 2. TEST EXECUTION TABLE

| TC ID | Story | Title | Result | Bug ID if Failed |
| --- | --- | --- | --- | --- |
| TC-1.1-01 | US-1.1 | Search with different valid origin and destination cities | PASS | — |
| TC-1.1-02 | US-1.1 | Reject search when origin and destination are the same | FAIL | BUG-01 |
| TC-1.1-03 | US-1.1 | Search a valid round-trip | PASS | — |
| TC-1.1-04 | US-1.1 | Reject return date before departure date | FAIL | BUG-02 |
| TC-1.1-05 | US-1.1 | Reject travel dates earlier than today | FAIL | BUG-03 |
| TC-1.1-06 | US-1.1 | Reject search with zero adults | FAIL | BUG-04 |
| TC-1.2-01 | US-1.2 | Enforce passenger count boundaries | FAIL | BUG-04 |
| TC-1.2-02 | US-1.2 | Prevent infants from exceeding adults | FAIL | BUG-05 |
| TC-1.2-03 | US-1.2 | Carry selected cabin through pricing | PASS | — |
| TC-2.1-01 | US-2.1 | Sort flights by price low to high | FAIL | BUG-06 |
| TC-2.1-02 | US-2.1 | Sort flights by shortest duration | PASS | — |
| TC-2.1-03 | US-2.1 | Sort flights by earliest departure | PASS | — |
| TC-2.2-01 | US-2.2 | Display only nonstop flights | FAIL | BUG-07 |
| TC-2.2-02 | US-2.2 | Restore results after disabling Nonstop filter | PASS | — |
| TC-2.3-01 | US-2.3 | Display complete flight details and low availability | PASS | — |
| TC-3.1-01 | US-3.1 | Accept valid lead contact details | PASS | — |
| TC-3.1-02 | US-3.1 | Reject invalid email and phone | FAIL | BUG-08, BUG-09 |
| TC-3.2-01 | US-3.2 | Accept valid DOB matching passenger type | PASS | — |
| TC-3.2-02 | US-3.2 | Reject invalid DOB | FAIL | BUG-10, BUG-11 |
| TC-3.3-01 | US-3.3 | Accept passport valid beyond travel | PASS | — |
| TC-3.3-02 | US-3.3 | Reject passport expiring before travel completion | FAIL | BUG-12 |
| TC-4.1-01 | US-4.1 | Prevent occupied and duplicate seat assignment | FAIL | BUG-13 |
| TC-4.1-02 | US-4.1 | Release previous seat when changing selection | PASS | — |
| TC-4.2-01 | US-4.2 | Require seats for all seat-holding passengers | FAIL | BUG-14 |
| TC-5.1-01 | US-5.1 | Enforce baggage quantity boundaries | FAIL | BUG-15, BUG-16 |
| TC-5.2-01 | US-5.2 | Select meals independently per passenger | PASS | — |
| TC-5.3-01 | US-5.3 | Add travel insurance to booking price | PASS | — |
| TC-5.4-01 | US-5.4 | Apply valid promo code exactly once | FAIL | BUG-17 |
| TC-5.4-02 | US-5.4 | Reject invalid promo code | FAIL | BUG-18 |
| TC-5.4-03 | US-5.4 | Remove promo and recalculate total | FAIL | BUG-19 |
| TC-6.1-01 | US-6.1 | Accept valid payment details | PASS | — |
| TC-6.1-02 | US-6.1 | Validate required payment fields, expiry and CVV | FAIL | BUG-20, BUG-21, BUG-22 |
| TC-6.2-01 | US-6.2 | Block payment until T&C are accepted | FAIL | BUG-23 |
| TC-6.3-01 | US-6.3 | Verify complete booking price calculation | BLOCKED | — |
| TC-7.1-01 | US-7.1 | Generate unique confirmation codes | PASS | — |
| TC-7.2-01 | US-7.2 | Verify confirmation summary matches booking | PASS | — |
| TC-7.3-01 | US-7.3 | Clear previous data when starting a new booking | FAIL | BUG-24 |

## 3. DETAILED EXECUTION RECORDS

### TC-1.1-01 — Search with different valid origin and destination cities

TC ID: TC-1.1-01

Story: US-1.1

Title: Search with different valid origin and destination cities

Preconditions:
1. SkyBook is accessible.
2. The user is on the Flight Search page.
3. The flight search form is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants.

Execution Steps Actually Performed:
1. Opened the supplied live URL and inspected the Flight Search form.
2. Kept the displayed VLM origin and HDX destination; selected One way.
3. Used the displayed future departure 2026-09-28, 1 Adult and Economy.
4. Clicked Search flights and inspected the outbound results.

Expected Result:
The search is submitted successfully and available one-way flights from VLM to HDX matching the selected criteria are displayed.

Actual Result:
Search advanced to “Choose your outbound flight” for Vellamar (VLM) to Halden Cross (HDX), Mon, Sep 28. Six flight results were displayed; the itinerary showed One-way, 1 passenger(s), Economy.

Test Status:
PASS

Evidence:
- CJ 101: 09:45–12:57, 3h 12m, Nonstop, $1,022.00.
- Other displayed flights: NS 675, AL 457, CJ 862, AL 168, NS 261.

### TC-1.1-02 — Reject search when origin and destination are the same

TC ID: TC-1.1-02

Story: US-1.1

Title: Reject search when origin and destination are the same

Preconditions:
1. SkyBook is accessible.
2. The user is on the Flight Search page.
3. The flight search form is displayed.

Exact Test Data Used:
Vellamar (VLM) → Vellamar (VLM); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants.

Execution Steps Actually Performed:
1. Reloaded to a clean search form.
2. Kept Vellamar as origin and selected Vellamar as destination.
3. Selected One way; used 2026-09-28, 1 Adult and Economy.
4. Clicked Search flights.

Expected Result:
The search is blocked and the user is clearly informed that the origin and destination cannot be the same.

Actual Result:
The application accepted Vellamar as both origin and destination and displayed six VLM-to-VLM flights. No same-city validation was displayed.

Test Status:
FAIL

Evidence:
- Heading: “Vellamar (VLM) to Vellamar (VLM) · Mon, Sep 28”.
- Example result: VeloJet · VJ 485 · 737 MAX 8, 15:20–23:24, $1,158.00.

Proposed bug reference(s): BUG-01.

### TC-1.1-03 — Search a valid round-trip

TC ID: TC-1.1-03

Story: US-1.1

Title: Search a valid round-trip

Preconditions:
1. SkyBook is accessible.
2. The user is on the Flight Search page.
3. The flight search form is displayed.

Exact Test Data Used:
VLM → HDX; Round trip; departure 2026-09-27; return 2026-10-04; 1 Adult; Economy.

Execution Steps Actually Performed:
1. Returned to search and restored HDX destination and Round trip.
2. Entered departure 2026-09-27 and return 2026-10-04; kept 1 Adult and Economy.
3. Clicked Search flights and inspected outbound results.
4. Selected outbound AeroLuna AL 856 to reveal and inspect the return results.

Expected Result:
The search is submitted successfully, and available outbound and return flights between VLM and HDX matching the selected travel dates and criteria are displayed.

Actual Result:
Outbound flights were displayed for VLM→HDX on Sun, Sep 27. After selecting AL 856, return flights were displayed for HDX→VLM on Sun, Oct 4.

Test Status:
PASS

Evidence:
- Outbound AL 856: 20:30–22:27, 1h 57m, Nonstop, $312.00.
- Return NL 632: 09:20–12:10, 2h 50m, Nonstop, $1,026.00.

### TC-1.1-04 — Reject return date before departure date

TC ID: TC-1.1-04

Story: US-1.1

Title: Reject return date before departure date

Preconditions:
1. SkyBook is accessible.
2. The user is on the Flight Search page.
3. Round-trip is selected.

Exact Test Data Used:
VLM → HDX; Round trip; departure 2026-09-30; return 2026-09-20; 1 Adult; Economy.

Execution Steps Actually Performed:
1. Returned to the search form.
2. Entered departure 2026-09-30 and return 2026-09-20.
3. Clicked Search flights and inspected the resulting itinerary.

Expected Result:
The search is blocked because the return date is earlier than the departure date, and clear validation is displayed.

Actual Result:
Search proceeded to outbound results even though the return date preceded departure. The itinerary displayed “Wed, Sep 30 · Return Sun, Sep 20”; no date-order validation appeared.

Test Status:
FAIL

Evidence:
- Outbound heading: Vellamar (VLM) to Halden Cross (HDX) · Wed, Sep 30.
- CJ 742 was displayed at $1,321.00.

Proposed bug reference(s): BUG-02.

### TC-1.1-05 — Reject travel dates earlier than today

TC ID: TC-1.1-05

Story: US-1.1

Title: Reject travel dates earlier than today

Preconditions:
1. SkyBook is accessible.
2. The flight search form is displayed.

Exact Test Data Used:
Execution date: 2026-09-07 (Asia/Riyadh). VLM→HDX, Round trip, 1 Adult, Economy. A: depart 2026-09-01, return 2026-10-05. B: depart 2026-09-28, return 2026-09-01.

Execution Steps Actually Performed:
1. Returned to search; entered dataset A and clicked Search flights.
2. Recorded the results and returned to search.
3. Replaced both dates with dataset B and clicked Search flights.
4. Recorded the resulting itinerary and absence of validation.

Expected Result:
Departure and return dates earlier than today cannot be used for a flight search. Invalid searches are blocked with clear validation.

Actual Result:
Both past-date searches proceeded to flight results. Dataset A displayed outbound flights for Tue, Sep 1; dataset B displayed an itinerary with Mon, Sep 28 departure and Tue, Sep 1 return. Neither search displayed past-date validation.

Test Status:
FAIL

Evidence:
- A: NS 421, $375.00; itinerary “Tue, Sep 1 · Return Mon, Oct 5”.
- B: CJ 101, $1,022.00; itinerary “Mon, Sep 28 · Return Tue, Sep 1”.

Dataset Results:
- A — FAIL: past departure accepted.
- B — FAIL: past return accepted.

Proposed bug reference(s): BUG-03.

### TC-1.1-06 — Reject search with zero adults

TC ID: TC-1.1-06

Story: US-1.1

Title: Reject search with zero adults

Preconditions:
1. SkyBook is accessible.
2. The flight search form is displayed.

Exact Test Data Used:
VLM→HDX; Round trip; depart 2026-09-28; return 2026-10-05; Economy; Adults changed 1→0; Children 0; Infants 0.

Execution Steps Actually Performed:
1. Returned to search and restored a valid return date.
2. Clicked the Adult minus control once.
3. Observed 0 Adults and 0 passenger(s) selected.
4. Clicked Search flights.

Expected Result:
The search is blocked unless at least one adult passenger is selected.

Actual Result:
The Adult count decreased to 0 and Search flights still opened outbound results. The results itinerary showed “0 passenger(s) · Economy”; no adult-minimum validation appeared.

Test Status:
FAIL

Evidence:
- Adult count: 0.
- Search results: CJ 101 $1,022.00 and five other flights.

Proposed bug reference(s): BUG-04.

### TC-1.2-01 — Enforce passenger count boundaries

TC ID: TC-1.2-01

Story: US-1.2

Title: Enforce passenger count boundaries

Preconditions:
1. SkyBook is accessible.
2. Passenger selector is available.

Exact Test Data Used:
Round trip VLM→HDX, 2026-09-28 / 2026-10-05, Economy. Adults tested 1→0→9, then attempted 10; Children 0→9, attempted 10; Infants 0→9, attempted 10.

Execution Steps Actually Performed:
1. Restored Adults to 1 on the search form; passenger controls were already displayed.
2. Clicked Adult minus and observed 0.
3. Clicked Adult plus nine times to reach 9, then once more.
4. Verified Children at 0; clicked Child plus nine times and once more.
5. Verified Infants at 0; clicked Infant plus nine times and once more.
6. Reloaded afterwards to clear the boundary-test counts.

Expected Result:
Adults remain within 1–9.
Children remain within 0–9.
Infants remain within 0–9.
Values outside the permitted ranges cannot be selected.

Actual Result:
Adults could be reduced below the required minimum to 0. Adults, Children and Infants each reached 9 and remained at 9 after another plus click. Children and Infants both supported 0.

Test Status:
FAIL

Evidence:
- Final boundary-test counts: 9 Adults, 9 Children, 9 Infants; 27 passenger(s) selected.
- Adult minimum failure is the same defect as TC-1.1-06.

Dataset Results:
- Adult minimum — FAIL: 1→0 allowed.
- Adult maximum — PASS: 9→9 after plus.
- Child zero/maximum — PASS: 0 available; 9→9 after plus.
- Infant zero/maximum — PASS: 0 available; 9→9 after plus.

Proposed bug reference(s): BUG-04.

### TC-1.2-02 — Prevent infants from exceeding adults

TC ID: TC-1.2-02

Story: US-1.2

Title: Prevent infants from exceeding adults

Preconditions:
1. Passenger selector is displayed.

Exact Test Data Used:
VLM→HDX; Round trip; 2026-09-28 / 2026-10-05; Economy; 1 Adult, 0 Children, 2 Infants.

Execution Steps Actually Performed:
1. Started from the reloaded 1 Adult / 0 Child / 0 Infant form.
2. Clicked Infant plus twice.
3. Observed 2 Infants with 1 Adult, then clicked Search flights.

Expected Result:
The system prevents or clearly rejects an infant count greater than the adult count.

Actual Result:
The UI allowed 2 Infants with only 1 Adult and proceeded to outbound results without validation.

Test Status:
FAIL

Evidence:
- Passenger selector showed Adults 1, Infants 2, “3 passenger(s) selected”.
- Results itinerary: “3 passenger(s) · Economy”.

Proposed bug reference(s): BUG-05.

### TC-1.2-03 — Carry selected cabin through pricing

TC ID: TC-1.2-03

Story: US-1.2

Title: Carry selected cabin through pricing

Preconditions:
1. A valid flight search can be performed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Three cabin datasets: Economy, Premium Economy, Business.

Execution Steps Actually Performed:
1. Returned to search, removed both infants, and selected One way.
2. Searched Economy and recorded the cabin and all displayed prices.
3. Returned to search, selected Premium Economy, searched and recorded prices.
4. Returned to search, selected Business, searched and recorded prices.

Expected Result:
Economy, Premium Economy and Business can be selected and the selected cabin carries through correctly to flight pricing.

Actual Result:
All three cabins could be selected and each results itinerary retained the selected cabin. Displayed flight pricing changed for each cabin dataset.

Test Status:
PASS

Evidence:
- Economy prices, top-to-bottom: $1,022, $1,350, $105, $491, $595, $636.
- Premium Economy: $1,091, $1,197, $1,511, $1,879, $2,072, $2,127.
- Business: $1,557, $2,192, $281, $3,088, $3,583, $437.
- Cabin searches returned different flight sets; no unsupported same-flight multiplier calculation was inferred.

Dataset Results:
- Economy — PASS.
- Premium Economy — PASS.
- Business — PASS.

### TC-2.1-01 — Sort flights by price low to high

TC ID: TC-2.1-01

Story: US-2.1

Title: Sort flights by price low to high

Preconditions:
1. Flight results containing multiple prices are displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Sort: Price: low to high.

Execution Steps Actually Performed:
1. Returned to search and restored Economy; submitted the search.
2. Explicitly selected Price: low to high.
3. Recorded all six prices top-to-bottom and compared numerically.

Expected Result:
Flights are ordered numerically from lowest to highest price.

Actual Result:
Price sorting displayed $1,022, $1,350, $105, $491, $595 and $636 in that order. This is not numeric ascending order because $105 follows $1,350.

Test Status:
FAIL

Evidence:
- Displayed order: CJ 101, NS 675, AL 457, CJ 862, AL 168, NS 261.
- Correct numeric order for those prices would be $105, $491, $595, $636, $1,022, $1,350.

Proposed bug reference(s): BUG-06.

### TC-2.1-02 — Sort flights by shortest duration

TC ID: TC-2.1-02

Story: US-2.1

Title: Sort flights by shortest duration

Preconditions:
1. Multiple flight results with different durations are displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Sort: Duration: shortest.

Execution Steps Actually Performed:
1. Selected Duration: shortest on the full results list.
2. Recorded and compared every displayed duration.

Expected Result:
Flights are ordered from shortest to longest duration.

Actual Result:
The six durations were displayed in ascending order: 3h 12m, 3h 16m, 3h 40m, 4h 18m, 5h 11m and 8h 16m.

Test Status:
PASS

Evidence:
- Flight order: CJ 101, NS 675, AL 168, CJ 862, NS 261, AL 457.

### TC-2.1-03 — Sort flights by earliest departure

TC ID: TC-2.1-03

Story: US-2.1

Title: Sort flights by earliest departure

Preconditions:
1. Multiple flight results with different departure times are displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Sort: Departure: earliest.

Execution Steps Actually Performed:
1. Selected Departure: earliest.
2. Recorded and compared all six departure times.

Expected Result:
Flights are ordered from earliest to latest departure.

Actual Result:
Departure times were ordered chronologically: 05:40, 09:45, 17:25, 20:45, 21:45 and 22:10.

Test Status:
PASS

Evidence:
- Flight order: NS 675, CJ 101, AL 168, CJ 862, AL 457, NS 261.

### TC-2.2-01 — Display only nonstop flights

TC ID: TC-2.2-01

Story: US-2.2

Title: Display only nonstop flights

Preconditions:
1. Results contain nonstop and connecting flights.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Sort: Departure: earliest; Nonstop only enabled.

Execution Steps Actually Performed:
1. Verified the full list contained nonstop, one-stop and two-stop flights.
2. Enabled Nonstop only.
3. Inspected the stops values of every remaining flight.

Expected Result:
Only flights with zero stops are displayed.

Actual Result:
The filter removed the two-stop flight but retained two one-stop flights alongside three nonstop flights. AL 457 and NS 261 remained visible despite Nonstop only being checked.

Test Status:
FAIL

Evidence:
- Remaining stops: NS 675 Nonstop; CJ 101 Nonstop; AL 168 Nonstop; AL 457 1 stop; NS 261 1 stop.

Proposed bug reference(s): BUG-07.

### TC-2.2-02 — Restore results after disabling Nonstop filter

TC ID: TC-2.2-02

Story: US-2.2

Title: Restore results after disabling Nonstop filter

Preconditions:
1. Flight results are displayed.
2. A sorting option can be selected.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Sort: Duration: shortest; Nonstop toggled off→on→off.

Execution Steps Actually Performed:
1. Disabled the previous filter, selected Duration: shortest and recorded the full list.
2. Enabled Nonstop only and recorded the reduced list.
3. Disabled Nonstop only and compared the restored list and selected sort.

Expected Result:
The full flight list is restored and the current sorting option remains applied.

Actual Result:
Disabling the filter restored all six flights in the original duration order. Duration: shortest remained selected.

Test Status:
PASS

Evidence:
- Before and after: CJ 101, NS 675, AL 168, CJ 862, NS 261, AL 457.
- Durations before and after: 3h 12m, 3h 16m, 3h 40m, 4h 18m, 5h 11m, 8h 16m.

Dataset Results:
- Full result restoration — PASS.
- Sort selection/order preservation — PASS.

### TC-2.3-01 — Display complete flight details and low availability

TC ID: TC-2.3-01

Story: US-2.3

Title: Display complete flight details and low availability

Preconditions:
1. Flight search results are displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. Six Economy results, including AL 168 and AL 457 with 2 seats left.

Execution Steps Actually Performed:
1. Inspected all six result entries for departure, arrival, duration, stops, airline, flight number, aircraft and seats remaining.
2. Scrolled the rendered page and visually inspected the low-availability styling.

Expected Result:
Each result displays departure, arrival, duration, stops, airline, flight number, aircraft and seats remaining.
Flights with 3 or fewer seats remaining are visually identified as low availability.

Actual Result:
Each result displayed all required flight details. AL 168 and AL 457 displayed “Only 2 left”; the inspected AL 168 availability text was highlighted in amber, unlike the ordinary seats-left text.

Test Status:
PASS

Evidence:
- CJ 101: VLM 09:45 → HDX 12:57, 3h 12m, Nonstop, CoastJet Regional, A319, 9 seats left.
- AL 168: VLM 17:25 → HDX 21:05, 3h 40m, Nonstop, AeroLuna, A319, amber “Only 2 left”.
- All-result detail matrix is included in the report.

Dataset Results:
- Departure/arrival — PASS.
- Duration/stops — PASS.
- Airline/flight number/aircraft — PASS.
- Seats remaining — PASS.
- Low-availability visual identification — PASS.

### TC-3.1-01 — Accept valid lead contact details

TC ID: TC-3.1-01

Story: US-3.1

Title: Accept valid lead contact details

Preconditions:
1. Passenger Details page is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Execution Steps Actually Performed:
1. Selected CJ 101 to open Passenger details.
2. Entered rahaf.test@example.com and 0791234567.
3. Completed name, DOB, passport number and expiry with the listed valid data.
4. Clicked Continue to seats.

Expected Result:
The valid email and realistic phone number are accepted and the user can continue.

Actual Result:
The email and phone were accepted, and the application advanced to Seat selection with a Test User passenger tab.

Test Status:
PASS

Evidence:
- Seat page: “Continue to extras (0/1 seated)” disabled.
- Booking total: $1,067.00.

### TC-3.1-02 — Reject invalid email and phone

TC ID: TC-3.1-02

Story: US-3.1

Title: Reject invalid email and phone

Preconditions:
1. Passenger Details page is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. A: email replaced with rahaf@; valid phone retained. B: email restored; phone replaced with 123456.

Execution Steps Actually Performed:
1. Returned from seats to the otherwise valid passenger form.
2. Entered dataset A and clicked Continue to seats; recorded the result.
3. Returned to Passenger details, restored the valid email and entered dataset B.
4. Clicked Continue to seats and recorded the result.

Expected Result:
An email without a valid domain/TLD is rejected.
A phone number shorter than 7 digits is rejected.
Clear validation is displayed for each invalid input.

Actual Result:
Both invalid contact datasets advanced to Seat selection. Email rahaf@ and six-digit phone 123456 were accepted without email or phone validation.

Test Status:
FAIL

Evidence:
- Both attempts displayed the Test User seat tab and “Continue to extras (0/1 seated)”.
- No error message was displayed on either submission.

Dataset Results:
- A invalid email — FAIL.
- B short phone — FAIL.

Proposed bug reference(s): BUG-08, BUG-09.

### TC-3.2-01 — Accept valid DOB matching passenger type

TC ID: TC-3.2-01

Story: US-3.2

Title: Accept valid DOB matching passenger type

Preconditions:
1. Passenger Details page is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Execution Steps Actually Performed:
1. Returned to Passenger details and restored the valid phone.
2. Identified Passenger 1 as ADULT and entered DOB 1990-01-15.
3. Kept the other valid fields and clicked Continue to seats.

Expected Result:
The DOB is accepted because it is not in the future and the calculated age matches the passenger type.

Actual Result:
DOB 1990-01-15 was accepted for the Adult passenger and the application advanced to Seat selection.

Test Status:
PASS

Evidence:
- Passenger heading before submission: “Passenger 1 ADULT LEAD”.
- Age is 36 on the selected travel date; Adult label is 16+ yrs.

### TC-3.2-02 — Reject invalid DOB

TC ID: TC-3.2-02

Story: US-3.2

Title: Reject invalid DOB

Preconditions:
1. Passenger Details page is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. A: DOB 2027-01-15. B: DOB 2020-01-15 for the same Adult passenger.

Execution Steps Actually Performed:
1. Returned to the valid passenger form and entered future DOB 2027-01-15.
2. Clicked Continue to seats and recorded the result.
3. Returned to Passenger details and changed DOB to 2020-01-15.
4. Clicked Continue to seats and recorded the result.

Expected Result:
A future DOB is rejected.
A DOB whose calculated age is inconsistent with the passenger type is rejected.
Clear validation is displayed.

Actual Result:
Both the future DOB and the DOB corresponding to age 6 were accepted for Passenger 1 ADULT LEAD. Each submission advanced to Seat selection without DOB validation.

Test Status:
FAIL

Evidence:
- A: future DOB 2027-01-15 accepted.
- B: DOB 2020-01-15 accepted despite the selected Adult category (16+ yrs).

Dataset Results:
- A future DOB — FAIL.
- B passenger-type mismatch — FAIL.

Proposed bug reference(s): BUG-10, BUG-11.

### TC-3.3-01 — Accept passport valid beyond travel

TC ID: TC-3.3-01

Story: US-3.3

Title: Accept passport valid beyond travel

Preconditions:
1. Passenger/passport details are displayed.
2. Travel dates are known.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity.

Execution Steps Actually Performed:
1. Returned to Passenger details and restored DOB 1990-01-15.
2. Entered passport expiry 2030-12-31, after the 2026-09-28 outbound trip.
3. Clicked Continue to seats.

Expected Result:
The passport expiry is accepted and the user can continue.

Actual Result:
Passport expiry 2030-12-31 was accepted and the application advanced to Seat selection.

Test Status:
PASS

Evidence:
- Outbound CJ 101 arrives 2026-09-28 at 12:57.
- No passport-expiry error was displayed.

### TC-3.3-02 — Reject passport expiring before travel completion

TC ID: TC-3.3-02

Story: US-3.3

Title: Reject passport expiring before travel completion

Preconditions:
1. Passenger/passport details are displayed.
2. Travel dates are known.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Passport expiry replaced with 2026-09-20.

Execution Steps Actually Performed:
1. Returned to the otherwise valid passenger form.
2. Entered passport expiry 2026-09-20, before outbound travel on 2026-09-28.
3. Clicked Continue to seats.

Expected Result:
The user cannot continue and clear passport-expiry validation is displayed.

Actual Result:
The application accepted passport expiry 2026-09-20 and advanced to Seat selection even though travel was on 2026-09-28. No expiry validation appeared.

Test Status:
FAIL

Evidence:
- Passenger passport QA1234567; expiry 2026-09-20.
- Seat selection displayed Test User and 0/1 seated.

Proposed bug reference(s): BUG-12.

### TC-4.1-01 — Prevent occupied and duplicate seat assignment

TC ID: TC-4.1-01

Story: US-4.1

Title: Prevent occupied and duplicate seat assignment

Preconditions:
1. Seat map is displayed.
2. Booking contains at least two seat-holding passengers.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. Occupied seat tested: 6A. Duplicate seat tested: 1A.

Execution Steps Actually Performed:
1. Reloaded and created the listed Adult/Child/Infant booking; filled valid passenger details.
2. Inspected the seat map and legend, identified grey occupied seat 6A and clicked it.
3. Observed no seat assignment, then selected available seat 1A for Test User.
4. Selected Test Child and clicked map seat 1A already assigned to Test User.

Expected Result:
An occupied seat cannot be selected.
The same seat cannot be assigned to more than one passenger.

Actual Result:
Occupied seat 6A could not be assigned: the count remained 0/2. However, seat 1A was assigned to both Test User and Test Child simultaneously, and the count became 2/2.

Test Status:
FAIL

Evidence:
- Tabs: “Test User1A” and “Test Child1A”.
- Continue to extras (2/2 seated) enabled.

Dataset Results:
- Occupied-seat prevention — PASS.
- Duplicate-seat prevention — FAIL.

Proposed bug reference(s): BUG-13.

### TC-4.1-02 — Release previous seat when changing selection

TC ID: TC-4.1-02

Story: US-4.1

Title: Release previous seat when changing selection

Preconditions:
1. Seat map is displayed.
2. A passenger can select an available seat.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. Adult Seat A 1A → Seat B 1E; Child first moved to separate seat 1C.

Execution Steps Actually Performed:
1. Removed the prior duplicate by changing Test Child to 1C.
2. Verified Test User still held 1A.
3. Selected Test User and changed the seat to available 1E.
4. Inspected the settled map and passenger tabs.

Expected Result:
Seat B becomes assigned to the passenger and the previously selected Seat A becomes available again.

Actual Result:
Test User’s seat changed from 1A to 1E. Seat 1E was highlighted as the current passenger’s seat; 1A returned to the available styling. The child retained 1C.

Test Status:
PASS

Evidence:
- Before: Test User1A, Test Child1C.
- After: Test User1E, Test Child1C.
- Visual map: 1E amber; 1A unassigned/available.

### TC-4.2-01 — Require seats for all seat-holding passengers

TC ID: TC-4.2-01

Story: US-4.2

Title: Require seats for all seat-holding passengers

Preconditions:
1. Booking contains 1 Adult, 1 Child and 1 Infant.
2. Seat Selection page is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. Fresh seat selections: Adult 1A, Child 1C.

Execution Steps Actually Performed:
1. Reloaded and recreated the listed booking with no seats assigned.
2. Recorded the initial seated count and Continue state.
3. Assigned only Adult 1A and recorded count/Continue state.
4. Selected Test Child, assigned 1C and recorded count/Continue state.
5. Verified no Infant seat tab or requirement was displayed.

Expected Result:
The Infant is excluded from the required seat count.
Continue remains disabled until both the Adult and Child have seats.
The remaining-unassigned count is accurate at every stage.

Actual Result:
The infant was excluded and counts progressed accurately from 0/2 to 1/2 to 2/2. Continue was disabled at 0/2 but became enabled at 1/2, before the child had a seat.

Test Status:
FAIL

Evidence:
- 0/2 seated: disabled.
- 1/2 seated: enabled.
- 2/2 seated: enabled.
- Only Test User and Test Child tabs were displayed.

Dataset Results:
- Infant excluded — PASS.
- Count accuracy — PASS (unassigned derived from displayed counts: 2, 1, 0).
- Require both seat-holding passengers before enabling Continue — FAIL.

Proposed bug reference(s): BUG-14.

### TC-5.1-01 — Enforce baggage quantity boundaries

TC ID: TC-5.1-01

Story: US-5.1

Title: Enforce baggage quantity boundaries

Preconditions:
1. Extras page is displayed.
2. Extra baggage control is available.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. Extras baseline: 0 bags, meals None, insurance off, no promo. Baggage tested −1 through 20.

Execution Steps Actually Performed:
1. Entered Extras with 0 bags and total $2,958.00.
2. Clicked minus once and recorded −1 bag and price.
3. Clicked plus repeatedly: 10 clicks reached 9, then 11 more reached 20.
4. Stopped at 20 as an unreasonable quantity for two seat-holding passengers; recorded the highest tested value.
5. Decreased baggage 20 times back to 0 before later tests.

Expected Result:
Baggage quantity cannot be less than 0.
A sane upper limit is enforced per passenger.

Actual Result:
The quantity decreased below zero to −1, producing a −$35 baggage line and total $2,923. It also reached 20 bags with a $700 baggage charge and total $3,658 without preventing increases. No upper limit was reached in the tested range.

Test Status:
FAIL

Evidence:
- Baseline 0 / $0 / $2,958.
- −1 / −$35 / $2,923.
- 20 / $700 / $3,658; 20 is the highest observed value, not an asserted maximum.

Dataset Results:
- Lower boundary — FAIL.
- Sane upper limit within tested range — FAIL.

Proposed bug reference(s): BUG-15, BUG-16.

### TC-5.2-01 — Select meals independently per passenger

TC ID: TC-5.2-01

Story: US-5.2

Title: Select meals independently per passenger

Preconditions:
1. Extras page is displayed.
2. Booking contains multiple passengers.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. Baggage reset to 0; no promo or insurance. Meal sequence: all None; Adult Standard; Child Vegetarian; Adult Vegan; Infant Standard.

Execution Steps Actually Performed:
1. Inspected all three meal dropdowns and their four options.
2. Selected Adult Standard; recorded the other passengers still at None and $12 meal charge.
3. Selected Child Vegetarian; recorded $24 total meals.
4. Changed Adult to Vegan; verified Child remained Vegetarian and Infant remained None.
5. Selected Infant Standard; recorded $36 meals, then reset all meals to None.

Expected Result:
Each passenger can independently select None, Standard, Vegetarian or Vegan without affecting another passenger's selection.

Actual Result:
Each passenger had None, Standard, Vegetarian and Vegan options. Changing the Adult meal did not alter the Child or Infant selections. Each selected non-None meal added $12, and three meals totaled $36.

Test Status:
PASS

Evidence:
- All None: meals $0, total $2,958.
- Adult Standard: meals $12, total $2,970.
- Adult Standard + Child Vegetarian: meals $24, total $2,982.
- Adult Vegan + Child Vegetarian + Infant Standard: meals $36, total $2,994.

Dataset Results:
- All four options available — PASS.
- Independent passenger choices — PASS.
- None/Standard/Vegetarian/Vegan selection coverage — PASS.

### TC-5.3-01 — Add travel insurance to booking price

TC ID: TC-5.3-01

Story: US-5.3

Title: Add travel insurance to booking price

Preconditions:
1. Extras page is displayed.
2. Insurance option is available.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. 0 bags; all meals None; no promo; insurance off→on.

Execution Steps Actually Performed:
1. Restored all meals to None and recorded total $2,958.
2. Enabled the Travel insurance checkbox.
3. Inspected the insurance line and total.

Expected Result:
Travel insurance is added as a flat-rate opt-in charge, appears in the price and is included exactly once.

Actual Result:
Enabling insurance added one $19 charge. The breakdown showed Travel insurance $19.00 and total $2,977.00, exactly $19 above the $2,958.00 baseline.

Test Status:
PASS

Evidence:
- UI label: “$19 flat · trip cancellation & delay cover”.
- Only one insurance line was present; 2,958 + 19 = 2,977.

### TC-5.4-01 — Apply valid promo code exactly once

TC ID: TC-5.4-01

Story: US-5.4

Title: Apply valid promo code exactly once

Preconditions:
1. Promo code field is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. 0 bags; meals None; insurance off; SAVE10 applied three times.

Execution Steps Actually Performed:
1. Disabled insurance and recorded undiscounted total $2,958.
2. Entered SAVE10 and clicked Apply; recorded discount and total.
3. Clicked Apply a second and third time, recording both changes.

Expected Result:
The valid promo is applied successfully and exactly once.
Repeated clicks/applications do not duplicate or compound the discount.

Actual Result:
SAVE10 initially showed a $291 discount and total $2,667. Repeated applications increased the discount to $583 and then $874, reducing the total to $2,375 and $2,084. The discount was not limited to one application.

Test Status:
FAIL

Evidence:
- Toast: “Promo code applied — 10% off your fare.”
- Applications 1/2/3: −$291 / −$583 / −$874.

Dataset Results:
- Valid code initially accepted — PASS.
- Repeated application does not duplicate discount — FAIL.

Proposed bug reference(s): BUG-17.

### TC-5.4-02 — Reject invalid promo code

TC ID: TC-5.4-02

Story: US-5.4

Title: Reject invalid promo code

Preconditions:
1. Promo code field is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. 0 bags; meals None; insurance off; no active promo; TEST.

Execution Steps Actually Performed:
1. Removed the prior promo and reselected None to restore the visible baseline to $2,958.
2. Entered TEST and clicked Apply.
3. Recorded the message, applied-code indicator and total.

Expected Result:
The invalid promo code is not applied.
A clear error is displayed.
The booking price is not incorrectly discounted.

Actual Result:
TEST was displayed as applied and produced the success message “Promo code applied!” rather than an error. The breakdown showed Promo TEST −$0.00 and the total remained $2,958.00.

Test Status:
FAIL

Evidence:
- “TEST applied”.
- “Promo code applied!”.
- Price before and after: $2,958.00.

Dataset Results:
- Invalid code rejected — FAIL.
- Clear error — FAIL.
- No incorrect price discount — PASS.

Proposed bug reference(s): BUG-18.

### TC-5.4-03 — Remove promo and recalculate total

TC ID: TC-5.4-03

Story: US-5.4

Title: Remove promo and recalculate total

Preconditions:
1. A valid SAVE10 promo is applied.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. 0 bags; meals None; insurance off; SAVE10 once, then removed.

Execution Steps Actually Performed:
1. Removed TEST and refreshed the displayed baseline via None: $2,958.
2. Applied SAVE10 once and recorded $291 discount and $2,667 total.
3. Clicked the ✕ beside SAVE10.
4. Inspected the resulting breakdown without making another price change.

Expected Result:
The promo discount is removed and the booking total is correctly recalculated to the appropriate non-discounted amount.

Actual Result:
Removing SAVE10 removed its applied label and discount line, but the total stayed at $2,667 instead of returning to $2,958. The remaining visible lines were Fares $2,913 and Taxes & fees $45 with zero extras.

Test Status:
FAIL

Evidence:
- Before promo: $2,958.
- With promo: $2,667.
- After removal: $2,667; visible non-discounted lines sum to $2,958.
- A later None selection restored $2,958 as cleanup; removal alone did not.

Proposed bug reference(s): BUG-19.

### TC-6.1-01 — Accept valid payment details

TC ID: TC-6.1-01

Story: US-6.1

Title: Accept valid payment details

Preconditions:
1. Payment page is displayed.
2. Booking is ready for payment.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 1 Infant. Selected CJ 101, CoastJet Regional, 09:45–12:57, A319, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Test Infant (Infant), DOB 2025-12-01; no infant passport fields displayed. Seats Adult 1A, Child 1C; all extras zero; no promo. Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C checked.

Execution Steps Actually Performed:
1. Cleared the promo and refreshed the undiscounted total to $2,958.
2. Continued to Payment and entered all five specified valid payment values.
3. Checked the fare-rules/T&C checkbox.
4. Clicked Pay now.

Expected Result:
All valid payment details are accepted and payment can proceed successfully.

Actual Result:
The practice payment completed successfully and Booking confirmed displayed code BK-70-41 with total paid $2,958.00.

Test Status:
PASS

Evidence:
- Confirmation: 1 adult(s), 1 child(ren), 1 infant(s); Economy; VLM→HDX, Mon, Sep 28.
- No real charge is performed by this practice site.

### TC-6.1-02 — Validate required payment fields, expiry and CVV

TC ID: TC-6.1-02

Story: US-6.1

Title: Validate required payment fields, expiry and CVV

Preconditions:
1. Payment page is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101; Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Seat 1A; all extras zero; total $1,067; T&C checked. Valid baseline: Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. A: all five fields blank, then populated card/expiry/CVV in sequence while name and ZIP stayed blank. B: expiry 01/20. C: expiry 0829. D: CVV 12. E: CVV 12345. F: CVV abc.

Execution Steps Actually Performed:
1. Built a fresh valid single-adult booking and opened blank Payment.
2. Submitted all fields blank; recorded card validation.
3. Entered valid card and resubmitted; recorded expiry validation.
4. Entered 08/29 and resubmitted; recorded CVV validation.
5. Entered CVV 123, leaving name and ZIP blank, and resubmitted.
6. Built a new booking and submitted otherwise valid data with expiry 01/20.
7. Built another booking and submitted expiry 0829; recorded rejection.
8. Restored expiry to 08/29 and submitted CVV 12.
9. Built new bookings separately for CVV 12345 and CVV abc; entered otherwise valid data, accepted T&C and submitted each.

Expected Result:
Card number, name on card, expiry, CVV and ZIP are required.
Expiry must be in valid MM/YY format and cannot be in the past.
CVV must contain exactly 3–4 numeric digits.
Invalid payment data is rejected with clear validation.

Actual Result:
Blank card, expiry and CVV were rejected in sequence, but payment completed with both name and ZIP blank. Past expiry 01/20 and CVVs 12, 12345 and abc each completed a booking. Expiry 0829 was rejected with “Enter expiry as MM/YY.”

Test Status:
FAIL

Evidence:
- Blank card: “Enter a valid card number.”
- Blank expiry / 0829: “Enter expiry as MM/YY.”
- Blank CVV: “Enter your card security code.”
- A blank name/ZIP completion: BK-70-65.
- B past expiry: BK-70-28; D short CVV: BK-70-67; E long CVV: BK-70-22; F alphabetic CVV: BK-70-49.
- Every completed dataset displayed total paid $1,067.00.

Dataset Results:
- A required fields — FAIL overall: card PASS; expiry PASS; CVV PASS; name FAIL; ZIP FAIL.
- B past expiry — FAIL.
- C invalid MM/YY format — PASS (0829 rejected).
- D CVV under 3 digits — FAIL.
- E CVV over 4 digits — FAIL.
- F nonnumeric CVV — FAIL.

Proposed bug reference(s): BUG-20, BUG-21, BUG-22.

### TC-6.2-01 — Block payment until T&C are accepted

TC ID: TC-6.2-01

Story: US-6.2

Title: Block payment until T&C are accepted

Preconditions:
1. Payment page is displayed.
2. All payment fields contain otherwise valid values.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 0 Children, 0 Infants. CJ 101; Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Seat 1A; zero extras; Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C unchecked.

Execution Steps Actually Performed:
1. Started a new valid single-adult booking and reached Payment.
2. Entered all valid payment fields and verified checkbox value 0 (unchecked).
3. Clicked Pay now.
4. Recorded completion; the test’s conditional retry after acceptance did not apply because booking had already completed.

Expected Result:
Payment is blocked while T&C/fare rules are unchecked.
Payment becomes eligible to proceed after acceptance.

Actual Result:
Payment completed while the fare-rules/T&C checkbox was unchecked. Booking confirmed displayed BK-70-08 and total paid $1,067.00; no acceptance validation was shown.

Test Status:
FAIL

Evidence:
- Checkbox immediately before Pay: unchecked.
- Confirmation: BK-70-08.

Dataset Results:
- Block unchecked payment — FAIL.
- Conditional checked retry — Not applicable: first payment already completed, as allowed by step 4.

Proposed bug reference(s): BUG-23.

### TC-6.3-01 — Verify complete booking price calculation

TC ID: TC-6.3-01

Story: US-6.3

Title: Verify complete booking price calculation

Preconditions:
1. Booking contains at least one Adult and one Child.
2. Price breakdown is displayed.

Exact Test Data Used:
Vellamar (VLM) → Halden Cross (HDX); one-way; departure 2026-09-28; Economy; 1 Adult, 1 Child, 0 Infants. CJ 101, $1,022 per adult. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Seats 1A/1C; 0 bags; meals None; no insurance/promo.

Execution Steps Actually Performed:
1. Created the listed Adult/Child booking and inspected its passenger-stage breakdown.
2. Entered valid details and assigned distinct seats.
3. Continued through zero extras to Payment and inspected the final breakdown.
4. Recorded every visible price line and added them arithmetically.
5. Checked whether individual passenger fare lines and a tax-scaling basis were exposed.

Expected Result:
Taxes and fees scale correctly.
Each Child is billed the Child fare exactly once.
The displayed booking total equals the sum of all displayed line items.

Actual Result:
The displayed lines summed correctly: Fares $2,811 + Taxes & fees $45 + zero extras = Total $2,856. However, the UI exposed only aggregate Fares, with no individual Child fare or tax basis. Exact-once Child billing and correct tax scaling could not be verified without inferring hidden calculations, so the overall case is BLOCKED.

Test Status:
BLOCKED

Evidence:
- Visible at Passenger details, Extras and Payment: Fares $2,811.00; Taxes & fees $45.00; Extra baggage $0.00; Meals $0.00; Travel insurance $0.00; Total $2,856.00.
- For context, the observed single-adult booking also showed $45 taxes; the UI supplied no rate/rule to establish a correct expected tax amount.

Dataset Results:
- Visible line-item sum — PASS: $2,856 = $2,856.
- Child charged exactly once — BLOCKED: no Child fare line.
- Tax scaling correctness — BLOCKED: no visible tax basis/rule.

### TC-7.1-01 — Generate unique confirmation codes

TC ID: TC-7.1-01

Story: US-7.1

Title: Generate unique confirmation codes

Preconditions:
1. Two bookings can be completed within the same browser/session.

Exact Test Data Used:
Same live tab/session without reload between bookings. A: VLM→HDX 2026-09-28, Economy, CJ 101, 1 Adult+1 Child, seats 1A/1C, $2,856. B: same route/date/cabin/flight, 1 Adult, seat 1A, $1,067. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C accepted; no extras/promo.

Execution Steps Actually Performed:
1. Completed Booking A with valid payment and recorded BK-70-39.
2. Clicked Start a new booking without reloading or ending the session.
3. Reduced Children from 1 to 0 and completed Booking B with valid details, seat and payment.
4. Recorded BK-70-78 and compared it with Booking A.
5. Opened Session bookings and verified both entries were present.

Expected Result:
Booking A and Booking B have different confirmation codes.
No two bookings in the same session share the same code.

Actual Result:
Booking A received BK-70-39 and Booking B received BK-70-78 in the same uninterrupted session. The codes differed, and both appeared separately in Session bookings.

Test Status:
PASS

Evidence:
- A: BK-70-39, $2,856.00.
- B: BK-70-78, $1,067.00.
- The session history showed both codes; no uniqueness guarantee beyond the observed bookings is inferred.

### TC-7.2-01 — Verify confirmation summary matches booking

TC ID: TC-7.2-01

Story: US-7.2

Title: Verify confirmation summary matches booking

Preconditions:
1. A booking can be completed successfully.

Exact Test Data Used:
VLM→HDX; 2026-09-28; one-way Business; Northern Skyline NS 845, 09:05–17:07, 8h 02m, 1 stop, E195-E2, $1,557 per adult; 1 Adult+1 Child. Test User (Adult), DOB 1990-01-15, passport QA1234567, expiry 2030-12-31, email rahaf.test@example.com, phone 0791234567. Synthetic QA identity. Test Child (Child), DOB 2016-01-15, passport QC1234567, expiry 2030-12-31. Seats 3A/3B. One bag $35; Adult Vegan and Child Vegetarian meals $24; insurance $19; no promo. Card 4111 1111 1111 1111; name Test User; expiry 08/29; CVV 123; ZIP 94107. T&C accepted.

Execution Steps Actually Performed:
1. Started a new booking, selected Business and added one Child.
2. Searched and recorded NS 845 itinerary; selected it.
3. Entered valid Adult/Child details, selected available seats 3A and 3B.
4. Added one bag, Vegan/Vegetarian meals and insurance.
5. Recorded Payment total $4,405 and the cabin/passenger/route information.
6. Entered valid payment, accepted T&C, completed booking and compared the confirmation.

Expected Result:
The confirmation summary accurately displays the booked itinerary, passengers, cabin and total paid.
The displayed total matches the completed booking charge.

Actual Result:
Confirmation BK-70-82 displayed VLM→HDX, Mon, Sep 28, 1 adult(s), 1 child(ren), 0 infant(s), Business, and total paid $4,405.00. These matched the recorded booking route/date, passenger counts, cabin and pre-payment total.

Test Status:
PASS

Evidence:
- Pre-payment breakdown: $4,282 fares + $45 taxes + $35 baggage + $24 meals + $19 insurance = $4,405.
- Confirmation summary presents route/date and passenger counts; it does not list passenger names, flight number or flight times.

Dataset Results:
- Displayed itinerary route/date — PASS.
- Passenger counts — PASS.
- Cabin — PASS.
- Total paid vs pre-payment total — PASS.

### TC-7.3-01 — Clear previous data when starting a new booking

TC ID: TC-7.3-01

Story: US-7.3

Title: Clear previous data when starting a new booking

Preconditions:
1. A booking containing flight, passenger, seat, extras and payment selections has been completed.

Exact Test Data Used:
Completed booking BK-70-82 from TC-7.2-01: VLM→HDX, 2026-09-28, one-way, Business, 1 Adult+1 Child, Test User/Test Child, seats 3A/3B, one bag, Vegan/Vegetarian meals, insurance on, valid payment, T&C checked. Fresh inspection data: Reset Adult, DOB 1991-02-16, passport QR1234567, expiry 2031-12-31, reset.test@example.com, 0791234568; Reset Child, DOB 2017-02-16, passport QR7654321, expiry 2031-12-31.

Execution Steps Actually Performed:
1. Recorded the completed booking’s selected values and clicked Start a new booking.
2. Inspected search fields and passenger counts before making new selections.
3. Submitted search and explicitly selected NS 845 to reach Passenger details; inspected the blank fields.
4. Entered the listed new Reset identities only to reach later pages.
5. Inspected Seat selection before assigning any seats; then assigned fresh 3A/3B to continue.
6. Inspected Extras without adding extras, then continued to Payment and inspected all fields and T&C.

Expected Result:
The previous flight, passenger, seat, extras and payment selections are cleared so the user starts with a fresh booking state.

Actual Result:
Start a new booking retained the VLM→HDX route, 2026-09-28 departure, One-way trip, Business cabin, and counts of 1 Adult and 1 Child. Passenger identity/contact fields were blank, seats were unassigned (0/2), baggage was 0, meals were None, insurance was unchecked, promo was blank, all payment fields were blank and T&C was unchecked. The booking was only partially reset.

Test Status:
FAIL

Evidence:
- Retained non-default values: One-way, Business, Child count 1.
- Return field still contained disabled 2026-10-05 (also present before reset).
- Prior fare breakdown disappeared at Search; a new flight had to be selected.
- Seats before new assignment: 0/2; Extras $0; new Payment fields blank.

Dataset Results:
- Trip/cabin/passenger-count reset — FAIL.
- Passenger identity/contact reset — PASS.
- Seat assignment reset — PASS.
- Extras reset — PASS.
- Payment/T&C reset — PASS.

Proposed bug reference(s): BUG-24.

### Flight detail evidence matrix (TC-2.3-01)

All six flights were observed for VLM→HDX, 2026-09-28, Economy. The row order below is the duration-sort order used during detail inspection.

| Airline / flight | Departure | Arrival | Duration | Stops | Aircraft | Seats remaining | Price per adult |
| --- | --- | --- | --- | --- | --- | --- | --- |
| CoastJet Regional / CJ 101 | 09:45 VLM | 12:57 HDX | 3h 12m | Nonstop | A319 | 9 seats left | $1,022.00 |
| Northern Skyline / NS 675 | 05:40 VLM | 08:56 HDX | 3h 16m | Nonstop | 737 MAX 8 | 7 seats left | $1,350.00 |
| AeroLuna / AL 168 | 17:25 VLM | 21:05 HDX | 3h 40m | Nonstop | A319 | Only 2 left (amber) | $595.00 |
| CoastJet Regional / CJ 862 | 20:45 VLM | 01:03 +1 HDX | 4h 18m | 2 stops | A319 | 6 seats left | $491.00 |
| Northern Skyline / NS 261 | 22:10 VLM | 03:21 +1 HDX | 5h 11m | 1 stop | E195-E2 | 9 seats left | $636.00 |
| AeroLuna / AL 457 | 21:45 VLM | 06:01 +1 HDX | 8h 16m | 1 stop | A320neo | Only 2 left | $105.00 |

## 4. BUG SUMMARY

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

## 5. TRACEABILITY MAPPING

| Epic | Story | TC | Result | Bug |
| --- | --- | --- | --- | --- |
| Epic 1 — FLIGHT SEARCH | US-1.1 | TC-1.1-01 | PASS | — |
| Epic 1 — FLIGHT SEARCH | US-1.1 | TC-1.1-02 | FAIL | BUG-01 |
| Epic 1 — FLIGHT SEARCH | US-1.1 | TC-1.1-03 | PASS | — |
| Epic 1 — FLIGHT SEARCH | US-1.1 | TC-1.1-04 | FAIL | BUG-02 |
| Epic 1 — FLIGHT SEARCH | US-1.1 | TC-1.1-05 | FAIL | BUG-03 |
| Epic 1 — FLIGHT SEARCH | US-1.1 | TC-1.1-06 | FAIL | BUG-04 |
| Epic 1 — FLIGHT SEARCH | US-1.2 | TC-1.2-01 | FAIL | BUG-04 |
| Epic 1 — FLIGHT SEARCH | US-1.2 | TC-1.2-02 | FAIL | BUG-05 |
| Epic 1 — FLIGHT SEARCH | US-1.2 | TC-1.2-03 | PASS | — |
| Epic 2 — SEARCH RESULTS | US-2.1 | TC-2.1-01 | FAIL | BUG-06 |
| Epic 2 — SEARCH RESULTS | US-2.1 | TC-2.1-02 | PASS | — |
| Epic 2 — SEARCH RESULTS | US-2.1 | TC-2.1-03 | PASS | — |
| Epic 2 — SEARCH RESULTS | US-2.2 | TC-2.2-01 | FAIL | BUG-07 |
| Epic 2 — SEARCH RESULTS | US-2.2 | TC-2.2-02 | PASS | — |
| Epic 2 — SEARCH RESULTS | US-2.3 | TC-2.3-01 | PASS | — |
| Epic 3 — PASSENGER DETAILS | US-3.1 | TC-3.1-01 | PASS | — |
| Epic 3 — PASSENGER DETAILS | US-3.1 | TC-3.1-02 | FAIL | BUG-08, BUG-09 |
| Epic 3 — PASSENGER DETAILS | US-3.2 | TC-3.2-01 | PASS | — |
| Epic 3 — PASSENGER DETAILS | US-3.2 | TC-3.2-02 | FAIL | BUG-10, BUG-11 |
| Epic 3 — PASSENGER DETAILS | US-3.3 | TC-3.3-01 | PASS | — |
| Epic 3 — PASSENGER DETAILS | US-3.3 | TC-3.3-02 | FAIL | BUG-12 |
| Epic 4 — SEAT SELECTION | US-4.1 | TC-4.1-01 | FAIL | BUG-13 |
| Epic 4 — SEAT SELECTION | US-4.1 | TC-4.1-02 | PASS | — |
| Epic 4 — SEAT SELECTION | US-4.2 | TC-4.2-01 | FAIL | BUG-14 |
| Epic 5 — EXTRAS & PROMO CODES | US-5.1 | TC-5.1-01 | FAIL | BUG-15, BUG-16 |
| Epic 5 — EXTRAS & PROMO CODES | US-5.2 | TC-5.2-01 | PASS | — |
| Epic 5 — EXTRAS & PROMO CODES | US-5.3 | TC-5.3-01 | PASS | — |
| Epic 5 — EXTRAS & PROMO CODES | US-5.4 | TC-5.4-01 | FAIL | BUG-17 |
| Epic 5 — EXTRAS & PROMO CODES | US-5.4 | TC-5.4-02 | FAIL | BUG-18 |
| Epic 5 — EXTRAS & PROMO CODES | US-5.4 | TC-5.4-03 | FAIL | BUG-19 |
| Epic 6 — PAYMENT | US-6.1 | TC-6.1-01 | PASS | — |
| Epic 6 — PAYMENT | US-6.1 | TC-6.1-02 | FAIL | BUG-20, BUG-21, BUG-22 |
| Epic 6 — PAYMENT | US-6.2 | TC-6.2-01 | FAIL | BUG-23 |
| Epic 6 — PAYMENT | US-6.3 | TC-6.3-01 | BLOCKED | — |
| Epic 7 — CONFIRMATION & HISTORY | US-7.1 | TC-7.1-01 | PASS | — |
| Epic 7 — CONFIRMATION & HISTORY | US-7.2 | TC-7.2-01 | PASS | — |
| Epic 7 — CONFIRMATION & HISTORY | US-7.3 | TC-7.3-01 | FAIL | BUG-24 |

## 6. BLOCKED / NOT FULLY EXECUTABLE TESTS

### TC-6.3-01 — BLOCKED

The final Payment UI showed Fares $2,811.00 and Taxes & fees $45.00, plus zero extras, totaling $2,856.00. It did not expose a per-Child fare line, fare rate, tax rate or tax basis. Therefore the exact-once Child billing and tax-scaling checks could not be completed through the rendered UI. The sum of displayed lines was verified and passed. The same aggregate-only presentation was observed at Passenger details and Extras. No extra UI control to expand passenger fare lines was shown on those screens.

No other test has a blocked outcome. TC-6.2-01’s conditional accepted-T&C retry was not applicable because the unchecked submission had already completed; this is a FAIL, not a blocker. The baggage test stopped at the allowed “clearly unreasonable quantity” condition of 20 bags; no untested maximum is claimed. The confirmation-code PASS is based on the specified two observed bookings, not an inferred system-wide guarantee.

## 7. FINAL QUALITY CHECK

- Exactly 37 unique TC IDs are present in the execution table and detailed records.
- All supplied TC IDs are accounted for; none is omitted or duplicated in the execution table.
- Every TC has an Actual Result and PASS/FAIL/BLOCKED status.
- All 20 FAIL cases reference one or more of the 24 unique proposed bugs.
- Every proposed bug has a severity and affected TC/story links.
- Multi-dataset outcomes are listed separately.
- 16 + 20 + 1 = 37.
- Evidence is recorded as observed UI values, messages and states. No fabricated screenshot files or hidden-calculation claims are included.
- No Jira or Xray mutations were performed.
