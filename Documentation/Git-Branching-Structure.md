# Revised Structure - Feature Branch
`Issue`/`Backlog` branches (e.g. `payment-iss10`) stem from the locked `summary` branches (e.g. `payment`). Only 1 pair can work on an `issue`/`backlog` branch at any time, and only 1 person can commit & push to the branch. This is done so to avoid branch-internal merge conflicts.

Upon completion of an `issue` branch, the code should be reviewed by an external member/pair. Once it is approved, a merge request may be made.

#### Note
*  `Issue`/`Backlog` branches should only be created for the **essential** backlog items extracted from the spreadsheet. The lists of valid `issue` branches for each sprint are under each diagram. You can also derive this list by checking whether an issue has the "essential-backlog-item" label.

*  `Issue`/`Backlog` branches should only be created when you are working on it that issue, because some issues might depend on other issues. Also, assign the issue to your lead (Jason/Lewis) before cracking on it!

*  This design does **NOT** limit the branching behaviour at the `backlog` branches level. You can still stem out spaghetti branches (although not encouraged) in your own developing `backlog` branch, as long as you merge everything back into the parent node, with the singular feature you were meant to implement.


# Change in pair programming
The old, static pairs in sprint 1 will be replaced by two dynamically-formed programming pairs, led by either Lewis or Jason, as they are the most knowledgeable in regards to the backend. 

The remaining 4 members will work with either Lewis or Jason to form 2 dynamic pairs. This is done so in attempt to better utilise other team members and increase productivity in backend development.

The remaining 2 members after the 2 pairs have formed will work on the frontend.


# Git Graph notation
*  The nodes with `LOCK` in it means it is **protected** - no one can push to them. They can be merged into its parent node via submitting a merge request (then @VincentLou will handle the merge conflicts).
*  The naming format of a `backlog item` branch is `[summary_branch_name]-iss[issue_number]`. For example, `booking-iss46` indicates that issue #46, which belongs to a larger set of features, *booking*, will be developed in this branch.


# Suggested Branching Behvaiour for Sprint 2
```mermaid
graph TD
  master[LOCK <br> master] --> sprint2(LOCK <br> sprint2)
  sprint2 --> frontend(LOCK <br> frontend)
  sprint2 --> backend(LOCK <br> backend)

  frontend --> pages[LOCK <br> populate-relevant-pages]

  pages --> pages-iss51
  pages --> pages-iss58

  backend --> payment[LOCK <br> payment]
  backend --> receipt[LOCK <br> receipt]
  backend --> booking[LOCK <br> remaining-booking]
  backend --> membership[LOCK <br> membership]

  booking --> booking-iss46
  booking --> booking-iss47
  booking --> booking-iss53
  booking --> booking-iss8
  booking --> booking-iss9

  style booking-iss8 fill:#00EE00

  payment --> payment-iss10
  payment --> payment-iss11
  payment --> payment-iss48
  
  receipt --> receipt-iss50
  receipt --> receipt-iss51
  receipt --> receipt-iss52
  
  membership --> membership-iss5
  membership --> membership-iss6
```

#### Available issue branches names:
- [ ] Remaining-Booking
  - [ ] #46: booking-iss46
  - [ ] #47: booking-iss47
  - [ ] #53: booking-iss53
  - [x] #8: booking-iss8
  - [ ] #9: booking-iss9

- [ ] Payment
    - [ ] #10: payment-iss10
    - [ ] #11: payment-iss11
    - [ ] #48: payment-iss48

- [ ] Receipt
  - [ ] #50: receipt-iss50
  - [ ] #51: receipt-iss51
  - [ ] #52: receipt-iss52

- [ ] Membership
  - [ ] #5: membership-iss5
  - [ ] #6: membership-iss6

- [ ] Populate-Relevant-Pages
  - [ ] #51: pages-iss51
  - [ ] #58: pages-iss58

# Foreseeable problems with this structure
*  If a hotfix needs to be applied, it will need to **propagate** down to every single node, which will cause a ton of merge conflicts.

Possible solution: Attach a hotfix branch to `master`. Only resolve the merge conflict once when merging a sprint branch into the master branch.

(But what if some bug causes everything to cease to function? Then surely the band-aid fix will need to be applied to every branch in order for everyone to continue working... You could argue if we overlooked a bug that severe in the master branch then it's our fault for not noticing it, but surely there's some better way to solve this issue?)