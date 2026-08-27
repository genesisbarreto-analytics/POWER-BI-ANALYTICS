# DAX Measures — Digital Channel Performance Dashboard

Las siguientes medidas son ejemplos anonimizados y simplificados de lógica utilizada en dashboards de adopción y comportamiento digital.

## Total Access

```DAX
Total Access =
COUNTROWS(FactDigitalActivity)
```

## Active Users / MAUs

```DAX
Active Users =
DISTINCTCOUNT(FactDigitalActivity[UserId])
```

## Access per MAU

```DAX
Access per MAU =
DIVIDE(
    [Total Access],
    [Active Users],
    0
)
```

## Previous Month Access

```DAX
Previous Month Access =
CALCULATE(
    [Total Access],
    DATEADD(DimDate[Date], -1, MONTH)
)
```

## Monthly Access Variation

```DAX
Monthly Access Variation =
DIVIDE(
    [Total Access] - [Previous Month Access],
    [Previous Month Access],
    0
)
```

## New Customers

```DAX
New Customers =
CALCULATE(
    DISTINCTCOUNT(FactDigitalActivity[CustomerId]),
    FILTER(
        VALUES(FactDigitalActivity[CustomerId]),
        [First Access Date] >= MIN(DimDate[Date]) &&
        [First Access Date] <= MAX(DimDate[Date])
    )
)
```

## Segment Share

```DAX
Segment Share =
DIVIDE(
    [Total Access],
    CALCULATE(
        [Total Access],
        ALL(DimSegment[Segment])
    ),
    0
)
```

> Nota: los nombres de tablas, columnas y lógica han sido simplificados para fines de portafolio.
