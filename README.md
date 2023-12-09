# Molding Machine

Este repositorio es parte integral del proyecto "API Factory", una aplicación centrada en la generación de código basada en las mejores prácticas. A continuación, se presenta información esencial sobre el modelo de datos y cómo transformarlo en un CRUD.

## Modelo de Datos

El aplicativo genera un modelo de datos que define la estructura de una entidad llamada empleado:

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
      enum: ["DNI", "RUC", "CE", "PPT"]
    document_number:
      type: string
    position:
      type: string
      enum: ["TM", "LT", "PO", "CL"]
      default: "TM"
    additional_info:
      type: string
    created:
      type: datetime
      default: "CURRENT_TIMESTAMP"
    updated:
      type: datetime
      default: "CURRENT_TIMESTAMP"
      on_update: "CURRENT_TIMESTAMP"
    recorder:
      type: string
      default: ""
    active:
      type: boolean
      default: false
```

A continuación, se proporciona la sentencia SQL para crear la tabla en MariaDB:

```sql
CREATE TABLE tbl_employees (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    birth_date DATE,
    address VARCHAR(255),
    email VARCHAR(255),
    phone_number INT,
    document_type ENUM("DNI", "RUC", "CE", "PPT"),
    document_number INT,
    position ENUM("TM", "LT", "PO", "CL") DEFAULT "TM",
    additional_info VARCHAR(255),
    created DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    recorder VARCHAR(255) DEFAULT "",
    active BOOLEAN DEFAULT FALSE
) AUTO_INCREMENT=1;
```
A continuación, se proporciona la especificación OpenAPI:

```yaml
openapi: 3.0.0
info:
  title: Employees API
  version: 1.0.0
paths:
  /employees:
    get:
      summary: Retrieve a list of employees
      responses:
        "200":
          description: Successful response
    post:
      summary: Create a new employee
      requestBody:
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Employee"
      responses:
        "201":
          description: Employee created successfully
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Employee"
components:
  schemas:
    Employee:
      type: object
      properties:
        employee_id:
          type: integer
          format: int32
        first_name:
          type: string
          maxLength: 255
        last_name:
          type: string
          maxLength: 255
        birth_date:
          type: string
          format: date
        address:
          type: string
          maxLength: 255
        email:
          type: string
          format: email
          maxLength: 255
        phone_number:
          type: integer
        document_type:
          type: string
          enum: ["DNI", "RUC", "CE", "PPT"]
        document_number:
          type: integer
        position:
          type: string
          enum: ["TM", "LT", "PO", "CL"]
          default: "TM"
        additional_info:
          type: string
          maxLength: 255
        created:
          type: string
          format: date-time
        updated:
          type: string
          format: date-time
        recorder:
          type: string
          maxLength: 255
        active:
          type: boolean
          default: false
      required:
        - first_name
        - last_name
```
