# Kotlin + Spring Cursor Rules

This README is written in English.  
This repo provides **Cursor Rules (`.mdc`)** for consistent **Spring Boot + Kotlin** API/DB/Test conventions.

---

## What is this?

A set of Cursor rules to enforce consistent conventions for **API design**, **JPA/QueryDSL database access**, and **testing with Kotest + MockK** in Spring Boot + Kotlin projects.

---

## How to use in Cursor

Cursor typically loads `.mdc` rule files from `.cursor/rules/`.

- **Option A (recommended)**: Copy this repo’s `rules/*.mdc` into your target project’s `.cursor/rules/`
- **Option B**: Link them using a symbolic link (symlink)

Example:

```bash
mkdir -p .cursor/rules
cp -R rules/*.mdc .cursor/rules/
```

> Note: For team usage, commit the rule files into your project repo and manage them under `.cursor/rules/`.

---

## Contributing / Extending

- If you add new rules under `rules/*.mdc`, also update this README with a short summary.
- Keep rules actionable: write them in **MUST / MUST NOT / SHOULD** form for easier team adoption.
