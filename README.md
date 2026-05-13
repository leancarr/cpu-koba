# 🟦 CPU Emulator

**CPU** es un emulador funcional de una CPU personalizada de 16 bits basada en una arquitectura RISC simplificada. El proyecto incluye una arquitectura completa, un ensamblador de dos pasadas y un depurador interactivo visual para terminal.

## 🚀 Estado Actual
El proyecto se encuentra en una fase **completamente funcional** con las siguientes características:

*   **Arquitectura Harvard:** Separación estricta entre memoria de programa y datos.
*   **Registros:** 16 registros de propósito general (R0 a R15).
*   **Memoria:** 4096 palabras para programa y 65,536 palabras para datos.
*   **Depurador TUI:** Interfaz visual en tiempo real con colores ANSI que muestra el estado de registros, flags (Z, N, C, V) y volcado de memoria.
*   **Ensamblador:** Soporta etiquetas (labels), comentarios, valores hexadecimales y cálculo de saltos relativos.

---

## 🛠️ Cómo Probarlo

### 1. Compilación
Necesitas `gcc` y `make`. Ejecuta:
```bash
make
```

### 2. Ejecutar un programa
Puedes usar los ejemplos incluidos en la carpeta `programs/`:
```bash
./kobarius programs/loop.asm
```

### 3. Comandos del Emulador
Una vez dentro, interactúa con la CPU:
*   `[Enter]`: Siguiente instrucción (Paso a paso).
*   `run`: Ejecuta el programa hasta el final (`HALT`).
*   `m <dir>`: Inspecciona una dirección de memoria.
*   `r`: Reinicia la ejecución.
*   `q`: Sale del programa.

---

## 📜 Set de Instrucciones (ISA)

La CPU entiende actualmente 8 tipos de instrucciones:

| Mnemónico | Descripción | Tipo |
| :--- | :--- | :--- |
| `LOAD Rd, #imm8` | Carga un valor de 8 bits en un registro | L-type |
| `ADD Rd, Rs1, Rs2` | Suma dos registros | R-type |
| `ADDI Rd, Rs, #imm4`| Suma un valor inmediato de 4 bits | I-type |
| `LW Rd, imm4(Rs)` | Carga una palabra de memoria de datos | I-type |
| `SW Rs, imm4(Rb)` | Guarda una palabra en memoria de datos | I-type |
| `BEQ Rs1, Rs2, lbl` | Salta a la etiqueta si Rs1 == Rs2 | I-type |
| `J label` | Salto incondicional a una dirección | J-type |
| `HALT` | Detiene la ejecución de la CPU | J-type |

---

## 📂 Estructura del Proyecto
*   `cpu.c / .h`: Lógica del ciclo de ejecución y definición de hardware.
*   `assembler.c / .h`: Motor de ensamblado de código fuente `.asm`.
*   `display.c / .h`: Interfaz visual y desensamblador.
*   `main.c`: Punto de entrada y bucle interactivo (REPL).
*   `programs/`: Código de ejemplo para pruebas.