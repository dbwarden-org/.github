<p align="center">
  <img src="https://raw.githubusercontent.com/dbwarden-org/dbwarden/main/assets/icon.png" alt="DBWarden" width="128"/>
</p>
<p align="center">
  <strong style="font-size: 2.5em;">DBWarden</strong>
</p>
<p align="center">
  <em>Your models are the source code. SQL is the output.</em>
</p>

<p align="center">
  <a href="https://www.python.org/downloads/">
    <img src="https://img.shields.io/badge/Python-3.12.7%2B-3776AB?logo=python&logoColor=white&style=for-the-badge" alt="Python">
  </a>
  <a href="https://pypi.org/project/dbwarden/">
    <img src="https://img.shields.io/pypi/v/dbwarden?logo=pypi&logoColor=white&style=for-the-badge" alt="PyPI">
  </a>
  <a href="https://github.com/dbwarden-org/dbwarden/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-10AC84?style=for-the-badge" alt="License">
  </a>
  <a href="https://docs.dbwarden.org/">
    <img src="https://img.shields.io/badge/Docs-docs.dbwarden.org-blue?logo=readthedocs&logoColor=white&style=for-the-badge" alt="Documentation">
  </a>
  <a href="https://codecov.io/gh/dbwarden-org/dbwarden">
    <img src="https://img.shields.io/codecov/c/github/dbwarden-org/dbwarden?logo=codecov&logoColor=white&style=for-the-badge" alt="Codecov">
  </a>
</p>

---

**DBWarden** is a declarative schema compiler for SQLAlchemy. You declare the schema you want in your SQLAlchemy models, and DBWarden compiles everything else: migration SQL, rollbacks, snapshots, and safety checks. There are no migration scripts to write or maintain. Your models are the contract.

This organization is the home of the DBWarden project and its official plugins.

---

## Quickstart

```bash
# install DBWarden
uv add dbwarden

# create a configuration
echo "
from dbwarden import DbwardenDatabase

class Primary(DbwardenDatabase):
    database_name = 'primary'
    database_type = 'postgresql'
    database_url_sync = 'postgresql://user:pass@localhost:5432/myapp'
    default = True
" > dbwarden.py

# generate your first migration
dbwarden make-migrations "create initial tables"

# apply it
dbwarden migrate
```

---

## Documentation

Full documentation with guides, cookbook, and API reference:  
**[docs.dbwarden.org](https://docs.dbwarden.org/)**

---

## Contributing

We welcome contributions to the core tool and to plugins.  
Start with the [core contribution guide](https://github.com/dbwarden-org/dbwarden/blob/main/CONTRIBUTING.md) or jump into any plugin’s issue tracker.

---

## License

DBWarden and all official plugins are released under the **MIT License**.
