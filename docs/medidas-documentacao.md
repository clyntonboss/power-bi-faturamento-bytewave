# Documentação de Medidas DAX

Este arquivo documenta as medidas utilizadas no modelo Power BI do projeto.

---

## percentual_faturamento_loja

```DAX
VAR _Resultado =
    DIVIDE(
        [faturamento_loja],
        [faturamento_total]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## quantidade_produtos

```DAX
VAR _Resultado =
    DISTINCTCOUNT(
        fVendas[nome_produto]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## cores_maior_menor_produtos_vendidos

```DAX
VAR _MenorProdutosVendidos =
    MINX(
        ALLSELECTED(
            dCalendario[mes_abreviado],
            dCalendario[mes_numero]
        ),
        [produtos_vendidos_total]
    )

VAR _MaiorProdutosVendidos =
    MAXX(
        ALLSELECTED(
            dCalendario[mes_abreviado],
            dCalendario[mes_numero]
        ),
        [produtos_vendidos_total]
    )

RETURN
SWITCH(
    TRUE(),
    [produtos_vendidos_total] = _MaiorProdutosVendidos, "#33CC33",
    [produtos_vendidos_total] = _MenorProdutosVendidos, "#FF0000",
    "#808080"
)
```

---

## maior_menor_produtos_vendidos

```DAX
VAR _MenorProdutosVendidos =
    MINX(
        ALLSELECTED(
            dCalendario[mes_abreviado],
            dCalendario[mes_numero]
        ),
        [produtos_vendidos_total]
    )

VAR _MaiorProdutosVendidos =
    MAXX(
        ALLSELECTED(
            dCalendario[mes_abreviado],
            dCalendario[mes_numero]
        ),
        [produtos_vendidos_total]
    )

VAR _Resultado =
    IF(
        [produtos_vendidos_total]=_MaiorProdutosVendidos||
        [produtos_vendidos_total]=_MenorProdutosVendidos,
        [produtos_vendidos_total]
    )

RETURN
    _Resultado
```

---

## percentual_produtos_vendidos_ecommerce

```DAX
VAR _Resultado =
    DIVIDE(
        [produtos_vendidos_ecommerce],
        [produtos_vendidos_total]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## percentual_produtos_vendidos_loja

```DAX
VAR _Resultado =
    DIVIDE(
        [produtos_vendidos_loja],
        [produtos_vendidos_total]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## produtos_vendidos_ecommerce

```DAX
VAR _Resultado =
    SUM(
        fVendas[unidades_ecommerce]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## produtos_vendidos_loja

```DAX
VAR _Resultado =
    SUM(
        fVendas[unidades_loja]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## produtos_vendidos_total

```DAX
VAR _Resultado =
    [produtos_vendidos_loja]+[produtos_vendidos_ecommerce]

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## ticket_medio

```DAX
VAR _Resultado =
    DIVIDE(
        [faturamento_total],
        [transações]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## titulo_mais_faturados

```DAX
0
```

---

## titulo_mais_transações

```DAX
0
```

---

## transações

```DAX
VAR _Resultado =
    COUNTROWS(
        fVendas
    ) * 2

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---

## quantidade_vendedores

```DAX
VAR _Resultado =
    DISTINCTCOUNT(
        fVendas[nome_vendedor]
    )

RETURN
    COALESCE(
        _Resultado,
        0
    )
```

---
