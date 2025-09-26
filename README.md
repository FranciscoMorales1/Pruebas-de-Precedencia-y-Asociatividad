

---

# 📘 Proyecto: Calculadora con ANTLR4

Este proyecto implementa una calculadora en **ANTLR4** utilizando el patrón **Visitor**.
Se presentan **dos versiones**:

1. **Normal (Original)** → Usa la precedencia estándar de operadores matemáticos.
2. **Alterado** → Todos los operadores tienen la misma precedencia y se evalúan de izquierda a derecha.

---

## 📂 Estructura de directorios

```
Tarea2/
│
├── Original/
│   ├── Calc.g4              # Gramática ANTLR original (precedencia estándar)
│   ├── Main.java            # Clase principal
│   ├── EvalVisitor.java     # Visitor con precedencia estándar
│   ├── antlr-4.13.2-complete.jar
│   └── Archivos generados por ANTLR (Lexer, Parser, Visitor base…)
│
└── Alterado/
    ├── CalcAlt.g4           # Gramática ANTLR alterada (todos izquierda)
    ├── MainAlt.java         # Clase principal
    ├── EvalAltVisitor.java  # Visitor con precedencia modificada
    ├── antlr-4.13.2-complete.jar
    └── Archivos generados por ANTLR (Lexer, Parser, Visitor base…)
```

---

## ▶️ Cómo ejecutar

1. Abrir una terminal (**PowerShell o CMD**).
2. **Pararse en la carpeta específica** según la versión que se quiera ejecutar:

### En **Original**:

```powershell
java -cp ".;.\antlr-4.13.2-complete.jar" Main
```

### En **Alterado**:

```powershell
java -cp ".;.\antlr-4.13.2-complete.jar" MainAlt
```

3. El programa pedirá expresiones matemáticas, por ejemplo:

```
2 + 3 * 4
2 ^ 3 ^ 2
(2 + 3) * 4
```

Para terminar, se usa **Ctrl+Z y Enter** en Windows.

---

## 📑 Gramáticas

* **Original (`Calc.g4`)**:
  Define la precedencia usual:

  * Potencia (`^`) con asociatividad a la derecha.
  * Multiplicación y división (`*`, `/`).
  * Suma y resta (`+`, `-`).

* **Alterado (`CalcAlt.g4`)**:
  Rediseñada para que **todos los operadores tengan la misma precedencia** y se evalúen **de izquierda a derecha**.

Este rediseño cumple con el enunciado del proyecto:

> "Escriba un programa en ANTLR que tenga una gramática en donde se puedan hacer operaciones matemáticas. [Use visitor].
> Con la gramática original realice pruebas de precedencia y asociatividad.
> Re diseñe la gramática y cambie la precedencia y asociatividad. Realice pruebas.
> Compare los resultados obtenidos. [Use varias cadenas de prueba]."

---

## 🧪 Casos de prueba

Se seleccionaron **6 expresiones**, de las cuales **5 muestran resultados diferentes** entre la calculadora original y la alterada, y **1 resulta igual en ambas**.

| Nº | Expresión     | Original (precedencia estándar) | Alterado (todos izquierda) | Diferencia                                                                                       |
| -- | ------------- | ------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| 1  | `2 + 3 * 4`   | 14                              | 20                         | Diferente: Original hace `3*4=12`, luego `2+12`; Alterado hace `2+3=5`, luego `5*4=20`.          |
| 2  | `2 ^ 3 ^ 2`   | 512                             | 64                         | Diferente: Original evalúa derecha (`2^(3^2)=512`); Alterado evalúa izquierda (`(2^3)^2=64`).    |
| 3  | `2 + 2 ^ 3`   | 10                              | 64                         | Diferente: Original primero potencia (`2^3=8`, luego `2+8=10`); Alterado hace `(2+2)^3=64`.      |
| 4  | `10 - 2 * 3`  | 4                               | 24                         | Diferente: Original multiplica (`2*3=6`, luego `10-6=4`); Alterado hace `(10-2)*3=24`.           |
| 5  | `100 / 5 ^ 2` | 4                               | 400                        | Diferente: Original primero potencia (`5^2=25`, `100/25=4`); Alterado hace `(100/5)^2=20^2=400`. |
| 6  | `8 / 4 / 2`   | 1                               | 1                          | Igual: en ambos casos la división es izquierda: `(8/4)/2=1`.                                     |

---

