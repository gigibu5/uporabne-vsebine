# Procedure
Sintaksa:
```sql
SET TERM !!;

CREATE PROCEDURE ime_procedure([argument1 tip1 [, argument2 tip2, ...]])
[RETURNS (sprem1 tip1)]
AS
[DECLARE VARIABLE ime_sprem tip_sprem;]
BEGIN
	/* Ukazi */
END!!

SET TERM ;!!
```

## Tipi procedur
- **Izvršne** - lahko vrnejo samo enkrat (ob klicu `SUSPEND` se program ustavi) Klic:
```sql
EXECUTE ime_proc();
```
- **Izbirne** - lahko vrnejo večkrat (tako imenovan izpis (izpiše ob klicu `SUSPEND`)) Klic:
```sql
SELECT * FROM ime_proc();
```

# Sprožilci
Sintaksa:
```sql
SET TERM !!;

CREATE TRIGGER ime_sprozilca
FOR ime_tabele
(BEFORE | AFTER) (INSERT [OR UPDATE [OR DELETE]])
AS
BEGIN
	/* UKAZI */
END!!

SET TERM ;!!
```

## NEW in OLD
Globalni spremenljivki, ki vsebujeta vrednosti novih oz. starih atributov pri sprožilcih.

| Spremenljivka | **INSERT** | **UPDATE** | **DELETE** |
|-|-|-|-|
| **NEW** | X | X | |
| **OLD** | | X | X |


Če je v sprožilcu klican EXCEPTION (razen, če ga obravnavamo), se akcija (insert, update, delete) ne bo izvedla.

# PSQL - splošno
**If stavek:**
```sql
IF (/* POGOJ */) THEN
BEGIN
	/* UKAZI */
END
ELSE BEGIN
	/* UKAZI */
END
```

**For zanka:**
```sql
FOR (/* SELECT STAVEK */) INTO /* Naštete spremenljivke, ki smo jih izbrali */ DO
BEGIN
	/* UKAZI */
END
```

Primer:
```sql
FOR SELECT ime, priimek FROM avtorji INTO :ime, :priimek DO 
BEGIN
	:izpis = :ime || ' ' || :priimek;
	SUSPEND;
END
```

# Izjeme
Ustvarjanje izjem:
```sql
CREATE EXCEPTION ime_izjeme 'Besedilo izjeme';
```

Klicanje izjem:
```sql
EXCEPTION ime_izjeme;
```

## Obravnavanje izjem
SQL kode:
```sql
WHEN SQLCODE -530 DO 
BEGIN
	/* UKAZI */
END
```

**Kode, k jih rabmo znaz:**
- -530 - tuji ključ ne obstaja
- -803 - podvojen primarni ključ

Definirane izjeme:
```sql
WHEN ime_izjeme DO 
BEGIN
	/* UKAZI */
END
```

Katerakoli izjema:
```sql
WHEN ANY DO 
BEGIN
	/* UKAZI */
END
```

# Generatorji
Uporabljajo se za generiranje ID-jev (kakor AUTO_INCREMENT v MySQL-u)

Ustvarjanje generatorja:
```sql
CREATE GENERATOR ime_generatorja;
```

Nastavljanje vrednosti generatorja (default 1):
```sql
SET GENERATOR ime_generatorja TO vrednost;
```

Uporaba generatorja:
```sql
:sprem = GEN_ID(ime_generatorja, inkrement);
```
V inkrementu je vrednost, za katero se poveča generator.

# Backup (arhiviranje)
**VSI UKAZI SE IZVAJAJO V CMD-ju IN NE V SQL UKAZNI VRSTICI!!**

Arhiv PB:
```
gbak -b -v -user sysdba -password masterkey C:\baza.fdb C:\arhiv.fdb
```
Zastavice:
- -b - backup
- -v - verbose (sprotno obveščanje)

Restavriranje:
```
gbak -c -v -user sysdba -password masterkey C:\arhiv.fdb C:\nova-baza.fdb
```