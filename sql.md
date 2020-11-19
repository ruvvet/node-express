# SQL NOTES

### Basics

select all

 ```SQL
SELECT * FROM tablename;
```

Select given specific parameters

```SQL
    field = 'somevalue';
    ...
    field IN ('value1', 'val2'...);
    ...
    field BETWEEN ...AND/OR...;
    ...
```

order by

```SQL
    ORDER BY... field
```

rename as

```SQL
    AS newname
```

### Conditionals

```SQL
AND
OR
XOR --true if one or the other, not both
```

### Operations

greater/less than
```SQL
SELECT field FROM tablename
    WHERE field2 >/</>=/<=/= somevalue;
```

can calculate new fields with matches
```SQL
SELECT field, mathstuffhere() FROM tablename
    WHERE....
```

### Strings

Select w/ wildcards
- % is a wildcard that can be any length
- _ (underscore) is one char slot
- use (str)% to find wildcards that start with the str
- %(str) that end with the str
- %(str)% contains the str
- (str start)%(str end) that returns any matches that start + end
- '%a%a%a%' finding any matches with 3 a's
- '_t%' where t is the second char in the string


```SQL

     LIKE '%str';
    ...
     LIKE 'str%';
    ...
     LIKE '%str%';
    ...
     LIKE 'strA%strB';
    ...
```

Length of a value/string

```SQL
    LENGTH(field) = ;
```

Concatenate strings

```SQL
    field2 = CONCAT(field, ' something');
```

Escaping single quote

```SQL
    People''s --double up the quote
```

### Functions

Get leftmost values

```SQL
    LEFT(field, #);
```

Round to specific # of decimal places

```SQL
    ROUND(#, number of decimal places);
```

Sum, count functions that aggregate results

```SQL
    SUM(field) --sum of returned matches

    COUNT(field) --# of returned matches
```

Max, Distinct which filter after query

```SQL
    DISTINCT(field) -- gives unique matches

    MAX(field) --gives max
```

Case for 'if/elif/else'

```SQL
CASE WHEN ...THEN...ELSE...END
```


Coalesce gets first non-null value

```SQL
    COALESCE (arg1, arg2) -- takes arguments and returns first non-null value
```

Group by, having which also filter after the query is returned

```SQL
    GROUP BY field -- used with sum/count where fields are aggrgated in select output
    HAVING -- filters displayed output (unlike WHERE which filters ths query)
```

Use a boolean to order things

```SQL
    WHERE field IN ('...') -- returns a boolean
    -- then order by the boolean
    ORDER BY field IN ('...')
```

Select in select

```SQL
--identify diff aliases for inner/outer select tables
SELECT continent, name, area
    FROM world x --name of outer
    WHERE area >=
        ALL
            (SELECT area
                FROM world y -- name of inner
                WHERE y.continent=x.continent AND area>0);
```

### Joins

```SQL
(INNER) JOIN -- returns all rows from both where ther are no null values
LEFT (OUTER) JOIN -- retiurns all from left, and matching from right, this means left can have null values
RIGHT (OUTER) JOIN -- returns all from right table, matching from left, so right table can have null
FULL (OUTER) JOIN -- returns all when there is a match in either table
```

