# DAX Measures — Omnichannel Automation & Business Value

Ejemplos portfolio-safe de medidas utilizadas para representar lógica omnicanal y automatización.

## Total Transactions

```DAX
Total Transactions =
COUNTROWS(FactOmnichannel)
```

## Automated Transactions

```DAX
Automated Transactions =
CALCULATE(
    [Total Transactions],
    FactOmnichannel[TransactionType] = "Automated"
)
```

## Automation Rate

```DAX
Automation Rate =
DIVIDE(
    [Automated Transactions],
    [Total Transactions],
    0
)
```

## Active Users / MAUs

```DAX
Active Users =
DISTINCTCOUNT(FactOmnichannel[UserId])
```

## Channel Share

```DAX
Channel Share =
DIVIDE(
    [Total Transactions],
    CALCULATE(
        [Total Transactions],
        ALL(DimChannel[Channel])
    ),
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

## Revenue

```DAX
Revenue =
SUM(FactOmnichannel[RevenueAmount])
```

## Collections

```DAX
Collections =
SUM(FactOmnichannel[CollectionAmount])
```

> Nota: los nombres de tablas, campos y reglas han sido simplificados para fines de portafolio. Los valores del mockup son demostrativos.
