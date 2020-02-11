# Sample Documents
### Receipt template from LeisureMost
An image of a receipt for a sports centre was found via Google. Through sampling this receipt, we derived some possible issues and hints to our future database schemas.

![image](uploads/cae351c5ad391753b3c1a580ae81f2bb/image.png)

| Receipt Fields                                | Note – Hints to our implementation                                                                                                                           |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Receipt Header – Company name, location, contact info | Basic information about the made-up company. Can be included to increase realism. |
|                                               | Missing Table Headers – unclear what each field means |
| **Employee**                                  | Table Name; Obvious Missing Fields – Employee Id |
| Employee: Name                                |                               |
| Employee: Shift Number                        | This is probably too detailed |
| **Transaction**                               | Database Table |
| Transaction: Id                               |   |
| Transaction: DateTime                         |   |
| **Booking Item**                              | Database Table (For look-up) |
| Booking Item: Name                            | Concise description  |
| Booking Item: Quantity                        | This seems to be unnecessary – if the same item is listed multiple times, multiple rows are used instead. Room for improvement. |
| **Price per item**                      | |
| **Price Total**                         | This is not necessary if the quantity is always 1. I think for our implementation we can make use of this aggregated field.                        |
| **Booking Summary**                               | Aggregated fields |
| Summary: Total to pay                        | Calculated by summing all item totals |
| Summary: Payment received                    | This could be needed for generality, since both cash and card payment are accepted. (In the case of card payment, payment received = total to pay) |
| Summary: Change (Received – ToPay)           | |
| Receipt Footer – Thank you message, legal info       |  |



# Interview
### Xercise4less
An interview with the manager of the Leeds Xercise4less gym was not carried out due to weather conditions.



# Research
### Xercise4less
Some research was carried out on the gym "Xercise4less" for hints as to how a real company handles the management & technological issues. Here are a number of insights:
* Mobile App is completely inaccessible unless you have an account.
* Password does not need to be supplied during account creation on web. There are 2 possible explanations:
  - Password is completely unnecessary (but this is proven to not be the case, as the mobile app requires password to authenticate the account login). Users are automatically logged on using locally cached data (e.g. cookies, mobile app cache)
  - Account creation is finalized through a verifiable link in the email. Password is supplied then.
