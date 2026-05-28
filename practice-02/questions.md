# SPARQL Practice 02 — Composants, Fournisseurs, Produits

Dataset: [data.ttl](data.ttl). Schema and themes are adapted from the 2022 BDA exam ([RDF-Exam-Q1-SPARQL-Composants.pdf](../ressources/RDF-Exam-Q1-SPARQL-Composants.pdf)), then extended with supplier countries, component prices, a deeper `:contient` graph, multi-supplier components, and an orphan component with no `:fournisseur`.

Save your answers as `q01.rq`, `q02.rq`, … in this folder.

## Schema reminder

```turtle
:Composant   a rdfs:Class .
:Fournisseur a rdfs:Class .
:Produit     a rdfs:Class .

:fournisseur a rdf:Property ; rdfs:domain :Composant ; rdfs:range :Fournisseur .
:contient    a rdf:Property ; rdfs:domain :Composant ; rdfs:range :Composant .
:utilise     a rdf:Property ; rdfs:domain :Produit   ; rdfs:range :Composant .
```

Extra (not in the exam):

- `:pays` on every `:Fournisseur` (string, e.g. `"UK"`).
- `:prix` on every `:Composant` (integer).
- `rdfs:label` on every URI.

## How to run

```powershell
arq --data=data.ttl --query=qNN.rq
```

## Prefixes you'll likely want

```sparql
PREFIX :     <http://cui.unig.ch/bda/>
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd:  <http://www.w3.org/2001/XMLSchema#>
```

---

## Easy

**Q1.** List the URI of every `:Composant` in the dataset.

**Q2.** List every `:Fournisseur` together with its label and its country (`:pays`).

**Q3.** List every `:Produit` and its label.

**Q4.** List every composant for which `:arm` is **a** supplier (one supplier among possibly several).

**Q5.** List every composant whose `:prix` is strictly greater than 50, returning URI and price.

---

## Medium

**Q6.** For every composant, return its URI and the label of each of its suppliers. Components with no declared supplier should still appear once with an unbound supplier label.

**Q7.** List every composant that has no `:fournisseur` declared.

**Q8.** List the composants directly contained in `:pcbBoardA` — no transitivity.

**Q9.** List every composant contained, directly or indirectly, in `:pcbBoardA`.

**Q10.** List every composant for which `:arm` is the **sole** supplier — `:arm` supplies it and no other supplier does.

**Q11.** List every composant supplied by **both** `:samsung` **and** `:skHynix`.

---

## Harder

**Q12.** List every produit that uses, directly or indirectly, the composant `:cortexA710`.

**Q13.** List every produit that uses, directly or indirectly, at least one composant for which `:arm` is the sole supplier.

**Q14.** For each produit, return its label and the count of distinct composants it uses directly or indirectly. Sort by count descending.

**Q15.** For each fournisseur, return its label and the number of distinct produits that depend on it directly or indirectly. Skip fournisseurs with zero dependent produits. Sort by count descending.

**Q16.** List the composants that are used, directly or indirectly, by at least two distinct produits. Return URI and the count of distinct dependent produits.

**Q17.** For each produit, return the total `:prix` summed over the distinct composants it uses directly or indirectly. Sort by total descending.

---

## Stretch

**Q18.** List every produit that uses, directly or indirectly, **every** composant supplied (among others) by `:arm`.

**Q19.** List every unordered pair of distinct produits `(?p1, ?p2)` that share at least one composant directly or transitively. Return each pair exactly once — not both `(A,B)` and `(B,A)`.

**Q20.** Find the fournisseur(s) who are the sole supplier of the largest number of composants. Return supplier label and the count. If several suppliers tie for first, return all of them.
