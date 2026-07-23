<p align="center">
  <img src="https://raw.githubusercontent.com/dbwarden-org/dbwarden/main/assets/icon.png" alt="DBWarden" width="128"/>
</p>
<p align="center">
  <strong style="font-size: 2.5em;">DBWarden</strong>
</p>
<p align="center">
  <em>Your SQLAlchemy models are your migrations.</em>
</p>

<p align="center">
  <a href="https://www.python.org/downloads/">
    <img src="https://img.shields.io/badge/Python-3.12%2B-3776AB?logo=python&logoColor=white&style=for-the-badge" alt="Python">
  </a>
  <a href="https://pypi.org/project/dbwarden/">
    <img src="https://img.shields.io/pypi/v/dbwarden?logo=pypi&logoColor=white&style=for-the-badge" alt="PyPI">
  </a>
  <a href="https://github.com/dbwarden-org/dbwarden/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-10AC84?style=for-the-badge" alt="License">
  </a>
  <a href="https://dbwarden.emiliano-go.com/">
    <img src="https://img.shields.io/badge/Docs-87%20pages-blue?logo=readthedocs&logoColor=white&style=for-the-badge" alt="Documentation">
  </a>
  <a href="https://codecov.io/gh/dbwarden-org/dbwarden">
    <img src="https://img.shields.io/codecov/c/github/dbwarden-org/dbwarden?logo=codecov&logoColor=white&style=for-the-badge" alt="Codecov">
  </a>
</p>

---

**DBWarden** is a model‑first database migration system built on SQLAlchemy.  
Define your schema in Python, review the generated SQL, and apply it with confidence, backed by a convergence gate that **proves** your migrations match your models.

This organization is the home of the DBWarden project and its official plugins.

---

## Community & Approved Plugins

Community plugins use the same entry‑point mechanism.  
Before they run, DBWarden asks for your explicit consent. No third‑party code executes without your knowledge.

[**→ Browse community plugins**](https://pypi.org/search/?q=dbwarden-)  
[**→ Learn about the Approved tier**](https://dbwarden.emiliano-go.com/plugins/approved-standard/)

---

## Quickstart

```bash
# install DBWarden
uv add dbwarden

# create a configuration
echo "
from dbwarden import database_config

database_config(
    database_name='primary',
    database_type='postgresql',
    database_url='postgresql://localhost/myapp',
)
" > dbwarden.py

# generate your first migration
dbwarden make-migrations "create initial tables"

# apply it
dbwarden migrate
```

---

## Documentation

Full documentation with guides, cookbook, and API reference:  
**[dbwarden.emiliano-go.com](https://dbwarden.emiliano-go.com/)**

---

## Contributing

We welcome contributions to the core tool and to plugins.  
Start with the [core contribution guide](https://github.com/dbwarden-org/dbwarden/blob/main/CONTRIBUTING.md) or jump into any plugin’s issue tracker.

---

## License

DBWarden and all official plugins are released under the **MIT License**.
