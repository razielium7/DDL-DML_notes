## DML Restricciones

**Clave principal**- convierte el atributo en la clave primaria aplicando restricciones implícitas de unicidad y obligatoriedad.

```SQL
[CONSTRAINT <nombre-de-restricción>]
	PRIMARY KEY (<atributo),
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

**Clave ajena** - establece restricciones sobre la clave ajena, solo puede tomar valores de la clave principal de referenciada o nulo.

```SQL
[CONSTRAINT <nombre-de-restricción>]
	FOREIGN KEY (<atributo1,atributo2>)
	REFERENCES <nombre-re-tabla-referenciada> (<clave referenciada>)
```


| Restricción         | uso                                                                                                                                                                  |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Clave principal** | convierte el atributo en la clave primaria aplicando restricciones implícitas de unicidad y obligatoriedad                                                           |
|                     | ```SQL   [CONSTRAINT <nombre-de-restricción>]       PRIMARY KEY (<atributo),   ```                                                                                   |
| **Unicidad**        | obligación de un atributo a ser único e irrepetible                                                                                                                  |
|                     | ```SQL   [CONSTRAINT <nombre-de-restricción>]       UNIQUE (<atributo1,atributo2>),   ```                                                                            |
| **Obligatoriedad**  | prohibe al atributo tener NULL como valor, obliga a tener un valor en todo instante                                                                                  |
|                     | ```SQL   [CONSTRAINT <nombre-de-restricción>]       NOT NULL (<atributo1,atributo2>),   ```                                                                          |
| **Clave ajena**     | establece restricciones sobre la clave ajena, solo puede tomar valores de la clave principal de referenciada o nulo                                                  |
|                     | ```SQL   [CONSTRAINT <nombre-de-restricción>]       FOREIGN KEY (<atributo1,atributo2>)       REFERENCES <nombre-re-tabla-referenciada> (<clave referenciada>)   ``` |

----------


![desk1](/img/desk1.jpg)

----------

[https://www.postgresql.org/docs/9.4/sql-insert.html](https://www.postgresql.org/docs/9.4/sql-insert.html "Referencias PostgreSQL")

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

### Tipos de datos


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