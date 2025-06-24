# Analyzing Industry Carbon Emissions

### Project Overview

![pollution](https://github.com/user-attachments/assets/a00114a4-ab24-409b-b703-fce8f311b9cd)

Photo by Maxim Tolchinskiy on Unsplash
  
When factoring heat generation required for the manufacturing and transportation of products, _Greenhouse gas emissions attributable to products, from food to sneakers to appliances, make up more than 75% of global emissions._

(Source: The Carbon Catalogue https://www.nature.com/articles/s41597-022-01178-9)

### Data Sources

Our data, which is publicly available on nature.com, contains product carbon footprints (PCFs) for various companies. PCFs are the greenhouse gas emissions attributable to a given product, measured in CO<sub>2</sub> (carbon dioxide equivalent).

This data is stored in a PostgreSQL database containing one table, `product_emissions`, which looks at PCFs by product as well as the stage of production that these emissions occurred. Here's a snapshot of what `product_emissions` contains in each column:

### `product_emissions`

| field                              | data type |
|------------------------------------|-----------|
| `id`                                 | `VARCHAR`   |
| `year`                               | `INT`       |
| `product_name`                       | `VARCHAR`   |
| `company`                            | `VARCHAR`   |
| `country`                            | `VARCHAR`   |
| `industry_group`                     | `VARCHAR`   |
| `weight_kg`                          | `NUMERIC`   |
| `carbon_footprint_pcf`               | `NUMERIC`   |
| `upstream_percent_total_pcf`         | `VARCHAR`   |
| `operations_percent_total_pcf`       | `VARCHAR`   |
| `downstream_percent_total_pcf`       | `VARCHAR`   |

We'll use this data to examine the carbon footprint of each industry in the dataset! 

### Key Questions
Which industries are the worst offenders in 2017?

### Data Analysis

```sql
-- Carbon Emissions by Industry
SELECT industry_group, COUNT(DISTINCT company) AS num_companies, ROUND(SUM(carbon_footprint_pcf),1) AS total_industry_footprint
FROM product_emissions
WHERE year = 2017
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
```

### Results/Findings
In 2017, the industry group with the highest total carbon footprint was "Materials," with a total industry footprint of 107,129 kgCO2. This group consists of three different companies.

### Recommendations
- Prioritize carbon reduction initiatives and sustainability programs on industries with the highest total carbon footprint.
- Encourage and support industries with lower carbon footprints to maintain their sustainable practices.
- Industries with a large number of companies but a high total carbon footprint should be encouraged to adopt energy-efficient technologies and practices.

