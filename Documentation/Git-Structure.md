# Suggested Branching Behvaiour for Sprint 2
```mermaid
graph TD
  master[fa:fa-lock master fa:fa-lock] --> sprint2(fa:fa-lock sprint2 fa:fa-lock)
  sprint2 --> frontend(fa:fa-lock frontend fa:fa-lock)
  sprint2 --> backend(fa:fa-lock backend fa:fa-lock)

  frontend --> populate[fa:fa-lock populate-relevant-pages fa:fa-lock]
  backend --> payment[fa:fa-lock payment fa:fa-lock]
  backend --> receipt[fa:fa-lock receipt fa:fa-lock]
  backend --> booking[fa:fa-lock remaining-booking fa:fa-lock]
  backend --> membership[fa:fa-lock membership fa:fa-lock]

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