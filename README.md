# Wichtige Infos
Bei den Commands, wenn ein Teil in [] steht, z.B. [schema], dann bedeutet das, dass dort dein eigener Wert stehen muss, also nicht einfach copy pasten

# DIREKTER LOGIN AUF POSTGRES
psql -d postgres -U postgres -h [IP]

# KOPIEREN EINER CSV DATEI
Zum verwenden dieser Methode, wird der direkte Login aufs Postgres erfordert

CSV Datei in die Tabelle eintragen. DELIMITER bestimmt die trennung, CSV HEADER zeigt ob ein Header vorhanden ist

Path ist der Pfad zu der Datei

```\copy [person(name, id_ort)] FROM '[PATH/PATH]' DELIMITER ';' ENCODING 'UTF-8' CSV HEADER;```

# Importieren einer SQL Datei
Zum verwenden dieser Methode, wird der direkte Login aufs Postgres erfordert

\i [PFAD/PFAD]

# Einen einzelnen Befehl in bash ausführe

```\! [Befehl]	Der Befehl wir in Bash Ausgeführ auch wenn man in postgres drin ist.```
---------------------------------------------------------------------------------------------

# Schlüsselwörter/attribute

## DML

UPDATE = Die Dateneinträge einer Tabelle verändern

ALTER = Eine Tabelle verändern

DROP = Ein Schema löschen

SET = Mich in ein bestimmtes schema versetzen

SHOW = Ausgabe von Information

CREATE = Tabelle erstellen oder user/rollen erstellen

INSERT = Dateneinträge in eine Tabelle hinzufügen

## Queries

SELECT = Das auswählen aus einer Tabelle und dessen Einträge

LIMIT = Ein Limit wie viele Einträge gezeigt werden sollen

OFFSET = Eine Verschiebung ab wann Einträge gezeigt werden sollen

DISTINCT = Das entfernen von duplikaten

WHERE = Die Abfrage an welcher Stelle

WHERE ... LIKE = Die Abrage eines Wertes bei dem etwas sein könnte

ILIKE = Selbe prinzip wie LIKE nur achtet es nicht auf gross oder kleinschreibung

AS = Ein Alias/Namensersatz (Für Beispiele nach Alias suchen)

UNION ALL = Kombiniert Ergebnisse aus mehreren SELECT-Abfragen mit Duplikaten. SELECT first_name FROM employees UNION ALL SELECT last_name FROM employees;
 
UNION = Kombiniert Ergebnisse aus mehreren SELECT-Abfragen ohne Duplikate. SELECT first_name FROM employees UNION SELECT last_name FROM employees;
 
COALESCE = Gibt den ersten Nicht-NULL-Wert in einer Liste zurück. SELECT COALESCE(commission_pct, 0) AS final_commission FROM employees; Um eine solche Liste zu erstellen, kannst du die COALESCE-Funktion verwenden, die den ersten Nicht-NULL-Wert aus einer Reihe von Werten zurückgibt. Für dein Szenario würdest du folgendes SQL-Statement schreiben: Abfrage SELECT person_id, COALESCE(phone_number, email, 'Nicht vorhanden') AS contact_info FROM people;
 
EXTRACT = Extrahiert Teile eines Datums (z. B. Jahr, Monat, Tag). SELECT EXTRACT(YEAR FROM hire_date) AS hire_year FROM employees;
 
TO_CHAR/RANDOM??? = Formatiert Werte (Zahlen oder Datumswerte) als Text. Sonst random was auswählen. SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD') AS formatted_date FROM dual; (SELECT RANDOM() AS random_value;)
 
ROUND = Rundet eine Zahl auf die angegebene Dezimalstelle. SELECT ROUND(123.456, 2) AS rounded; -- Ergebnis: 123.46
 
CASE =Du kannst für diese Aufgabe auch die CASE-Anweisung verwenden, um eine bedingte Logik zu implementieren. Dies ist eine flexible Alternative zu COALESCE, bei der du explizit angeben kannst, welche Bedingungen geprüft werden sollen. Abfrage mit CASE SELECT person_id, CASE WHEN phone_number IS NOT NULL THEN phone_number WHEN email IS NOT NULL THEN email ELSE 'Nicht vorhanden' END AS contact_info FROM people;
 
FORMAT = Formatiert Zahlen oder Text. SELECT FORMAT('%.2f', 1234.567) AS formatted_number; -- Ergebnis: '1234.57'
 
