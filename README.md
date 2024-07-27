# Exploratory-Data-Analysis

## 1. Introduction:

Project is based on number of layoffs across the world in different sectors from year 2020 till 2023, The data is taken from alex the analyst youtube channel , link to the video [Press here for the link](https://www.youtube.com/watch?v=QYd-RtK58VQ&t=563s)

## 2. Data Used:

The data used is CSV File ,you can download here [layoffs.csv](https://github.com/theatallah/Exploratory-Data-Analysis/tree/main/CSV%20Files)

## 3. Tools Used:

The tools used are mysql workbench, which is a free license database software

## 4. The analysis:

### Question 1: Max Laid off

The Maximum number of laid off employees 

``` SQL
SELECT max(total_laid_off)
FROM layoffs_final;
```
The Result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%201.jpg)

### Question 2: Laid off all staff

The Companies that laid off all their staff

``` SQL
SELECT *
FROM layoffs_final
WHERE percentage_laid_off=1;
```
The Result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%202.jpg)

### Question 3: Sum of total laid off by company

```SQL
SELECT company,sum(total_laid_off) AS total_laid_off
FROM layoffs_final
GROUP BY company
ORDER BY 2 DESC;
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%203.jpg)
### Question 4: Layoffs by industry

```SQL
SELECT industry,sum(total_laid_off) total_laid_off
FROM layoffs_final
GROUP BY industry
ORDER BY total_laid_off DESC;
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%204.jpg)
### Question 5: layoffs by countries

```SQL
SELECT country,SUM(total_laid_off) AS total_laid_off
FROM layoffs_final
GROUP BY country	
ORDER BY 2 DESC;
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%205.jpg)
### Question 6: Layoffs by years

```SQL
SELECT YEAR(`date`),sum(total_laid_off)
FROM layoffs_final
GROUP BY year(`date`);
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%206.jpg)
### Question 7: Layoffs by company stage

```SQL
SELECT stage,sum(total_laid_off) total_laid_off
FROM layoffs_final
GROUP BY stage
ORDER BY 2 DESC;
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%207.jpg)

### QUESTION 8: Rolling Total of layoffs over years

```SQL
WITH Rolling_total AS (
SELECT YEAR(`date`) year,month(`date`) month,sum(total_laid_off) AS total_laid_off
FROM layoffs_final
WHERE YEAR(`date`) IS NOT NULL
GROUP BY year,month
ORDER BY year,month)

SELECT year,month,total_laid_off,SUM(total_laid_off) OVER (ORDER BY year,month) AS Rolling_total_layoffs
FROM Rolling_total;
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%208.jpg)

### Question 9: Layoffs by year & Company

```SQL
SELECT company,year(date) year,sum(total_laid_off) as total_layoffs
FROM layoffs_final
WHERE total_laid_off IS NOT NULL
GROUP BY company,year
ORDER BY total_layoffs DESC;
```
The result can be found [here](https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%209.jpg)

### Question 10 : Rank the layoffs by years and company

```SQL
WITH all_company AS (
SELECT company,year(date) year,sum(total_laid_off) as total_layoffs
FROM layoffs_final
WHERE total_laid_off IS NOT NULL AND year(date) is not null
GROUP BY company,year
ORDER BY total_layoffs DESC),
company_rankings AS (
SELECT *,dense_rank() OVER (partition by year ORDER BY total_layoffs DESC) AS layoffs_rank
FROM all_company)
```

### Question 11: Top 5 company layoffs by year

```SQL
WITH all_company AS (
SELECT company,year(date) year,sum(total_laid_off) as total_layoffs
FROM layoffs_final
WHERE total_laid_off IS NOT NULL AND year(date) is not null
GROUP BY company,year
ORDER BY total_layoffs DESC),
company_rankings AS (
SELECT *,dense_rank() OVER (partition by year ORDER BY total_layoffs DESC) AS layoffs_rank
FROM all_company)
SELECT *
FROM company_rankings
WHERE layoffs_rank<=5
```
The result for questions 10 & 11 can be found [here](
https://github.com/theatallah/Exploratory-Data-Analysis/blob/main/Questions%20snapshots/question%2010%20%26%2011.jpg)
