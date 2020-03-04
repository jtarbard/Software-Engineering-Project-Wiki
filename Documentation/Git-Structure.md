```mermaid
graph TD
  master[master <br> LOCK] --> sprint2(sprint2 <br> LOCK)
  sprint2 --> frontend(frontend <br> LOCK)
  sprint2 --> backend(backend <br> LOCK)

  frontend --> populate[populate-relevant-pages <br> LOCK]
  backend --> payment[payment <br> LOCK]
  backend --> receipt[receipt <br> LOCK]
  backend --> booking[remaining-booking <br> LOCK]
  backend --> membership[membership <br> LOCK]
```
---
Sub-branches will be created from the locked feature branches and worked on by a single pair. Upon completion of the sub-feature the code should be reviewed by an external member/pair and once approved a merge request may be made.