RPAD/LPAD = fügt Zeichen links (LPAD) oder rechts (RPAD) hinzu, um eine feste Länge zu erreichen. SELECT LPAD('123', 5, '0') AS left_padded; -- Ergebnis: '00123' SELECT RPAD('ABC', 5, '-') AS right_padded; -- Ergebnis: 'ABC--'
 
TRIM = Entfernt Leerzeichen oder bestimmte Zeichen. SELECT TRIM(' SQL ') AS trimmed; -- Ergebnis: 'SQL'
 
REPLACE = Ersetzt einen Teilstring durch einen anderen. SELECT REPLACE('PostgreSQL', 'Post', 'My') AS replaced; -- Ergebnis: 'MygreSQL'
 
TO_DATE = Konvertiert Text in ein Datumsformat. SELECT TO_DATE('2025-01-20', 'YYYY-MM-DD') AS date_formatted;
 
AGE = Berechnet die Differenz zwischen zwei Datumswerten. SELECT AGE(NOW(), hire_date) AS time_employed FROM employees;
 
INNER JOIN = Verbindet Tabellen und gibt Datensätze mit Übereinstimmungen zurück. SELECT e.first_name, d.department_name FROM [employees e INNER JOIN departments d] ON e.department_id = d.department_id;
 
LEFT JOIN = Gibt alle Datensätze aus der linken Tabelle zurück, auch ohne Übereinstimmungen. SELECT e.first_name, d.department_name [FROM employees e LEFT JOIN] departments d ON e.department_id = d.department_id;
 
RIGHT JOIN = Gibt alle Datensätze aus der rechten Tabelle zurück, auch ohne Übereinstimmungen. SELECT e.first_name, d.department_name FROM employees e [RIGHT JOIN departments d] ON e.department_id = d.department_id;
 
COUNT() = Zählt Datensätze oder Nicht-NULL-Werte. SELECT COUNT(*) AS total_employees FROM employees;
 
MAX() = Gibt den höchsten Wert einer Spalte zurück. SELECT MAX(salary) AS highest_salary FROM employees;
 
MIN() = Gibt den niedrigsten Wert einer Spalte zurück. SELECT MIN(salary) AS lowest_salary FROM employees;
 
SUM() = Summiert alle Werte in einer Spalte. SELECT SUM(salary) AS total_salary FROM employees;
 
AVG() = Berechnet den Durchschnitt der Werte in einer Spalte. SELECT AVG(salary) AS average_salary FROM employees;
 
HAVING = Filtert Gruppenergebnisse nach Aggregatfunktionen
 
Ohne GROUP BY: Sie können HAVING auch ohne Gruppierung verwenden, um Bedingungen auf Aggregatfunktionen der gesamten Tabelle anzuwenden: SELECT SUM(salary) AS TotalSalary FROM employees HAVING SUM(salary) > 100000;
 
Mit GROUP BY: SELECT department_id, SUM(salary) AS TotalSalary FROM employees GROUP BY department_id HAVING SUM(salary) > 50000;
 
SELECT department_id, COUNT() AS employee_count FROM employees GROUP BY department_id HAVING COUNT() > 10;

## Berechtigungen
GRANT = Berechtigung erteilen

REVOKE = Berechtigung nehmen

CREATE = Rolle erstellen (Am besten für die Berechtigungen)

# Allgemein Wissen
CSV = Comma seperated value

DBMS = Database Management System

MySQL (Relationsmodell basiert)

ERM, ERD, ED

DDL = Data Definition Language

SQL = Structured Query Language

DML = Data Manipulation Language

DQL = Data Query Language

---------------------------------------------------------------------------------------------

# Datenbank login

```sudo -u postgres psql```

---------------------------------------------------------------------------------------------

# Schema 1.0

Ein Schema erstellen

```create schema [mySchema];```

---------------------------------------------------------------------------------------------

Gibt die Liste der Schemen aus

```\dn```

---------------------------------------------------------------------------------------------

Löscht ein Schema mit den zugehörigen Tabellen

```drop schema [myschema] CASCADE;```

---------------------------------------------------------------------------------------------

Bewegung innerhalb eines bestimmten Schemas

```set search_path to [myschema];```

---------------------------------------------------------------------------------------------

Zeigt das aktuelle schema in dem ich mich befinde

```SHOW search_path;```

---------------------------------------------------------------------------------------------

Erstellt eine Tabelle innerhalb eines Schemas

```create table person ([firstname] varchar(10), [lastname] varchar(20));```

---------------------------------------------------------------------------------------------

# Tabellen 1.0

Werden die tabellen angezeigt

