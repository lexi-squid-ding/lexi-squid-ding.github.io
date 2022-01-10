---
title: "SQL: Filter your coffee on multiple conditions"
date: 2022-01-09
categories:
  - blog
tags:
  - SQL
  - Data Science
  - Snowflake
---

_Which is better for selecting, multiple queries with one condition for each or one query with multiple conditions using OR?_

Let's say you have a SQL table containing coffee products, the companies they come from, and whether the product is foreign (vs. domestic). 

```sql
CREATE TABLE coffee_products (
product_id varchar(225),
company_name varchar(225),
is_foreign boolean,
);
```

To get all domestic products from [Sightglass](https://sightglasscoffee.com/) and [Philz Coffee](https://www.philzcoffee.com/), and both domestic/international products from [Souvenir](https://www.souvenir-coffee.com/), your first idea might be to add a boolean filter for each of the 3 company criteria like so (don't forget parentheses!):

```sql
SELECT * FROM coffee_products cp
WHERE (cp.company_name = 'sightglass' AND is_foreign=FALSE)
OR (cp.company_name = 'philz' AND is_foreign=FALSE)
OR (cp.company_name = 'souvenir')
```

However, this is actually scanning the data thrice (one for each criterion)!

Creating a single boolean condition by adding outside parens is more efficient. Consolidating the queries cut my query runtime on a real dataset from 1.5 hours to 10 minutes. 

```sql
SELECT * FROM coffee_products cp
WHERE ((cp.company_name = 'sightglass' AND is_foreign=FALSE)
    OR (cp.company_name = 'philz' AND is_foreign=FALSE)
    OR (cp.company_name = 'souvenir')
    )
```

Be careful with your coffee filters!
- Lexi
