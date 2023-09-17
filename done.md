# SQL Házi

Ez kell hogy valamelyik query ne faileljen

``` sql
SET sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```

## Megoldások

1. Mi MADAGASZKÁR fővárosa?

```sql
SELECT fovaros FROM orszagok WHERE orszag = 'MADAGASZKÁR';
```

2. Melyik ország fővárosa OUAGADOUGOU?

```sql
SELECT orszag FROM orszagok WHERE fovaros = 'OUAGADOUGOU';
```

3. Melyik ország autójele a TT?

```sql
SELECT orszag FROM orszagok WHERE autojel = 'TT';
```

4. Melyik ország pénzének jele az SGD?

```sql
SELECT orszag FROM orszagok WHERE penzjel = 'SGD';
```

5. Melyik ország nemzetközi telefon-hívószáma a 61?

```sql
SELECT orszag FROM orszagok WHERE telefon = 61;
```

6. Mekkora területű Monaco?

```sql
SELECT terulet FROM orszagok WHERE orszag = 'MONACO';
```

7. Hányan laknak Máltán?

```sql
SELECT nepesseg*1000 FROM orszagok WHERE orszag = 'MÁLTA';
```

8. Mennyi Japán népsűrűsége?

```sql
SELECT nepesseg*1000 / terulet AS nepesseg_suruseg FROM orszagok WHERE orszag = 'JAPÁN';
```

9. Hány lakosa van a Földnek?

```sql
SELECT SUM(nepesseg*1000) FROM orszagok;
```

10. Mennyi az országok területe összesen?

```sql
SELECT SUM(terulet) FROM orszagok;
```

11. Mennyi az országok átlagos népessége?

```sql
SELECT AVG(nepesseg*1000) FROM orszagok;
```

12. Mennyi az országok átlagos területe?

```sql
SELECT AVG(terulet) FROM orszagok;
```

13. Mennyi a Föld népsűrűsége?

```sql
SELECT SUM(nepesseg*1000) / SUM(terulet) AS fold_nepesseg_suruseg FROM orszagok;
```

14. Hány 1.000.000 km2-nél nagyobb területű ország van?

```sql
SELECT COUNT(*) FROM orszagok WHERE terulet > 1000000;
```

15. Hány 100 km2-nél kisebb területű ország van?

```sql
SELECT COUNT(*) FROM orszagok WHERE terulet < 100;
```

16. Hány 20.000 főnél kevesebb lakosú ország van?

```sql
SELECT COUNT(*) FROM orszagok WHERE nepesseg*1000 < 20000;
```

17. Hány országra igaz, hogy területe kisebb 100 km2-nél, vagy pedig a lakossága kevesebb 20.000 főnél?

```sql
SELECT COUNT(*) FROM orszagok WHERE terulet < 100 OR nepesseg*1000 < 20000;
```

18. Hány ország területe 50.000 és 150.000 km2 közötti?

```sql
SELECT COUNT(*) FROM orszagok WHERE terulet BETWEEN 50000 AND 150000;
```

19. Hány ország lakossága 8 és 12 millió közötti?

```sql
SELECT COUNT(*) FROM orszagok WHERE nepesseg*1000 BETWEEN 8000000 AND 12000000;
```

20. Mely fővárosok népesebbek 20 millió főnél?

```sql
SELECT orszag, fovaros, nep_fovaros FROM orszagok WHERE nep_fovaros > 20000;
```

21. Mely országok népsűrűsége nagyobb 500 fő/km2-nél?

```sql
SELECT orszag, nepesseg*1000 / terulet AS nepesseg_suruseg FROM orszagok WHERE nepesseg*1000 / terulet > 500;
```

22. Hány ország államformája köztársaság?

```sql
SELECT COUNT(*) FROM orszagok WHERE allamforma = 'köztársaság';
```

23. Mely országok pénzneme a kelet-karib dollár?

```sql
SELECT orszag FROM orszagok WHERE penznem = 'kelet-karib dollár';
```

24. Hány ország nevében van benne az "ORSZÁG" szó?

```sql
SELECT COUNT(*) FROM orszagok WHERE orszag LIKE '%ORSZÁG%';
```

25. Mely országokban korona a hivatalos fizetőeszköz?

```sql
SELECT orszag FROM orszagok WHERE penznem LIKE '%korona%';
```

26. Mennyi Európa területe?

```sql
SELECT SUM(terulet) FROM orszagok WHERE foldr_hely LIKE '%Európa%';
```

27. Mennyi Európa lakossága?

```sql
SELECT SUM(nepesseg*1000) FROM orszagok WHERE foldr_hely LIKE '%Európa%';
```