```\dt;```

---------------------------------------------------------------------------------------------

Die Struktur einer Tabelle anzeigen

```\d person```

---------------------------------------------------------------------------------------------

Eine Tabelle löschen mit all ihren Inhalten

```\drop table person CASCADE```

---------------------------------------------------------------------------------------------

Einträge in einer Tabelle generieren

```insert into person ([firstname], [lastname]) values ('[Mert]', '[Bal]');```

---------------------------------------------------------------------------------------------

Alle Einträge einer Tabelle ausgeben

```select * from person;```

---------------------------------------------------------------------------------------------

# Tabellen 2.0

Inhalt einer Tabelle verändern (z.B. rename oder datentyp ändern)

```ALTER TABLE ort RENAME ortsname TO name;```

---------------------------------------------------------------------------------------------

Das verändern eines Datentypes eines Attributs

```ALTER TABLE [Tabellenname]```
```ALTER COLUMN [ATTRIBUTSNAME] TYPE VARCHAR(10);```

---------------------------------------------------------------------------------------------

Values abändern

```UPDATE ort SET plz=8307 WHERE name='Effretikon';```

---------------------------------------------------------------------------------------------

Das löschen eines Eintrags in der Datenbank

```DELETE FROM [Tabellenname]```
```WHERE [Attributsname] = 'XYZ';```

---------------------------------------------------------------------------------------------

Primary key hinzufügen

```ALTER TABLE ort ADD PRIMARY KEY(plz);```

---------------------------------------------------------------------------------------------

# Tabellen Abfragen 3.0

Tabelle erstellen mit einem primary key und ohne angesetztem search path und mit

```CREATE TABLE ["NoserYoung".job] ([job_id] integer PRIMARY KEY GENERATED BY DEFAULT AS IDENTITY, [name] varchar(50));```

```CREATE TABLE [staff] ([staff_id] integer PRIMARY KEY GENERATED BY DEFAULT AS IDENTITY);```

---------------------------------------------------------------------------------------------

Ausgabe der Tabellen Struktur

```\d [job]```

---------------------------------------------------------------------------------------------

Einer Tabelle den Primary Key als Fremdschlüssel hinzufügen von einer anderen Tabelle

```ALTER TABLE [staff] ADD COLUMN [id_job] integer REFERENCES [job(job_id)]```

---------------------------------------------------------------------------------------------

# Abfragen 1.0

Searchpath setzen, eine Tabelle aussuchen und dann:

---------------------------------------------------------------------------------------------

Alle Einträge ausgeben

```SELECT * FROM [job];```

---------------------------------------------------------------------------------------------

Sortieren nach einem Attribut und je nach Sortierrichtung (Zahl sortiert nach Attributindex statt min_salary)

Datensätze werden zu maximal 5 limitiert (Zahl kann variabel sein), kann ebenfalls nach dem DESC hinzugefügt werden

OFFSET fängt die Datensätze verschoben an und überspringt je nach anzahl

```SELECT * FROM [job] ORDER BY [min_salary] DESC;```

```LIMIT 5;```

```OFFSET 5;```

---------------------------------------------------------------------------------------------

Es wird ein Alias name für ein Attribut gegeben

```SELECT [last_name] AS [Nachname] FROM [employee];```

---------------------------------------------------------------------------------------------

Es werden doppelte Einträge entfernt

```SELECT DISTINCT [last_name] FROM [employee] ORDER BY 1;```

---------------------------------------------------------------------------------------------

Filtern wonach man suchen möchte (z.B. nur user mit nhm gewissen salär anzeigen)

```SELECT * FROM [employee] WHERE [salary] > 2000;```

---------------------------------------------------------------------------------------------

Zeigt user nur mit einem bestimmten last name an

```SELECT * FROM [employee] WHERE [last_name] = '[King]';```

---------------------------------------------------------------------------------------------

AND wird verwendet um mehrere statements zu kombinieren

OR um entweder oder zu zeigen

```WHERE [last_name] = '[King]' AND [salary] > 2000;```

---------------------------------------------------------------------------------------------

Zeigt nur Einträge mit employees welche mit dem Nachnamen B anfängt

```SELECT * FROM [employee] WHERE [last_name] LIKE '[B%]';```

---------------------------------------------------------------------------------------------

Zeigt nur Einträge mit employees welche mit dem Nachnamen B anfängt und maximal ein Zeichen nach dem B haben oder sucht nach einem Zeichen zwischen dem Eintrag

```SELECT * FROM [employee] WHERE [last_name] LIKE '[B_ll]';```

