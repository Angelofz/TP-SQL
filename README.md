# TP1 SQL Oracle
## Exercice 1
### 1.1 Première partie

1. L'instruction SELECT suivante est-elle exécutée avec succès : (oui/non) ?

```sql
SELECT last_name, job_id, salary AS Sal
FROM employees;
```
> Oui
>
> ![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/1.png)

2. L'instruction SELECT suivante est-elle exécutée avec succès: (oui/non) ?

```sql
SELECT * 
FROM JOB_HISTORY;
```
> Oui

![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/2.png)

3. L'instruction suivante présente quatre erreurs de codage. Pouvez-vous les
identifier ?

```sql
SELECT employee_id, last_name
sal x 12 ANNUAL SALARY
FROM employees; 
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/3.png)

>Erreur 1: il manque une `,` après `last_name`  
>Erreur 2: `sal` n'existe pas dans la table il faut utiliser `salary`  
>Erreur 3: `*` doit être utilisé à la place de `x`  
>Erreur 4: il manque les `""` dans `ANNUAL SALARY`

### 1.2 Deuxième Partie
1. Le département des ressources humaines souhaite une interrogation affichant le nom, l'ID de poste, la date d'embauche et l'ID d'employé de chaque employé, l'ID d'employé apparaissant en premier. Associez l'alias `STARTDATE` à la colonne `HIRE_DATE`.

```sql
SELECT
    employee_id,
    last_name,
    job_id,
    hire_date as STARTDATE
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/4.png)

2. Le département des ressources humaines souhaite une interrogation affichant tous les ID de postes uniques de la table `EMPLOYEES`.

```sql
SELECT DISTINCT job_id
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/5.png)

3. Nommez les entêtes de colonne respectivement : `Emp #`, `Employee`, `Job et Hire` `Date`.
Exécutez à nouveau votre interrogation. Le département des ressources humaines a demandé un état listant tous les employés avec leur ID de poste. Affichez le nom concaténé avec l'ID de poste (en séparant les deux par une virgule et un espace) et intitulez la colonne `Employee and Title`.

```sql
SELECT
    employee_id as "Emp #",
    last_name as Employee,
    job_id as Job,
    hire_date as "Hire Date",
    last_name || ', ' || job_id as "Employee and Title"
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/6.png)

4. Pour vous familiariser avec le contenu de la table `EMPLOYEES`, créez une Interrogation affichant toutes les données de cette table. Séparez les colonnes de Résultat par une virgule. Attribuez le titre de colonne `THE_OUTPUT`.

```sql
SELECT employee_id || ',' || first_name || ',' || last_name || ',' || email || ',' || phone_number || ',' || hire_date || ',' || job_id || ',' || salary || ',' || commission_pct || ',' || manager_id || ',' || department_id as THE_OUTPUT
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/7.png)

## Exercice 2

1. Pour des raisons budgétaires, ce département a besoin d'un état affichant le nom et le salaire des employés qui gagnent plus de 12 000 $.

```sql
SELECT
    last_name,
    salary
FROM employees
WHERE salary > 12000;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/8.png)

2. Ouvrez une nouvelle feuille de calcul SQL Worksheet. Créez un état affichant le nom et le numéro de département correspondant à l'ID d'employé 176.

```sql
SELECT
    last_name,
    department_id
FROM employees
WHERE employee_id = 176;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/9.png)

3. Le département des ressources humaines a besoin de connaître les employés dont le salaire est élevé et ceux dont le salaire est faible. Modifiez le fichier ex_02_01.sql pour afficher le nom et le salaire des employés dont le salaire ne figure pas dans la plage de 5 000 $ à 12 000 $.

```sql
SELECT
    last_name,
    salary
FROM employees
WHERE salary NOT BETWEEN 5000 AND 12000;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/10.png)

4. Créez un état affichant le nom, l'ID de poste et la date d'embauche des employés nommés Matos et Taylor. Triez les données par ordre croissant en fonction de la date d'embauche
 
```sql
SELECT
    last_name,
    job_id,
    hire_date
FROM employees
/* WHERE last_name = 'Matos' OR last_name = 'Taylor'; */
WHERE last_name IN ('Taylor','Matos')
ORDER BY hire_date;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/11.png)

