##DML Restricciones
**Clave principal**- convierte el atributo en la clave primaria aplicando restricciones iplicitas de unicidad y obligatoriedad.

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

**Check**

    SQL
    [CONSTRAINT <nombre-de-restricción>]
    	NOT NULL (<atributo1,atributo2>)