28. Mennyi Európa népsűrűsége?

```sql
SELECT SUM(nepesseg*1000) / SUM(terulet) AS europa_nepesseg_suruseg FROM orszagok WHERE foldr_hely LIKE '%Európa%';
```

29. Hány ország van Afrikában?

```sql
SELECT COUNT(*) FROM orszagok WHERE foldr_hely LIKE '%Afrika%';
```

30. Mennyi Afrika lakossága?

```sql
SELECT SUM(nepesseg*1000) FROM orszagok WHERE foldr_hely LIKE '%Afrika%';
```

31. Mennyi Afrika népsűrűsége?

```sql
SELECT SUM(nepesseg*1000) / SUM(terulet) AS afrika_nepesseg_suruseg FROM orszagok WHERE foldr_hely LIKE '%Afrika%';
```

32. Melyek a szigetországok?

```sql
SELECT orszag FROM orszagok WHERE foldr_hely LIKE '%sziget%';
```

33. Mely országok államformája hercegség, vagy királyság?

```sql
SELECT orszag FROM orszagok WHERE allamforma LIKE '%herceg%' OR allamforma LIKE '%király%';
```

34. Hány országnak nincs autójelzése?

```sql
SELECT COUNT(*) FROM orszagok WHERE autojel IS NULL;
```

35. Mennyi a váltószáma az aprópénznek azokban az országokban, ahol nem 100?

```sql
SELECT COUNT(*) FROM orszagok WHERE valtopenz NOT LIKE '%100%';
```

36. Hány ország területe kisebb Magyarországénál?

```sql
SELECT COUNT(*) FROM orszagok WHERE terulet < (SELECT terulet FROM orszagok WHERE orszag = 'MAGYARORSZÁG');
```

37. Melyik a legnagyobb területű ország, és mennyi a területe?

```sql
SELECT orszag, terulet FROM orszagok ORDER BY terulet DESC LIMIT 1;
```

38. Melyik a legkisebb területű ország, és mennyi a területe?

```sql
SELECT orszag, terulet FROM orszagok ORDER BY terulet LIMIT 1;
```

39. Melyik a legnépesebb ország, és hány lakosa van?

```sql
SELECT orszag, nepesseg*1000 FROM orszagok ORDER BY nepesseg*1000 DESC LIMIT 1;
```

40. Melyik a legkisebb népességű ország, és hány lakosa van?

```sql
SELECT orszag, nepesseg*1000 FROM orszagok ORDER BY nepesseg*1000 LIMIT 1;
```

41. Melyik a legsűrűbben lakott ország, és mennyi a népsűrűsége?

```sql
SELECT orszag, nepesseg*1000 / terulet AS nepesseg_suruseg FROM orszagok ORDER BY nepesseg*1000_suruseg DESC LIMIT 1;
```

42. Melyik a legritkábban lakott ország, és mennyi a népsűrűsége?

```sql
SELECT orszag, nepesseg*1000 / terulet AS nepesseg_suruseg FROM orszagok ORDER BY nepesseg*1000_suruseg LIMIT 1;
```

43. Melyik a legnagyobb afrikai ország és mekkora?

```sql
SELECT orszag, terulet FROM orszagok WHERE foldr_hely LIKE '%Afrika%' ORDER BY terulet DESC LIMIT 1;
```

44. Melyik a legkisebb amerikai ország és hányan lakják?

```sql
SELECT orszag, nepesseg*1000 FROM orszagok WHERE foldr_hely LIKE '%Amerika%' ORDER BY terulet LIMIT 1;
```

45. Melyik az első három legsűrűbben lakott "országméretű" ország (tehát nem város- vagy törpeállam)?

```sql
SELECT orszag, nepesseg*1000 / terulet AS nepesseg_suruseg FROM orszagok ORDER BY nepesseg*1000_suruseg DESC LIMIT 3;
```

46. Melyik a világ hat legnépesebb fővárosa?

```sql
SELECT orszag, fovaros, nep_fovaros FROM orszagok ORDER BY nep_fovaros DESC LIMIT 6;
```

47. Melyik tíz ország egy főre jutó GDP-je a legnagyobb?

```sql
SELECT orszag, gdp / nepesseg*1000 AS gdp_per_capita FROM orszagok ORDER BY gdp_per_capita DESC LIMIT 10;
```

48. Melyik tíz ország össz-GDP-je a legnagyobb?

```sql
SELECT orszag, gdp FROM orszagok ORDER BY gdp DESC LIMIT 10;
```

49. Melyik országban a legszegényebbek az emberek?