5. Affichez le nom et le numéro de département de tous les employés du département 20 ou 50 par ordre alphabétique croissant, en fonction du nom

```sql
SELECT
    last_name,
    department_id
FROM employees
WHERE department_id IN (20,50)
ORDER BY last_name;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/12.png)

6. Modifiez le fichier ex_02_03.sql pour afficher le nom et le salaire des employés qui gagnent entre 5 000 $ et 12 000 $, et travaillent dans le département 20 ou 50.
Intitulez respectivement les colonnes `Employee` et `Monthly Salary`.

```sql
SELECT
    last_name as Employee,
    salary as "Monthly Salary"
FROM employees
WHERE salary BETWEEN 5000 AND 12000
AND department_id IN (20,50);
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/13.png)

7. Le département des ressources humaines a besoin d'un état affichant le nom et la date d'embauche de tous les employés embauchés en 1994.

```sql
SELECT
    last_name,
    hire_date
FROM employees
WHERE EXTRACT(year FROM hire_date) = 1994;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/14.png)

8. Créez un état affichant le nom et l'intitulé de poste de tous les employés qui n'ont pas de manager.

```sql
SELECT
    last_name,
    job_id
FROM employees
WHERE manager_id IS NULL; 
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/15.png)

9. Créez un état affichant le nom, le salaire et la commission de tous les employés qui perçoivent des commissions. Triez les données par ordre décroissant en fonction du salaire et des commissions.
Utilisez la position numérique de la colonne dans la clause ORDER BY.

```sql
SELECT 
    last_name,
    salary,
    commission_pct
FROM employees
WHERE commission_pct IS NOT NULL
ORDER BY 2 DESC,3 DESC;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/16.png)

10. Les membres du département des ressources humaines souhaitent davantage de souplesse dans les interrogations que vous écrivez. Ils voudraient un état affichant le nom et le salaire des employés qui gagnent plus qu'un montant saisi par
l'utilisateur en réponse à une invite ( &variable (SQL Dev) ou :variable(APEX)).

```sql
SELECT
    last_name,
    salary
FROM employees
WHERE salary > :salaire;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/17.png)

![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/18.png)

## Exercice 3

1. Ecrivez une interrogation permettant d'afficher la date système. Nommez la colonne `Date`.

```sql
SELECT SYSDATE as "Date"
FROM DUAL;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/19.png)

2./3. Le département des ressources humaines a besoin d'un état permettant d'afficher le numéro d'employé, le nom, le salaire et le salaire augmenté de 15,5 % (exprimé sous la forme d'un nombre entier) pour chaque employé. Nommez la colonne `New Salary`.

```sql
SELECT
    employee_id,
    last_name,
    salary,
    ROUND(salary * 1.155,0) as "New Salary"
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/2O.png)

4. Modifiez l'interrogation ex_03_02.sql pour ajouter une colonne permettant de soustraire l'ancien salaire du nouveau. Nommez la colonne `Increase`.

```sql
SELECT
    employee_id,
    last_name,
    salary,
    "New Salary",
    "New Salary" - salary as Increase
FROM 
(
    SELECT
        employee_id,
        last_name,
        salary,
        ROUND(salary * 1.155,0) as "New Salary"
    FROM employees
);
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/21.png)

5. Ecrivez une interrogation permettant d'afficher le nom (la première lettre en majuscule et toutes les autres lettres en minuscules) et la longueur du nom de tous les employés dont le nom commence par les lettres "J", "A" ou "M". Attribuez à
chaque colonne un libellé approprié. Triez les résultats en fonction du nom des employés.

```sql
SELECT
    INITCAP(last_name) as Name,
    LENGTH(last_name) as Length
FROM employees
WHERE last_name LIKE 'A%'
OR last_name LIKE 'J%'
OR last_name LIKE 'M%'
ORDER BY last_name;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/22.png)

6. Réécrivez l'interrogation de sorte que l'utilisateur soit invité à saisir la lettre par laquelle le nom doit commencer. Par exemple, si l'utilisateur saisit "H" (en majuscule) à l'invite, le résultat doit afficher tous les employés dont le nom commence par la lettre "H".