Es spielt keine rolle ob groß oder kleingeschrieben

ILIKE ist case insentitive

---------------------------------------------------------------------------------------------

Ordner erstellen wo das backup rein soll

```mkdir db-backuptest```

---------------------------------------------------------------------------------------------

Backup erstellen an einen designierten ort

```sudo -u postgres pg_dump --schema [SCHEMANAME] > ./db-backuptest/[dump_NAME_]`date +%Y%m%d`.sql```

---------------------------------------------------------------------------------------------

Ein backup restoren

```sudo -u postgres psql < ./db-backuptest/[dump_NAME_]`date +%Y%m%d`.sql ```

---------------------------------------------------------------------------------------------

Attribute verketten (Weitere hinzufügen in der selben Art für mehrere Argumente)

```SELECT [last_name] || ', ' || [id_job] AS ["Employee and Title"] FROM [employee];```

---------------------------------------------------------------------------------------------

Den user, welcher derzeit ein Schema verwendet anzeigen

```SELECT CURRENT_USER;```

```SELECT SESSION_USER;```

---------------------------------------------------------------------------------------------

Die aktuelle Zeit anzeigen

```SELECT now();```

---------------------------------------------------------------------------------------------

# Berechtigungen 1.0

Berechtigung gegeben, dass ein User ein Schema einsehen kann

```GRANT USAGE ON SCHEMA [hr] TO [joe];```

---------------------------------------------------------------------------------------------

Berechtigung eines Users eines Schemas entfernen

```REVOKE USAGE ON SCHEMA [hr] FROM [joe];```

---------------------------------------------------------------------------------------------

Einem User die Berechtigung geben, alle Tabellen innerhalb eines Schemas einzusehen

```GRANT SELECT ON ALL TABLES IN SCHEMA [public] TO [user];```

---------------------------------------------------------------------------------------------

CRUD Erlaubnis für eine Tabelle einem User geben

```GRANT SELECT, INSERT, UPDATE, DELETE on TABLE [hr.country] TO [joe];```

---------------------------------------------------------------------------------------------

Berechtigung eines Users einer Tabelle entfernen

```REMOKE SELECT, INSERT, UPDATE, DELETE on TABLE [hr.country] FROM [joe];```

---------------------------------------------------------------------------------------------

Eine Rolle erstellen mit Berechtigungen

```create role [listjob];```

---------------------------------------------------------------------------------------------

Eine Rolle einem User übergeben

```GRANT [listjob] to [joe];```

---------------------------------------------------------------------------------------------

Einer Rolle bestimmte Berechtigungen übergeben

```GRANT SELECT on table [hr.job] to [listjob];```

---------------------------------------------------------------------------------------------

Einem User die Rolle entziehen

```REVOKE [listjob] from [joe];```

---------------------------------------------------------------------------------------------

# Abfragen 2.0 SINGLE ROW FUNCTION

Union all verbindet zwei unterschiedliche Select und gibt sie sortiert aus

```SELECT * FROM```

```(```

```(SELECT employee_id, first_name, last_name FROM employee WHERE first_name LIKE 'E%' LIMIT 3)```

```UNION ALL ```

```(SELECT employee_id, first_name, last_name FROM employee WHERE last_name LIKE 'E%' LIMIT 2)```

```ORDER BY first_name) AS m```

```WHERE m.first_name LIKE '%i%';```

---------------------------------------------------------------------------------------------

Mitarbeiter ausgeben welche ein älteres Einstellungsdatum haben, daher <

```SELECT last_name, first_name FROM employee WHERE hire_date < '1990-12-31' AND gender = 'F'```

```ORDER BY last_name, first_name LIMIT 50;```

---------------------------------------------------------------------------------------------

Extrahiert den Monat aus einem einem ganzen Jahres Datum oder filtert nach Mitarbeitern welche im Monat Januar angeheuert worden sind

```SELECT EXTRACT(MONTH FROM hire_date) AS hire_month FROM employee;```

```SELECT * FROM employee WHERE EXTRACT(MONTH FROM hire_date) = 1;```

---------------------------------------------------------------------------------------------

# Abfragen 3.0 JOINS

```SELECT * FROM country```

