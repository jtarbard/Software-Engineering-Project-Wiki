# Note to self
* Fixture: in `conftest.py`. E.g. `def new_item()`, pass fixtures in parameters and you can call them
* `pytest --setup-show tests/functional/` shows how conftest.py is being called
* `-v` probably means verbose. It shows PASS and FAILED for each test. Runs all tests.

My format (as of now):
3 "categories/levels"
1. Basic - testing the explicitly handled cases (written code) works properly ( = intended handling behaviour )
2. Extra - testing non-explicit cases works properly in the function
3. Edge - weird and unconventional use of the routes. These are difficult tests but should still pass

## Login
### Basic
---
- User logged in (cookies? ask lewis) - redirect to index page
- No cookies
- Behaviour: Has Basket cookie - remove the basket cookie, redirect to this route (runs this function) again
(Shouldn't this be done when user logs off? redundant test (in a good way)?)
- => Finally, render `login_register.html` with `page_type="login"`

### Extra
---

### Edge
---

## Register

## Preserved login state

## Non-volatile Database

## Database population script

## Prototypical Homepage UI with page redirection

## Viewing the full list of activities in the database

## Book and pay for an activity at a specified date and time (the payment is not simulated yet)

## Store booking history (as receipts in database), display all booking history on demand

## Many-to-many database relationships

## Buy membership (with duration)

## Apply membership discount

## Cash/Card payment simulation

## Generate QR-code for receipts

## Generate PDF for receipts

## Mailing receipts

## Search for activities between time slots, with specific activities names and facility usage

## Cancel booking

## Facility Images

## Bulk book with discount