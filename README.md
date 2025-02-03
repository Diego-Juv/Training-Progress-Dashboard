# 📄 Project Explanation

This documentation explains the code and the involved tables that are used to track the progress of training courses within a company from **2019 to 2024**. The purpose of the code is to analyze the course progress by determining which employees have completed courses and when, aggregating this information by organizational dimensions (such as department, address, and year of entry) and comparing performance over the years.

---

## 📊 Explanation of the Tables

### A. Dimension Tables

  - **`empleados` Table:** Contains information about employees (e.g., name, year of entry, address).
  - **`cursos` Table:** Lists all available courses.
  - **`puestos` Table:** Provides details about the positions held by employees, such as department.

### B. Fact Tables

- **`finalizados` Table:** Contains records of when employees completed courses, including dates and possibly other performance metrics.

- **Key Characteristics of Fact Tables:**
  - **Metrics:** Store values that can be aggregated (e.g., counts, sums).
  - **Foreign Keys:** Include keys that relate to dimension tables to provide contextual details (e.g., linking a course completion to an employee or course).
  - **High Volume:** Generally contain a large number of records as they capture each event or transaction.

---

## 📈 Final Dashboard
My final dashboard can be accessed at the following link:  

[Dashboard on Looker Studio](https://lookerstudio.google.com/reporting/f19786e8-759a-4a74-974b-dc005c91631a)

---

## 📄 MySQL Structure

[View the SQL Structure documentation](<SQL Structure.md>)


   🧑‍💻 SQL Skills Used:

- **WITH**: Defines Common Table Expressions (CTEs) to create temporary result sets that can be referenced within the main query.

- **CROSS JOIN**: Produces a Cartesian product of two tables, pairing each row from the first table with every row from the second.

- **LEFT JOIN**: Returns all rows from the left table and the matched rows from the right table; if no match is found, NULLs are returned for columns from the right table.

- **CASE**: Implements conditional logic to return specific values based on defined conditions.

- **ROW_NUMBER() OVER (PARTITION BY... ORDER BY...)**: Assigns a unique sequential integer to rows within a partition of the result set, ordered by specified columns.

- **PARTITION BY**: Divides the result set into partitions to which the ROW_NUMBER() function is applied.

- **ORDER BY**: Determines the sequence in which rows are returned or processed.

- **GROUP BY**: Aggregates data by grouping rows that share the same values in specified columns.

- **SUM()**: Calculates the total sum of a numeric column.

- **LAG() OVER (PARTITION BY... ORDER BY...)**: Accesses data from a previous row in the same result set without the need for a self-join.