```sql
SELECT
    INITCAP(last_name) as Name,
    LENGTH(last_name) as Length
FROM employees
WHERE last_name LIKE :start_letter || '%'
ORDER BY last_name;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/23.png)

![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/24.png)

7. Modifiez l'interrogation de sorte que la casse de la lettre saisie n'affecte pas le résultat. La lettre saisie doit être convertie en majuscule avant traitement par l'interrogation `SELECT`.

```sql
SELECT
    INITCAP(last_name) as Name,
    LENGTH(last_name) as Length
FROM employees
WHERE last_name LIKE INITCAP(:start_letter) || '%'
ORDER BY last_name;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/25.png)

![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/26.png)

8. Le département des ressources humaines souhaite connaître l'ancienneté de chaque employé. Pour chacun d'eux, affichez le nom et calculez le nombre de mois entre la date du jour et la date d'embauche de l'employé. Nommez la colonne `MONTHS_WORKED`. Triez les résultats sur la base du nombre de mois d'ancienneté. Arrondissez le nombre de mois au nombre entier supérieur le plus proche.

```sql
SELECT
    last_name,
    CEIL(MONTHS_BETWEEN(SYSDATE,hire_date)) as MONTHS_WORKED
FROM employees
ORDER BY MONTHS_WORKED;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/27.png)

## Exercice 4

1. Créez un état qui produit les éléments suivants pour chaque employé : ***<employee last name> earns <salary> monthly but wants <3 times salary.>***. Intitulez la colonne `Dream Salaries`

```sql
SELECT
last_name || ' earns ' || TO_CHAR(salary, 'fm$99,999.00') || ' monthly but wants ' || TO_CHAR(3*salary, 'fm$99,999.00') as "Dream Salaries"
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/28.png)

2. Pour chaque employé, affichez le nom, la date d'embauche et la date de révision du salaire, soit le premier lundi après six mois d'ancienneté. Intitulez la colonne `REVIEW`. Affichez les dates sous la forme ***"Monday, the Thirty-First of July, 2000"***

```sql
SELECT
    last_name,
    hire_date,
    TO_CHAR(NEXT_DAY(ADD_MONTHS(hire_date, 6),'monday'), 'fmDay, "the" Ddspth "of" Month, YYYY') as REVIEW
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/29.png)

3. Affichez le nom, la date d'embauche et le jour de la semaine où l'employé a commencé. Intitulez la colonne `DAY`. Triez les résultats en fonction du jour de la semaine.

    
```sql
SELECT
    last_name,
    hire_date,
    TO_CHAR(hire_date,'DAY') as DAY
FROM employees
ORDER BY TO_CHAR(hire_date, 'd');
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/30.png)

4. Créez une interrogation qui affiche le nom et le montant de la commission de chaque employé. Si un employé ne perçoit pas de commission, indiquez "No Commission". Intitulez la colonne `COMM`.

```sql
SELECT
    last_name,
    COALESCE(TO_CHAR(commission_pct),'No Comission') as COMM
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/31.png)    
 
5. A l'aide de la fonction DECODE, écrivez une interrogation qui affiche le niveau de tous les employés sur la base de la valeur de la colonne JOB_ID, à l'aide des données suivantes :
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/32.png)
```sql
 SELECT
    job_id,
    DECODE(job_id,
        'AD_PRES','A',
        'ST_MAN','B',
        'IT_PROG','C',
        'SA_REP','D',
        'ST_CLERK','E',
        0) as GRADE
FROM employees;   
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/33.png)

6. Réécrivez l'instruction de l'exercice précédent à l'aide de la syntaxe CASE.    

```sql
SELECT
    job_id,
    CASE job_id
        WHEN 'AD_PRES' THEN 'A'
        WHEN 'ST_MAN' THEN 'B'
        WHEN 'IT_PROG' THEN 'C'
        WHEN 'SA_REP' THEN 'D'
        WHEN 'ST_CLERK' THEN 'E'
        ELSE '0'
    END as GRADE
FROM employees;
```
    
## Exercice 5

1. Les fonctions de groupe opèrent sur plusieurs lignes et produisent un résultat par groupe.
> Vrai   
2. Les fonctions de groupe prennent en compte les valeurs NULL dans les calculs.
> Faux
3. La clause WHERE restreint les lignes avant inclusion dans un calcul de groupe
> Vrai

