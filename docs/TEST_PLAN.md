# SkyBook Test Plan

## Objective

Validate the complete SkyBook practice flight-booking flow and document observable behavior from search through confirmation.

## Scope

- Flight search, dates, passenger counts, and cabin selection
- Result sorting, filtering, and flight details
- Passenger contact, identity, and passport details
- Seat selection and assignment rules
- Baggage, meals, travel insurance, and promo codes
- Payment validation, terms acceptance, and price breakdown
- Confirmation codes, booking summary, and starting a new booking

## Approach

Manual functional testing using positive, negative, boundary, and end-to-end scenarios. Results were recorded from the rendered UI. Hidden application data and source code were not used.

## Environment

- Application: [SkyBook Practice Booking](https://claude.ai/code/artifact/5028f8a7-4747-4b7e-b07f-a4dddf65807c)
- Test management: Jira with Zephyr Essential
- Execution date: 2026-09-07
- Time zone recorded by the original execution report: Asia/Riyadh

## Entry Criteria

- Practice site is accessible.
- The flight-search form loads.
- Test data and expected results are defined.

## Exit Criteria

- All 37 planned test cases have an execution result.
- Every failed case has at least one linked defect.
- Traceability covers Epic → Story → Test Case → Bug where applicable.

## Result Summary

- Total: 37
- Passed: 16
- Failed: 20
- Blocked: 1
- Bugs: 24

## Limitation

TC-6.3-01 remained blocked because the UI exposed aggregate fare and tax lines but not the individual child fare or tax calculation basis. The visible arithmetic was verified.