```INNER`JOIN region ON id_region = region_id;```

---------------------------------------------------------------------------------------------

```SELECT * FROM country c```

```INNER JOIN region r ON c.id_region = r.region_id;```

---------------------------------------------------------------------------------------------

Mit dem INNER JOIN wird noch das department hinzugefügt, um den Namen korrekt anzuzeigen

1 wählt die spalte aus nach welcher es sortieren soll

```SELECT MAX(salary), MIN(salary), department_name FROM employee e```

```INNER JOIN department d ON e.id_department = d.department_id```

```GROUP BY department_name ORDER BY 1 DESC;```

---------------------------------------------------------------------------------------------

```SELECT COUNT(*) AS "Employees per Department", department_name```

```FROM employee```

```INNER JOIN department ON id_department = department_id```

```GROUP BY department_name```

```ORDER BY "Employees per Department";```

---------------------------------------------------------------------------------------------

```SELECT DISTINCT m.salary as salary, m.employee_id, m.last_name```

```FROM employee e```

```JOIN employee m ON e.id_manager = m.employee_id```

```WHERE m.salary > 8000```

```ORDER BY salary DESC;```

---------------------------------------------------------------------------------------------

# Abfragen 4.0 Aggregatsfunktionen

Die Mengenausgabe von Zeilen

```SELECT COUNT (*) AS "Number of Departments" FROM department;```

---------------------------------------------------------------------------------------------

Gibt den höchsten Wert einer Spalte aus 

```SELECT MAX(employee_id) FROM employee;```

---------------------------------------------------------------------------------------------

Gibt einen Namen aus mit dem letzten Buchstaben (z.B. Z)

```SELECT MAX(last_name) FROM employee;```

---------------------------------------------------------------------------------------------

Gibt einen Namen aus der mit dem frühsten Buchstaben anfängt (z.B. a wenns einen gibt)

```SELECT MIN(last_name) FROM employee;```

---------------------------------------------------------------------------------------------

Gibt den Durchschnitt eines Wertes aus

```SELECT AVG(salary) FROM employee;```

---------------------------------------------------------------------------------------------

Gibt die Summe aller Werte aus

```SELECT SUM(salary) FROM employee:```

---------------------------------------------------------------------------------------------

Gibt den max wert aus, aber nur von denen Zeilen, welche id_department 60 haben

```SELECT MAX(salary) from employee WHERE id_department = 60;```

---------------------------------------------------------------------------------------------

Gibt die Gesamtmenge von einem Attribut aus, welche nach einem gewissen Attribut sortiert werden (Müssen die selben sein im Kontext)

```SELECT COUNT(city), id_country FROM location GROUP BY id_country;```

---------------------------------------------------------------------------------------------

Gibt die Summe der Gehälter in einem department aus oder gibt das max/min aus eines departments

```SELECT id_department, SUM(salary) FROM employee GROUP BY id_department;```

```SELECT id_department, MAX(salary), MIN(salary) FROM employee GROUP BY id_department```

---------------------------------------------------------------------------------------------

HAVING funktioniert wie ein zweites WHERE

```SELECT MAX(salary), id_department FROM employee```

```GROUP BY id_department```

```HAVING max(salary) > 12000;```

---------------------------------------------------------------------------------------------

# Abfragen 5.0 Sub Query/Sub Select

---------------------------------------------------------------------------------------------

# Good To Know

Mit in kann ich das or skippen und abkürzen

```SELECT last_name, id_department FROM employee WHERE id_department in (20, 50) ORDER BY last_name;```

---------------------------------------------------------------------------------------------

!= erfüllt die selbe Logik wie WHERE NOT

```SELECT * FROM location WHERE city != 'Geneva';```

---------------------------------------------------------------------------------------------

Das getrennte Anzeigen von Daten, aber zur Darstellung als ein ganzes funktioniert wie folgt:

```SELECT 'The salary of ' || last_name || ' after a 10% raise is $' || ROUND(salary * 1.1) AS "New Salary" FROM employee WHERE commission_pct IS NULL;```

---------------------------------------------------------------------------------------------

Referential actions

```alter table <tabellenname> add constraint <Name_FK> foreign key (Attribut(Welches FK annimmt)) References <andere_tabelle_VomPK>(Attribut_Mit-PK) on delete <cascade> on update <cascade>```


`alter table <tabellenname> add constraint <Name_FK> foreign key (<spalten_name>) References <andere_tabelle>(<spalte>) on delete <cascade> on update <cascade>` = 
	FK mit Referential Actions
 
 
	(Cascade: automatisch Angepasst
 
	set NULL: setzt den Wert des FK auf NULL
 
	set default: setzt auf einen festgelegten Standardwert

	restrict: es wird verweigert, solang keine abhängige Einträge existieren
 
	no action: keine Änderung in der Referenztabelle ist erlaubt)
