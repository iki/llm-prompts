Convert the MySQL input to Markdown table while following the output rules.

# Output Rules

- remove comments
- for each table use PascalCase model name
- for each field use camelCase field name
- for each field value convert it to utf-8 encoding from charset specified in field or table definition (if present, in that order)
- for each table output markdown table with camelCase field names in header and field values in rows

# MySQL Input

```sql

```
