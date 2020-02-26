# Critical Issues
Issues here should be checked and fixed automatically in scripts in the final build. They can be done anytime.

| Issue | Solution |
| ------ | ------ |
| `logs` and `main/db` folders need exist | Create empty folders with those names |
| FileNotFound: `~[project_path]/main/logs/...` is not found | Append/Remove `/main` in the working directory of PyCharm configuration | 
| ModuleNotFound: `main` | Append/Remove `/main` in the working directory of PyCharm configuration | 
| ModuleNotFound: `flask` (, passlib, etc.) | Check Python Interpreter in PyCharm Settings, add the missing modules |