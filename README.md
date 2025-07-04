# Analyzing Industry Carbon Emissions

### Project Overview

![pollution](https://github.com/user-attachments/assets/a00114a4-ab24-409b-b703-fce8f311b9cd)

Photo by Maxim Tolchinskiy on Unsplash
  
When factoring heat generation required for the manufacturing and transportation of products, _Greenhouse gas emissions attributable to products, from food to sneakers to appliances, make up more than 75% of global emissions._

(Source: The Carbon Catalogue https://www.nature.com/articles/s41597-022-01178-9)

### Data Sources

Our data, which is publicly available on nature.com, contains product carbon footprints (PCFs) for various companies. PCFs are the greenhouse gas emissions attributable to a given product, measured in CO<sub>2</sub> (carbon dioxide equivalent).

This data is stored in a PostgreSQL database containing one table, `product_emissions`, which looks at PCFs by product as well as the stage of production that these emissions occurred. Here's a snapshot of what `product_emissions` contains in each column:

<h4><code>product_emissions</code></h4>

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Data Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>id</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>year</code></td>
      <td><code>INT</code></td>
    </tr>
    <tr>
      <td><code>product_name</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>company</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>country</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>industry_group</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>weight_kg</code></td>
      <td><code>NUMERIC</code></td>
    </tr>
    <tr>
      <td><code>carbon_footprint_pcf</code></td>
      <td><code>NUMERIC</code></td>
    </tr>
    <tr>
      <td><code>upstream_percent_total_pcf</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>operations_percent_total_pcf</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
    <tr>
      <td><code>downstream_percent_total_pcf</code></td>
      <td><code>VARCHAR</code></td>
    </tr>
  </tbody>
</table>

### Key Question
Which industries are the worst offenders in 2017?

### Data Analysis
Include some interesting code/features worked with

```sql
-- Carbon Emissions by Industry
SELECT industry_group,
       COUNT(DISTINCT company) AS num_companies,
       ROUND(SUM(carbon_footprint_pcf),1) AS total_industry_footprint
FROM product_emissions
WHERE year = 2017
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
```

### Results/Findings
In 2017, the industry group with the highest total carbon footprint was "Materials", with a total industry footprint of 107,129 kgCO<sub>2</sub>. This group consists of three different companies.

### Recommendations
- Prioritize carbon reduction initiatives and sustainability programs on industries with the highest total carbon footprint.
- Encourage and support industries with lower carbon footprints to maintain their sustainable practices.
- Industries with a large number of companies but a high total carbon footprint should be encouraged to adopt energy-efficient technologies and practices.

