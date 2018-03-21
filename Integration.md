# TP Integration


## Pig
```pig
salaries_0 = LOAD '/user/cloudera/Yolo/Salaries.csv' 
USING PigStorage(';') 
AS (numero:int, nom:chararray, prenom:chararray,civilite:int, CP:int, date_naissance:chararray);

salaries = FOREACH salaries_0 GENERATE numero, nom, civilite, ToDate (date_naissance,'dd/MM/yyyy') as dateNaissance;
salariesFormate = FOREACH salaries GENERATE numero, nom, civilite, ToString (dateNaissance,'dd/MM/yyyy') as dn, YearsBetween(CurrentTime(), dateNaissance) as Age;
STORE salariesFormate INTO '/user/cloudera/Yolo/resultats3Pig'
USING PigStorage (';');
```
