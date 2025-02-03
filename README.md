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

## 🔍 Code Structure Overview

### 1. CTE `primeros_finalizados`

- **Purpose:**  
  Identify, for each combination of employee and course, the **first date** when the course was completed.

- **What It Does:**  
  - Selects data from the `finalizados` table.
  - Uses the `ROW_NUMBER()` window function partitioned by `id_empleado` and `id_curso`, ordering by `fecha_finalizacion` in ascending order.
  - Renames `fecha_finalizacion` as `primer_fecha` and assigns a sequential number to each record so that only the first completion (where the number is 1) is considered.

---

### 2. CTE `Datos`

- **Purpose:**  
  Generate a detailed dataset that includes every combination of employees and courses, indicating whether each course was completed or not.

- **What It Does:**  
  - **CROSS JOIN:** Combines the `empleados` and `cursos` tables to obtain all possible combinations.
  - **JOIN:** Merges data from the `puestos` table to add additional details (such as department).
  - **LEFT JOIN:** Connects with the `primeros_finalizados` CTE to determine if a course was completed, filtering to only consider the first occurrence (`Veces_finalizado = 1`).
  - **CASE Statement:** Assigns a numerical status:
    - `1` if the course was completed (i.e., a valid `primer_fecha` exists).
    - `0` if the course is pending (i.e., `primer_fecha` is NULL).
  - Extracts additional fields like the date and year of completion.

---

### 3. CTE `Datos_agrupados`

- **Purpose:**  
  Consolidate the detailed data by grouping it according to organizational dimensions such as **department**, **address**, and **year of entry**.

- **What It Does:**  
  - Groups data from `Datos` by `departamento`, `direccion`, and `año_ingreso`.
  - Sums the `Estatus` field to calculate the number of completed courses per group.
  - Uses a window function (combining `SUM` and `COUNT`) to compute the total number of courses evaluated for each employee across the groups.

---

### 4. Final Query

- **Purpose:**  
  Present the final report with aggregated data, including year-over-year comparisons.

- **What It Does:**  
  - Selects data from `Datos_agrupados`, including:
    - `departamento`
    - `direccion`
    - `año_ingreso`
    - `Completados` (total completed courses)
    - `Total` (total courses evaluated)
  - Utilizes the `LAG` window function to retrieve the previous year's `Completados` and `Total` values (based on `año_ingreso`) for each `departamento` and `direccion` combination.
  - Orders the final output by `departamento`, `direccion`, and `año_ingreso` for clear analysis.

---


## 🚀 Overall Purpose

The overall objective of this code and its supporting tables is to:

- **Determine First Completions:**  
  Identify the first instance of course completion for each employee-course pair.

- **Create a Comprehensive Dataset:**  
  Generate a complete list of all possible employee-course combinations, indicating course completion status (1 for completed, 0 for pending).

- **Aggregate and Analyze Data:**  
  Group the data by relevant organizational dimensions (department, address, year of entry) to calculate key performance metrics.


