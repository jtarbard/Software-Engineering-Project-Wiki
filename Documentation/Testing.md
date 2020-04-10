# Note to self
* Fixture: in `conftest.py`. E.g. `def new_item()`, pass fixtures in parameters and you can call them
* `pytest --setup-show tests/functional/` shows how conftest.py is being called
* `-v` probably means verbose. It shows PASS and FAILED for each test. Runs all tests.

My format (as of now):
3 "categories/levels"
1. Basic - testing the explicitly handled cases (written code) works properly ( = intended handling behaviour )
2. Extra - testing non-explicit cases works properly in the function
3. Edge - weird and unconventional use of the routes. These are difficult tests but should still pass

## Login (Outdated Done, assert flash as error msg)
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

## (Outdated Done, assert flash as error msg) Register

## Preserved login state

## (Done) Non-volatile Database
No Test.

## Database population script

## (Outdated Done) Prototypical Homepage UI with page redirection: Index page

## Viewing the full list of activities in the database

## Book and pay for an activity at a specified date and time (the payment is not simulated yet)

## Store booking history (as receipts in database), display all booking history on demand

## (Done) Buy membership (with duration)

## (Done) Apply membership discount

## Cash/Card payment simulation

## Generate QR-code for receipts

## Generate PDF for receipts

## Mailing receipts

## Search for activities between time slots, with specific activities names and facility usage

## (Done) Cancel booking

## Facility Images

## (Done) Bulk book with discount

- [ ] <Rule '/activities/types' (POST, HEAD, OPTIONS, GET) -> activities.view_activity_types>
- [ ] <Rule '/account/view_statistics' (POST, HEAD, OPTIONS, GET) -> account.view_usages>
- [ ] <Rule '/account/membership' (HEAD, OPTIONS, GET) -> account.view_account_membership>
- [x] <Rule '/account/register' (HEAD, OPTIONS, GET) -> account.register_get>
- [ ] <Rule '/account/receipts' (HEAD, OPTIONS, GET) -> account.view_account_receipts>
- [ ] <Rule '/account/bookings' (HEAD, OPTIONS, GET) -> account.view_account_bookings>
- [ ] <Rule '/account/details' (POST, HEAD, OPTIONS, GET) -> account.view_account_details>
- [x] <Rule '/account/log_out' (HEAD, OPTIONS, GET) -> account.log_out>
- [x] <Rule '/account/basket' (HEAD, OPTIONS, GET) -> basket.basket_view>
- [x] <Rule '/account/login' (HEAD, OPTIONS, GET) -> account.login_get>
- [ ] <Rule '/account/home' (HEAD, OPTIONS, GET) -> account.view_account>
- [ ] <Rule '/account/card' (POST, HEAD, OPTIONS, GET) -> account.view_payment_details>
- [x] <Rule '/info/memberships' (HEAD, OPTIONS, GET) -> info.membership_view>
- [x] <Rule '/info/memberships/cancel' (HEAD, OPTIONS, GET) -> info.cancel_membership>
- [x] <Rule '/info/memberships/buy' (OPTIONS, POST) -> info.buy_membership>
- [ ] <Rule '/info/contact_us' (HEAD, OPTIONS, GET) -> info.contact_us_view>
- [ ] <Rule '/info/facilities' (HEAD, OPTIONS, GET) -> info.facilities_view>
- [ ] <Rule '/info/about' (HEAD, OPTIONS, GET) -> info.about_func>
- [x] **<Rule '/misc/policy_info' (HEAD, OPTIONS, GET) -> misc.policy_info_view>**
- [ ] <Rule '/misc/help' (HEAD, OPTIONS, GET) -> misc.help_view>
- [x] **<Rule '/' (HEAD, OPTIONS, GET) -> index.index_func>**
- [ ] <Rule '/transactions/view_individual_receipts/<receipt_id>' (HEAD, OPTIONS, GET) -> transaction.e_m_get>
- [ ] <Rule '/transactions/receipts/<encrypted_receipt>' (HEAD, OPTIONS, GET) -> transaction.receipt_get>
- [ ] <Rule '/activities/view_activities' (POST, HEAD, OPTIONS, GET) -> activities.view_activities>
- [ ] <Rule '/activities/view_activity/<activity_id>' (HEAD, OPTIONS, GET) -> activities.view_activity>
- [ ] <Rule '/activities/<sent_activity>_<multiple>' (POST, HEAD, OPTIONS, GET) -> activities.view_activities>
- [ ] <Rule '/static/<filename>' (HEAD, OPTIONS, GET) -> static>