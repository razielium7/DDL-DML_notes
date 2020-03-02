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
	{ SELECT... | DEFAULT VALUES | VALUES (<valor1>, <valor2>, <vlalorN>), (valorX, <valorY>, <valorZ>)};
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
SELECT nombre, continente, capitál-del-pais
FROM mundo
WHERE continent LIKE 'Europa';
```
Los atributos de INSERT y SELECT deben de pertenecer a mismos dominios y respetar la orden.

**UPDATE**- actualiza.

```SQL

```


**DELETE**- elimina.

```SQL

```