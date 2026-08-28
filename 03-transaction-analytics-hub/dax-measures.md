# DAX Measures — Transaction Analytics Hub

Ejemplos portfolio-safe de medidas reutilizables para un producto BI con múltiples dominios funcionales.

## Total Transactions
```DAX
Total Transactions =
COUNTROWS(FactTransactions)
```

## Active Users / MAUs
```DAX
Active Users =
DISTINCTCOUNT(FactTransactions[UserId])
```

## Daily Average
```DAX
Daily Average =
DIVIDE(
    [Total Transactions],
    DISTINCTCOUNT(DimDate[Date]),
    0
)
```

## Previous Month Transactions
```DAX
Previous Month Transactions =
CALCULATE(
    [Total Transactions],
    DATEADD(DimDate[Date], -1, MONTH)
)
```

## Monthly Growth
```DAX
Monthly Growth =
DIVIDE(
    [Total Transactions] - [Previous Month Transactions],
    [Previous Month Transactions],
    0
)
```

## Functionality Share
```DAX
Functionality Share =
DIVIDE(
    [Total Transactions],
    CALCULATE(
        [Total Transactions],
        ALL(DimFunctionality[Functionality])
    ),
    0
)
```

## Segment Share
```DAX
Segment Share =
DIVIDE(
    [Total Transactions],
    CALCULATE(
        [Total Transactions],
        ALL(DimSegment[Segment])
    ),
    0
)
```

## Activations
```DAX
Activations =
CALCULATE(
    [Total Transactions],
    FactTransactions[Action] = "Activation"
)
```

## Deactivations
```DAX
Deactivations =
CALCULATE(
    [Total Transactions],
    FactTransactions[Action] = "Deactivation"
)
```

> Nota: los nombres de tablas, campos y reglas fueron simplificados para fines de portafolio.
