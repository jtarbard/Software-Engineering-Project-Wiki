The demo mode hosts the server locally at `127.0.0.1:5000`. You can access the website via that IP address.

When starting the server for the first time (or when the "the_vertex.sqlite" database file does not exist), the database will get generated with demo data populated. This will take up about 10 minutes (the time taken is mostly due to bookings). These data include:
- Facilities
- Employee Roles
- Activities (sessions) - the session times are random everytime, so no dates are hard coded.
- Memberships
- Bookings - 1-3 bookings will be made for each session. This is for demonstrating manager statistics.
- Accounts: there are 3 accounts, 1 for each role. These are `team_10_c@leeds.ac.uk` for customer; `team_10_e@leeds.ac.uk` for employee; and `team_10_m@leeds.ac.uk` for manager. Their passwords are the same: `WeAreTeam10`.