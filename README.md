# Molding Machine

Este repositorio es parte integral del proyecto "API Factory", una aplicación centrada en la generación de código basada en las mejores prácticas. A continuación, se presenta información esencial sobre el modelo de datos y cómo transformarlo en un CRUD.

## Modelo de Datos

El aplicativo emplea un modelo de datos que define la estructura de una entidad llamada empleado:

```yaml
employee:
  properties:
    employee_id:
      type: integer
      primary_key: true
      auto_increment: true
    first_name:
      type: string
      not_null: true
    last_name:
      type: string
      not_null: true
    birth_date:
      type: date
    address:
      type: string
    email:
      type: string
    phone_number:
      type: string
    document_type:
      type: string
      enum: ['DNI', 'RUC', 'CE', 'PPT']
    document_number:
      type: string
    position:
      type: string
      enum: ['TM', 'LT', 'PO', 'CL']
      default: 'TM'
    additional_info:
      type: string
    created:
      type: datetime
      default: 'CURRENT_TIMESTAMP'
    updated:
      type: datetime
      default: 'CURRENT_TIMESTAMP'
      on_update: 'CURRENT_TIMESTAMP'
    recorder:
      type: string
      default: ''
    active:
      type: boolean
      default: false
```

A continuación, se proporciona la sentencia SQL (compatible con MariaDB) para crear la tabla:

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
