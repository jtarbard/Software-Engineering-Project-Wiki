# Suggested Branching Behvaiour for Sprint 2
```mermaid
graph TD
  master[LOCK <br> master] --> sprint2(LOCK <br> sprint2)
  sprint2 --> frontend(LOCK <br> frontend)
  sprint2 --> backend(LOCK <br> backend)

  frontend --> populate[LOCK <br> populate-relevant-pages]
  backend --> payment[LOCK <br> payment]
  backend --> receipt[LOCK <br> receipt]
  backend --> booking[LOCK <br> remaining-booking]
  backend --> membership[LOCK <br> membership]

  booking --> booking-iss46
  booking --> booking-iss47
  booking --> booking-iss53
  booking --> booking-iss8

  payment --> payment-iss10
  payment --> payment-iss48
  payment --> payment-iss49
  
  receipt --> receipt-iss50
  receipt --> receipt-iss51
  receipt --> receipt-iss52
  
  membership --> membership-iss5
  membership --> membership-iss6
```

---
Sub-branches will be created from the locked feature branches and worked on by a single pair. Upon completion of the sub-feature the code should be reviewed by an external member/pair and once approved a merge request may be made.