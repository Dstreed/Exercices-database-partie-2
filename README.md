# Exercices 1 :

Ecrivez une requête SQL qui affiche tous les titres et descriptions des films dont la description contient le mot Amazing.

```sql
dvdrental=> SELECT title, description FROM film WHERE description LIKE '%Amazing%';
```

# Exercices 2 :

Ecrivez une requête SQL qui récupère tous les paiements supérieurs à 10. Il faudra récupérer l'id, le prénom, le nom du client ainsi que le montant et la date du paiement.

```sql
dvdrental=> SELECT payment.customer_id, customer.first_name, customer.last_name, payment.amount, payment.payment_date FROM payment INNER JOIN customer ON payment.customer_id = customer.customer_id WHERE amount > 10;
```

# Exercice 3 :

Ecrivez une requête SQL qui affiche le chiffre d'affaire gagné par le video club depuis son ouverture.

```sql
dvdrental=> SELECT SUM(amount) FROM payment;
   sum
----------
 61312.04
(1 row)

```

# Exercice 4 :

Ecrivez une requête SQL qui affiche le titre de tous les films dont la langue est l'anglais et dont la durée est supérieure à 120 minutes.

```sql
dvdrental=> SELECT title  FROM film WHERE language_id=1 AND length>120;
```

# Exercices 5 :

Ecrivez une requête SQL qui affiche le TOP 10 des clients qui ont fait le plus d'achat dans ce video club. Il faudra récupérer leur id, prénom, nom, email. Il vous faudra utiliser les requêtes auxiliaires avec WITH pour cette exercice.

```sql
WITH customer_total AS (SELECT customer_id, SUM(amount) total_amount FROM payment GROUP BY customer_id ORDER
 BY total_amount DESC LIMIT 10) SELECT customer_id, first_name, last_name, email FROM customer WHERE customer_id IN (SEL
ECT customer_id FROM customer_total);
```

# Exercice 6 :

Récupérer les mêmes informations que l'exercice précédent, mais ajouter avec un JOIN le montant total des achats pour chacun du TOP 10 des clients.

```sql
WITH customer_total AS (SELECT customer_id, SUM(amount) as total_amount FROM payment GROUP BY customer_id), top_customers AS (SELECT customer_id, total_amount FROM customer_total ORDER BY total_amount DESC LIMIT 10) SELECT customer.customer_id, customer.first_name, customer.last_name, customer.email, top_customers.total_amount FROM customer INNER JOIN top_customers ON customer.customer_id=top_customers.customer_id ORDER BY top_customers.total_amount DESC;

```
