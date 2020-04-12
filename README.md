## Índice:

  - [DML](#DML)
    - [INSERT](#INSERT)
    - [UPDATE](#UPDATE)
    - [DELETE](#DELETE)
  - [Tipos de datos](#Tipos-de-datos)
  - [DDL](#DDL)
    - [Restricciones](#Restricciones)
    - [CHECK](#CHECK)
    - [CREATE](#CREATE)
    - [DROP](#DROP)
    - [ALTER](#ALTER)



# DML 

----------
## INSERT

["Referencias PostgreSQL"](https://www.postgresql.org/docs/9.4/sql-insert.html "Referencias PostgreSQL")

**INSERT**- Introduce valores para los atributos seleccionados. Pueden ser resultado de una consulta, valores por defecto, o valores escritos (coincidiendo en orden los valores con los atributos).

En MariaDB "INTO" es opcional, en PostgreS es obligatorio.

```SQL
INSERT INTO <nombre-de-tabla> 
	( <atributo1>, <atributo2>, <valorN>...) 
	{ SELECT...| VALUES (<valor1>, <valor2>, <vlalorN>), (vl.X, <vl.Y>, <vl.Z>)};
```

Ejemplo VALUES:

```SQL
INSERT INTO world
(name, continent, capital)
VALUES
('Spain', 'Europe', 'Madrid')
('Germany', 'Europe', 'Berlin')
('Japan', 'Asia', 'Tokyo');
```

Ejemplo SELECT:

```SQL
INSERT INTO world
	(name, continent, capital)
SELECT 	nombre, continente, capitál-del-pais
FROM mundo
WHERE continent LIKE 'Europa';
```
Los atributos de INSERT y SELECT deben de pertenecer a mismos dominios y respetar la orden.

## UPDATE

**UPDATE**- actualiza los atributos de las tuplas de la tabla.


```SQL
UPDATE <nombre-de-tabla>
	SET	<atributo1> = <valor1>,
		<atributo2> = <valor2>
		[WHERE <predicado>];
```

Ejemplo:

```SQL
UPDATE world
	SET 	continent = 'Africa'
	WHERE 	name = 'Spain'
	OR	name = 'Portugal';
```


## DELETE
**DELETE**- elimina las tuplas seleccionadas.


```SQL
DELETE FROM <nombre-de-tabla>
[WHERE <predicados>];
```

NO DEJAR EL PREDICADO VACIO, por muy opcional que sea!

Ejemplo:

```SQL
DELETE FROM world
WHERE continent LIKE 'Europe';
```


----------
![desk1](/img/desk3.jpg)


----------

# Tipos de datos


| tipo de datos | desc.                                                |
|---------------|------------------------------------------------------|
| INTEGER       | número entero                                        |
| DECIMAL       | número preciso                                       |
| REAL          | número no preciso                                    |
| -             | -                                                    |
| CHAR          | texto de longitud fija (40 -> 40, ni más ni menos)   |
| VARCHAR       | texto de longitud variable (40 -> 0-40)              |
| TEXT          | texto de longitud ilimitada/ usar para descripciones |
| -             | -                                                    |
| DATE          | día, mes, año                                        |
| TIME          | hora, minuto, segundo [zona horaria]                 |
| TIMESTAMP     | DATE+TIME                                            |


| BOOLEAN | desc.                                        |
|---------|----------------------------------------------|
| TRUE    | verdadero                                    |
| FALSE   | falso                                        |
| NULL    | nulo                                         |
| -       | -                                            |
| MONEY   | evita problemas como 0.1+0.2=3.0...04        |
| -       | -                                            |
| UUID    | identificador universal único (programación) |
| JSON    | java script object notation                  |
| XML     | extensible markup                            |
| CIDR    | classless interdomain routing                |
| INET    | direccionamiento IpV4 / IpV6                 |



----------
# DDL - Data Definition Language


## Restricciones

**Clave principal**- convierte el atributo en la clave primaria aplicando restricciones implícitas de unicidad y obligatoriedad.

```SQL
[CONSTRAINT <nombre-de-restricción>]
	PRIMARY KEY (<atributo1>[,<atributo2>...]),
```

**La clave pricipal puede estar formada por mas de un atributo!**

Puede definirse en la misma estrofa que el atributo o posteriormente como CONSTRAINT.

```sql
CREATE TABLE alumnos (
	nombre VARCHAR(20) PRIMARY KEY;
);
```



**Unicidad**  - obligación de un atributo a ser único e irrepetible.

```SQL
[CONSTRAINT <nombre-de-restricción>]
	UNIQUE (<atributo1,atributo2>),
```

**Obligatoriedad** - prohibe al atributo tener NULL como valor, obliga a tener un valor en todo instante.

```SQL
[CONSTRAINT <nombre-de-restricción>]
	NOT NULL (<atributo1,atributo2>),
```

**Clave ajena** - establece restricciones sobre la clave ajena, solo puede tomar valores de la clave principal de referenciada o nulo. Es importante definir el comportamiento a la hora de actualización/borrado de la tabla referenciada.

```SQL
[CONSTRAINT <nombre-de-restricción>]
	FOREIGN KEY (<atributo1,atributo2>)
	REFERENCES <nombre-re-tabla-referenciada> (<clave referenciada>)
	ON DELETE [CASCADE | NO ACTION | SET NULL | SET DEFAULT]
	ON UPDAte [CASCADE | NO ACTION | SET NULL | SET DEFAULT]
```

- ON DELETE define la reacción al borrado.

- ON UPDATE define reacción a la modificación.

| NO ACTION   | habilitado por defecto, ausencia de efecto alguno                                                                    |
|-------------|----------------------------------------------------------------------------------------------------------------------|
| SET DEFAULT | requiere que exista un valor por defecto (de lo contrario saltaría a NULL), ante cambios establece valor por defecto |
| SET NULL    | pone datos a NULL                                                                                                    |
| CASCADE     | los datos se actualizan junto con sus referencias, en caso de borrado se eliminan junto con ellos                    |

----------

## CHECK
Parametro que nos permite limitar los valores de los atributos.
Puede ser una limitación numérica, por comparación o, incluso, mediante un predicado (WHERE).

```sql
CREATE TABLE profesores (
  nombre VARCHAR(30) PRIMARY KEY,
  fechaInicio DATE, 
  fechaFinContrato DATE,
  CONSTRAINT Check_fechas
    CHECK (fechaInicio < fechaFinContrato),
    );
```
A la hora de la creación de tabla condicionamos las fechas, prohibiendo que la fecha de fin de contrato sea anterior a su inicio. Los únicos que tienen derecho de hacerlo son Einstein y Hawking con sus experimentos cuánticos.

----------


##  CREATE
Comando para crear bases de datos, esquemas, tablas y dominios.


#### **Crear base de datos:**

```SQL
CREATE DATABASE <nombre>;
```

Opcionalmente podemes emplear ```IF NOT EXISTS``` para evitar errores por coincidencias de nombres.


```SQL
CREATE DATABASE [IF NOT EXIST] <nombre>;
```

#### De misma forma se crearia un **esquema:** 

```SQL
CREATE SCHEMA [IF NOT EXIST] <nombre>;
```

#### Crear dominio:
A la hora de **crear dominio** sera necesario especificar el tipo de datos del dominio para, posteriormente, poder referirse a el y tener mas ergonomía de trabajo.

```SQL
CREATE DOMAIN <nombre> <tipo_dato;
```

Ejemplos:

```SQL
CREATE DOMAIN nombrePers VARCHAR(15);
```
```SQL
CREATE DOMAIN tipoDNI CHAR(9);
```

#### Crear tabla:


Durante la creación de tabla podemos especificar las los atributos, su tipo de datos y restricciones. Tambien podemos introducir los "CHECK" y "CONSTRAINT" a la hora de crear una tabla.


 ```sql
	 CREATE TABLE <nombre> (
	 <nombre_atributo1> <tipo_dato> <restricción> ,
	 <nombre_atributo2> <tipo_dato> <restricción> ,
	 [CONSTRAINT]
);
```


Ejemplo:


 ```sql
	 CREATE TABLE personal (
	 apellido VARCHAR(30) NOT NULL,
	 dni tipoDNI ,
	 sueldo INTEGER (8) ,
	 CONSTRAINT PK_att
	 PRIMARY KEY (dni),
	 CHECK (sueldo => 0)
);
```


## DROP


Comando para la eliminación de tablas, bases de datos y esquemas.


**Base de datos**:

 ```sql
	 DROP DATABASE <nombre-de-BD-existente>
	[CASCADE | RESTRICT ];
```


**Esquema**:

 ```sql
	 DROP SCHEMA <nombre-de-schema-existente>
	[CASCADE | RESTRICT ] ;
```


**Tabla**:

 ```sql
	 DROP TABLE <nombre-de-tabla-existente>
	[CASCADE | RESTRICT ] ;
```


Los parametros opcionales CASCADE y RESTRICT  definen la forma de borrado:

Para evitar un borrado accidental de una base de datos o tabla que tienen datos almacenados se usaría **RESTRICT**

Para una eliminación continua del elemento indicado se usaría **CASCADE**.


----------

## ALTER

["MariaDB ALTER"](https://mariadb.com/kb/en/alter-table)

Comando para modificar una tabla, renombrar la tabla o sus columnas, agegar/quitar CONSTRAINT y columnas.

```sql
ALTER TABLE <nombre-de-tabla-existente>
    [RENAME TO <nombre-nuevo>],
    [RENAME COLUMN <nombre-de-columna> TO <nombre-nuevo>],
    [ADD | DROP [COLUMN | CONSTRAINT] <nombre>];
```

Ejemplos:


```sql
ALTER TABLE personal
    ADD departamento VARCHAR(20);
```
Hemos agregado columna "departamento"


```sql
ALTER TABLE personal
    ADD CONSTRAINT FK_departamento
    FOREIGN KEY (departamento)
    REFERENCES departamentos (departamento)
    ON DELETE SET NULL
    ON UPDATE CASCADE;
```
Hemos definido "departamento" como clave agena que hae referencia a la tabla departamentos.


```sql
ALTER TABLE personal
    DROP PRIMARY KEY;
```
Hemos anulado la restricción de la clave principal.


```sql
ALTER TABLE personal
    ADD CONSTRAINT PK_compuesta
    PRIMARY KEY (dni,departamento);
```
Hemos agregado nueva clave principal compuesta por "dni" y "departamento"


- Nota importante! ```A la hora de establecer clave ajena es necesario definir su comportamiento respeto a la modificación de la clave referenciada```

![desk1](/img/desk1.jpg)
