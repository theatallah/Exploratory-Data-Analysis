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
The Result can be found [here]