```sql
SELECT orszag, gdp / nepesseg*1000 AS gdp_per_capita FROM orszagok ORDER BY gdp_per_capita LIMIT 1;
```

50. Melyik a 40. legkisebb területű ország?

```sql
SELECT orszag, terulet FROM orszagok ORDER BY terulet LIMIT 39,1;
```

51. Melyik a 15. legkisebb népsűrűségű ország?

```sql
SELECT orszag, nepesseg*1000 FROM orszagok ORDER BY nepesseg*1000 LIMIT 14,1;
```

52. Melyik a 61. legnagyobb népsűrűségű ország?

```sql
SELECT orszag, nepesseg*1000 / terulet AS nepesseg_suruseg FROM orszagok ORDER BY nepesseg*1000_suruseg DESC LIMIT 60,1;
```

53. Melyik három ország területe hasonlít leginkább Magyaroszág méretéhez?

```sql
SELECT orszag, terulet FROM orszagok WHERE terulet BETWEEN (SELECT terulet FROM orszagok WHERE orszag = 'MAGYARORSZÁG') - 50000 AND (SELECT terulet FROM orszagok WHERE orszag = 'MAGYARORSZÁG') + 50000 AND orszag <> 'MAGYARORSZÁG' ORDER BY ABS(terulet - (SELECT terulet FROM orszagok WHERE orszag = 'MAGYARORSZÁG')) LIMIT 3;
```

54. Az emberek hányadrésze él Ázsiában?

```sql
SELECT SUM(nepesseg*1000) / (SELECT SUM(nepesseg*1000) FROM orszagok) AS asia_lakossag_resz FROM orszagok WHERE foldr_hely LIKE '%Ázsia%';
```

55. A szárazföldek mekkora hányadát foglalja el Oroszország?

```sql
SELECT terulet / (SELECT SUM(terulet) FROM orszagok WHERE foldr_hely NOT LIKE '%víz%') AS oroszorszag_terulet_resz FROM orszagok WHERE orszag = 'OROSZORSZÁG';
```

56. Az emberek hány százaléka fizet euroval?

```sql
SELECT COUNT(*) / (SELECT COUNT(*) FROM orszagok) * 100 AS euroval_fizeto_lakossag_szazalek FROM orszagok WHERE penznem = 'euro';
```

57. Hányszorosa a leggazdagabb ország egy főre jutó GDP-je a legszegényebb ország egy főre jutó GDP-jének?

```sql
SELECT MAX(gdp / nepesseg*1000) / MIN(gdp / nepesseg*1000) AS gazdagsag_arany FROM orszagok;
```


58. A világ össz-GDP-jének hány százalékát adja az USA?

```sql
SELECT gdp / (SELECT SUM(gdp) FROM orszagok) * 100 AS usa_gdp_szazalek FROM orszagok WHERE orszag = 'EGYESÜLT ÁLLAMOK';
```

59. A világ össz-GDP-jének hány százalékát adja az euroövezet?

```sql
SELECT SUM(gdp) / (SELECT SUM(gdp) FROM orszagok WHERE penznem = 'euro') * 100 AS euroovezet_gdp_szazalek FROM orszagok WHERE penznem = 'euro';
```

60. Melyek azok az átlagnál gazdagabb országok, amelyek nem az európai vagy az amerikai kontinensen találhatóak?

```sql
SELECT orszag, gdp / nepesseg*1000 AS gdp_per_capita FROM orszagok WHERE gdp / nepesseg*1000 > (SELECT AVG(gdp / nepesseg*1000) FROM orszagok) AND foldr_hely NOT LIKE '%Európa%' AND foldr_hely NOT LIKE '%Amerika%';
```

61. Milyen államformák léteznek Európában?

```sql
SELECT DISTINCT allamforma FROM orszagok WHERE foldr_hely LIKE '%Európa%';
```

62. Hányféle államforma létezik a világon?

```sql
SELECT COUNT(DISTINCT allamforma) FROM orszagok;
```

63. Hányféle fizetőeszközt használnak Európában az eurón kívül?

```sql
SELECT COUNT(DISTINCT penznem) FROM orszagok WHERE foldr_hely LIKE '%Európa%' AND penznem <> 'euro';
```

64. Mely pénznemeket használják több országban is?  

```sql
SELECT penznem, COUNT(DISTINCT orszag) AS orszagok_szama FROM orszagok GROUP BY penznem HAVING COUNT(DISTINCT orszag) > 1;
```

65. Mely országok államformája egyedi?

```sql
SELECT orszag, allamforma FROM orszagok GROUP BY allamforma HAVING COUNT(DISTINCT orszag) = 1;
```