4. Déterminez le salaire le plus élevé, le salaire le plus bas, le salaire cumulé et le salaire moyen pour tous les employés. Intitulez respectivement les colonnes `Maximum`, `Minimum`, `Sum` et `Average`. Arrondissez les résultats à l'entier le plus proche.

```sql    
SELECT
    MAX(salary) as Maximum,
    MIN(salary) as Minimum,
    SUM(salary) as Sum,
    ROUND(AVG(salary)) as Average
FROM employees;
```    
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/34.png)
    
5. Modifiez l'interrogation enregistrée dans le fichier ex_05_04.sql afin d'afficher le salaire minimum, le salaire maximum, le salaire cumulé et le salaire moyen pour chaque type de poste.

```sql 
SELECT
    job_id,
    MAX(salary) as Maximum,
    MIN(salary) as Minimum,
    SUM(salary) as Sum,
    ROUND(AVG(salary)) as Average
FROM employees
GROUP BY job_id;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/35.png)
    
6. Ecrivez une interrogation permettant d'afficher le nombre de personnes occupant le même poste.
    
```sql  
SELECT
    job_id,
    COUNT(*)
FROM employees
WHERE job_id = :nom_du_poste
GROUP BY job_id;
```    
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/36.png)
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/37.png)

7. Déterminez le nombre de managers sans les répertorier. Intitulez la colonne `Number of Managers`. Indice : Utilisez la colonne `MANAGER_ID` pour déterminer le nombre de Managers
    
```sql
SELECT
COUNT(DISTINCT(manager_id)) as "Number of Managers"
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/38.png)
    
8. Trouvez la différence entre le salaire le plus élevé et le salaire le plus bas. Intitulez la colonne `DIFFERENCE`.
     
```sql
SELECT
MAX(salary) - MIN(salary) as DIFFERENCE
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/39.png)    
   
9. Créez un état permettant d'afficher le numéro de manager et le salaire de l'employé le moins payé sous les ordres de ce manager. Excluez toute personne pour laquelle le manager n'est pas connu. Excluez les groupes dans lesquels le salaire minimum est inférieur ou égal à 6 000 $. Triez les résultats par ordre décroissant sur la base du salaire
    
```sql
SELECT
    manager_id,
    MIN(salary)
FROM employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id
/* HAVING NOT (MIN(Salary) <= 6000); */
HAVING(MIN(Salary) > 6000)
ORDER BY MIN(salary) DESC;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/40.png)
    
10. Créez une interrogation permettant d'afficher le nombre total d'employés et, pour ce total, le nombre d'employés embauchés en 1995, 1996, 1997 et 1998 (2005, 2006, 2007, 2008). Créez les en-têtes de colonne appropriés.

```sql    
SELECT
    COUNT(DISTINCT(employee_id)) as TOTAL,
    SUM(DECODE(EXTRACT(year FROM hire_date),1995,1)) as "1995",
    SUM(DECODE(EXTRACT(year FROM hire_date),1996,1)) as "1996",
    SUM(DECODE(EXTRACT(year FROM hire_date),1997,1)) as "1997",
    SUM(DECODE(EXTRACT(year FROM hire_date),1998,1)) as "1998"
FROM employees;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/41.png)
    
11. Créez une interrogation de matrice permettant d'afficher le poste, le salaire correspondant à ce poste sur la base du numéro de département et le salaire total correspondant à ce poste, pour les départements 20, 50, 80 et 90, en intitulant
chaque colonne de façon appropriée
    
```sql    
SELECT DISTINCT
    job_id as Job,
    DECODE(department_id,20,ROUND(AVG(salary),0)) as "Dept 20",
    DECODE(department_id,50,ROUND(AVG(salary),0)) as "Dept 50",
    DECODE(department_id,80,ROUND(AVG(salary),0)) as "Dept 80",
    DECODE(department_id,90,ROUND(AVG(salary),0)) as "Dept 90",
    SUM(salary) as Total
FROM employees
WHERE department_id is not null
GROUP BY job_id,department_id;
```
![Cover](https://github.com/Angelofz/TP1-SQL-Oracle/blob/main/image/42.png)    
