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



