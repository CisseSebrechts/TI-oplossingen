# Databanken 1 Examenoplossingen

Deze oplossingen zijn één van de examens op de examenwiki van Diana. Ik weet niet welke en ik weet ook niet wie deze oplossingen heeft geschreven.

1.

```sql
SELECT row_number() over () as volgnr,
geslacht, plaats, count()
FROM spelers
GROUP BY rollup (geslacht, plaats)
union
SELECT row_number() over () as volgnr, null, plaats, count()
FROM spelers
GROUP BY rollup (plaats)
ORDER BY geslacht, plaats
```



2. Alles wat false met de where-conditie wordt niet getoont

```sql
SELECT spelersnr, sum(bedrag), sum(bedrag)
FILTER (WHERE bedrag>50)
FROM boetes
GROUP BY spelersnr;
```



3. met behulp van een foreign key add constraint FK2 foreign key (spelersnr) references
 spelers (spelersnr)

4. 

  * relationeel: gebruik van tabellen,rijen, kolommen

  * hierarchisch: gebruik van segmenten,records,fields

5.
  opl query: 

| 1    | 1    | 4    |
| ---- | ---- | ---- |
| 2    | 2    | 4    |

6. 

  * Get next 
    * rekening met pointer houder, begint op huidige plaats in de boom, stopt wnr next is gevonden(= volgende segment)
  * Get next within Parent
    * beginnen vanaf pointer maar alleen in afhankelijke segmenten van parent
  * PCB = program communication block
    * tegenhanger = ODMS
    * Dit programma geeft de verzorgsters die op hun zaal minstens één patiëntje hebben dat
      valium neemt.

7. 

  **Atomicity**: boolean
  **Consistency**: state
  **Isolation**: concurrency
  **Durability**: levensduur
  **Stelling**: omgekeerd -> RDBMS voordeliger dan NoSQL

8. 

  * **transactie** 
    * verzameling SQL-instructies die door één gebruiker ingevoerd wordt (mutaties blijvend of ongedaan maken)
  * Commit : permanent maken van een transactie
  * Rollback : ongedaan maken van een transactie

9. **Gevaren**: 

	Dirty read (uncommitted read) :
		een gebruiker leest een gegeven dat nooit gecommit werd
	Nonrepeatable – nonreproducible read :
		Een gebruiker leest voor en na de commit andere gegevens (gegevens worden gewijzigd)
	Phantom read :
			een gebruiker leest voor en na de commit andere gegevens (er komen nieuwe gegevens)
	Lost update :
	 		Een wijziging van één gebruiker wordt overschreven door een andere gebruiker
**Oplossing** :
 	Transacties serieel verwerken !
 Oplossing indien honderden gebruikers tegelijk willen werken
 	Transacties parallel verwerkeni !

**Locking** :
● de rij waar één gebruiker mee werkt wordt gelocked
voor de andere gebruikers
● als transactie afgelopen is, wordt de blokkade
opgeheven 

**Deadlock** :
● indien twee of meerdere gebruikers op elkaar
wachten
● Oplossing :
● indien deadlock aanwezig, dan wordt één transactie
afgebroken

**Isolation level** : mate van isolatie van gebruikers

* Niveaus:
* Serializable : maximaal gescheiden
* Repeatable read :
  * lezen : share blokkades (stopt bij einde transactie)
  * muteren : exclusive blokkades
* Cursor stability (read committed) :
  * lezen : share blokkades (stopt bij einde select)
  * muteren : exclusive blokkades
* Dirty read (read uncommitted) :
  * lezen : share blokkades (stopt bij einde select)
  * muteren : exclusive blokkades (stopt bij einde mutatie)

10. Verschil gecorreleerd en niet gecorreleerde subquery

    ```
    gecorreleerde subquery kan nietautonoom uitgevoerd worden.
    niet-gecorreleerde subquery wel apart uitvoeren
    ```

    

Soorten subquery
* Scalaire subquery:1 rij, 1 waarde
* Rij-subquery:1 rij
* Kolom-subquery:elke rij 1 waarde
* Tabel-subquery:verzameling rijen en kolommen

verschillen hierarchisch en netwerk:

bij netwerk: members zonder owners kunnen bestaan
recordtype kan member zijn in meerdere settypes
meerdere settypes tssen zelfde recordtypes bestaan

view: tabel die zichtbaar is voor de gebruiker maar geen opslagruimte enneemt (bevat geen rijen)
nut: vereenvoudigen van routinematige instructies
reorganiseren van tabellen
stapsgewijs opzetten van SELECT-instructies
beveiligen van gegevens

CREATE VIEW leeftijden(spelersnr, leeftijd) as SELECT blabla FROM