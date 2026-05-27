# SPARQL Practice — Chapters 1–3

Dataset: [data.ttl](data.ttl) — a small library of sci-fi / fantasy novels, authors and publishers.

Run each query with ARQ:

```powershell
arq --data=data.ttl --query=qNN.rq
```

Save your answers as `q01.rq`, `q02.rq`, … in this folder.

Prefixes you'll likely want:

```sparql
PREFIX lib:  <http://example.org/lib#>
PREFIX d:    <http://example.org/data/>
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dc:   <http://purl.org/dc/elements/1.1/>
PREFIX xsd:  <http://www.w3.org/2001/XMLSchema#>
```

---

## Easy — basic triple patterns

**Q1.** List the title of every book.

**Q2.** List the name of every author.

**Q3.** For every book, return its title and its page count.

**Q4.** Return the URI, title and publication year of every book published in 2008.

---

## Medium — joins, OPTIONAL, FILTER, DISTINCT, UNION

**Q5.** For every book return its title together with the *name* of its author (not the author URI).

**Q6.** Return every book's title and its publication year, **including** books whose year is unknown. Books with no year should still show up.

**Q7.** Return every author who has **not** written any book in this dataset. *(Hint: `FILTER NOT EXISTS` or `MINUS`.)*

**Q8.** List every distinct genre present in the dataset, with no duplicates.

**Q9.** Return the titles of books published by **either** Tor Books **or** Gollancz (use `UNION`).

**Q10.** Return the titles of books with more than 300 pages, published after 1980.

**Q11.** Return the titles of all books, ordered alphabetically, but only the first 5.

---

## Harder — aggregation, BIND, VALUES, subqueries

**Q12.** For each author (by name), return how many books they wrote in this dataset. Sort by count descending.

**Q13.** Return the average page count across all books that have a known page count. *(One row.)*

**Q14.** For each genre, return the year of the most recent book in that genre.

**Q15.** Return one column called `?label` formatted like `"Kindred (1979)"` for every book that has a known year. *(Use `BIND` and `CONCAT` / `STR`.)*

**Q16.** Using `VALUES`, return the books written by either Le Guin or Liu Cixin (look them up by author URI: `d:leguin`, `d:liu`).

**Q17.** Return the names of authors who wrote **more than one** book in this dataset. *(Subquery with `GROUP BY` + `HAVING`, or filter on the count.)*

**Q18.** Find books whose author was born **before 1940**. Return the book title, author name, and birth year.

---

## Stretch — schema lookup & class hierarchy

**Q19.** Use `rdfs:label` on `lib:Book` to fetch the French label of the class `Book`. Return just the label.

**Q20.** `lib:Novel` is declared `rdfs:subClassOf lib:Book`. Write a query that returns every instance of `lib:Book` **including** instances declared only as `lib:Novel`. *(Hint: a property path on `rdf:type`/`rdfs:subClassOf`, e.g. `?b rdf:type/rdfs:subClassOf* lib:Book`.)*
