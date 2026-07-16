# App Features Specification — Smart Eco-Mooring Buoy

## Booking

- Users book a **time slot within a bay**, not a specific buoy — the system assigns an available buoy on arrival.
- Three time slots per day: **morning / afternoon / night**.
- Overbooking is managed using an estimated no-show percentage model (similar to airline booking models), applied at the bay/slot level rather than per individual buoy.
- Within a slot, allocation is **first-come, first-served**.
- Free cancellation up to a defined threshold before the slot start (proposed default: 2 hours — to be validated for technical feasibility and ease of implementation).
- Cancelling after the threshold counts as a no-show for overbooking model purposes.

## Check-in

- Hybrid approach: **automatic detection** (e.g. GPS/proximity) combined with **manual confirmation** in the app.
- If check-in doesn't happen within the allotted time, the slot becomes available again for other users within the same bay/slot (unless the bay is already full due to overbooking).

## Deposit

- The former "+fee" concept is implemented as a **refundable security deposit**, not a separate charge.
- The deposit is withheld in cases such as no-show or violations (e.g. anchoring outside the reserved slot/zone).

## Dynamic Pricing

- A predictive wind model (weekly/monthly horizon) estimates beach/bay occupancy: favorable wind forecasts → higher expected boat traffic → higher **booking fee** for that zone/date.
- Dynamic pricing affects **only the booking fee**, not the security deposit.

## Wind Sensors

- Detect safety-relevant wind conditions.
- If a boat is anchored outside its reserved slot or designated zone, it is flagged as an **illegal mooring**.
- Wind data also feeds the predictive occupancy model — particularly useful along coasts with high sailing-boat traffic.

## Coast Guard / Enforcement

- Coast Guard involvement is **on-request only** (not automatically pushed).
- Their role: verify that mooring/parking has been paid for.
- Illegal mooring events detected via wind sensors are **automatically logged but only passively visible** in the dashboard — no automatic push alert is sent to the Coast Guard.

## Data Access

| Role | Data Access |
|---|---|
| Boat owner | Water quality + wind data |
| Coastal Ecosystem Guardian / Coast Guard | Full environmental dataset (all sensors) |

## Open Items

- Final validation of the cancellation threshold (technical feasibility, ease of implementation).
