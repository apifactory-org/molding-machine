# Molding Machine

Este repositorio es parte integral del proyecto "API Factory", una aplicación centrada en la generación de código basada en las mejores prácticas. A continuación, se presenta información esencial sobre el modelo de datos y cómo transformarlo en un CRUD.

## Modelo de Datos

El aplicativo emplea un modelo de datos que define la estructura de la tabla de empleados en la base de datos. A continuación, se proporciona la sentencia SQL (compatible con MariaDB) para crear la tabla:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    birth_date DATE,
    address VARCHAR(255),
    email VARCHAR(255),
    phone_number INT,
    document_type ENUM('DNI', 'RUC', 'CE', 'PPT'),
    document_number INT,
    position ENUM('TM', 'LT', 'PO', 'CL') DEFAULT 'TM',
    additional_info VARCHAR(255),
    created DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    recorder VARCHAR(255) DEFAULT '',
    active BOOLEAN DEFAULT FALSE
) AUTO_INCREMENT=1;
```
