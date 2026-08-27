# DAX Measures — Virtual Assistant Analytics & Containment

Ejemplos portfolio-safe de medidas utilizadas para representar la lógica analítica del dashboard.

## Atenciones Totales

```DAX
Atenciones Totales =
COUNTROWS(FactAssistantInteractions)
```

## Atenciones Válidas

```DAX
Atenciones Válidas =
CALCULATE(
    [Atenciones Totales],
    FactAssistantInteractions[EsValida] = TRUE()
)
```

## Atenciones Solo BOT

```DAX
Atenciones Solo BOT =
CALCULATE(
    [Atenciones Válidas],
    FactAssistantInteractions[DerivadaSM] = FALSE()
)
```

## MAUs Solo BOT

```DAX
MAUs Solo BOT =
CALCULATE(
    DISTINCTCOUNT(FactAssistantInteractions[UsuarioId]),
    FactAssistantInteractions[DerivadaSM] = FALSE()
)
```

## Derivación a SM

```DAX
Derivación a SM =
CALCULATE(
    [Atenciones Válidas],
    FactAssistantInteractions[DerivadaSM] = TRUE()
)
```

## % Contención BOT

```DAX
% Contención BOT =
DIVIDE(
    [Atenciones Solo BOT],
    [Atenciones Válidas],
    0
)
```

## Tasa de Abandono

```DAX
Tasa de Abandono =
DIVIDE(
    [Atenciones Abandonadas],
    [Atenciones Totales],
    0
)
```

## Clientes Nuevos

```DAX
Clientes Nuevos =
CALCULATE(
    DISTINCTCOUNT(FactAssistantInteractions[ClienteId]),
    FactAssistantInteractions[TipoCliente] = "Nuevo"
)
```

## Clientes Recurrentes

```DAX
Clientes Recurrentes =
CALCULATE(
    DISTINCTCOUNT(FactAssistantInteractions[ClienteId]),
    FactAssistantInteractions[TipoCliente] = "Recurrente"
)
```

> Nota: los nombres de tablas, campos y reglas han sido simplificados para fines de portafolio. La lógica conserva la intención analítica del proyecto.
