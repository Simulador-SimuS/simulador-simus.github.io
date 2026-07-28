# SimuS
## Simulador del Procesador Sapiens
### Manual de Uso

---

## 1. Introducción

SimuS (Simulador Sapiens) es una herramienta educativa desarrollada para simular el funcionamiento del procesador Sapiens. Este simulador permite a los estudiantes escribir, compilar y ejecutar programas en lenguaje assembly, visualizando en tiempo real el comportamiento del procesador, los registros, las flags y la memoria.

SimuS ofrece funciones avanzadas de depuración, incluyendo ejecución paso a paso, puntos de interrupción (breakpoints), visualización de memoria y puertos de entrada/salida simulados.

---

## 2. Interfaz de Usuario

El idioma de la interfaz de usuario puede seleccionarse en portugués, inglés o español haciendo clic en una de las banderas ubicadas en la esquina superior de la ventana principal.

La interfaz de SimuS está dividida en tres paneles principales, cada uno con funciones específicas para facilitar el desarrollo y la depuración de programas. 

### 2.1. Panel Izquierdo - Editor y Ejecución

Este panel contiene tres pestañas que permiten editar código, visualizar errores y realizar el seguimiento de la ejecución:

#### 2.1.1. Pestaña Editor

Área de edición de código assembly con las siguientes características:

- Editor de texto con resaltado de sintaxis (syntax highlighting) para código assembly.
- Fondo oscuro para reducir la fatiga visual durante la programación.
- Fuente monoespaciada (Consolas) para una mejor alineación del código.
- Soporte para comentarios (líneas iniciadas con punto y coma `;`).

#### 2.1.2. Pestaña Errores

Muestra los mensajes de error generados durante la compilación:

- Enumera todos los errores encontrados en el código fuente.
- Cada error muestra la línea y una descripción del problema.
- Haga clic en un error para posicionar el cursor en la línea correspondiente del editor.
- Una etiqueta (badge) roja en el título de la pestaña indica el número de errores encontrados.

#### 2.1.3. Pestaña Ejecución

Visualización del código compilado con funciones de depuración:

- Muestra el código assembly junto con las direcciones de memoria en hexadecimal.
- Resaltado en amarillo en la línea actual de ejecución (PC - Program Counter).
- Las etiquetas (labels) se muestran en color naranja para una fácil identificación.
- Haga clic en cualquier línea para añadir/eliminar un punto de interrupción (breakpoint), marcado en rojo en la dirección.
- Desplazamiento automático para seguir la ejecución del programa.

### 2.2. Panel Central - CPU y Controles

Este panel concentra todos los controles de ejecución y la visualización del estado de la CPU:

#### 2.2.1. Botones de Control

Cinco botones con colores distintos para controlar la ejecución:

- **Paso (Naranja):** Ejecuta una única instrucción y se detiene. Es ideal para una depuración detallada.
- **Ejecutar (Verde):** Ejecuta el programa continuamente a velocidad normal (50 ms por instrucción). Se detiene automáticamente en los breakpoints o al encontrar la instrucción HLT.
- **Turbo (Rosa):** Ejecuta el programa a alta velocidad (1000 instrucciones por ciclo). Es útil para programas largos. También respeta los breakpoints.
- **Detener (Rojo):** Interrumpe la ejecución en cualquier modo (Ejecutar o Turbo).
- **Reset (Negro):** Reinicia el procesador al estado inicial después de un HLT. Restaura el PC, los registros y los puertos de E/S, pero preserva el contenido de la memoria.

#### 2.2.2. Barra de Estado

Muestra el estado actual del simulador en texto gris, debajo de los botones de control. Los mensajes incluyen: *"Listo"*, *"Ejecutando..."*, *"TURBO - Ejecutando..."*, *"HALT - Programa Finalizado"*, entre otros.

#### 2.2.3. Registros

Tres casillas que muestran los valores de los registros principales en hexadecimal:

- **AC (Acumulador):** Registro de 8 bits utilizado para operaciones aritméticas y lógicas (formato: XX).
- **PC (Program Counter):** Registro de 16 bits que apunta a la dirección de la siguiente instrucción (formato: XXXX).
- **SP (Stack Pointer):** Registro de 16 bits que apunta al tope de la pila (formato: XXXX, inicializado en FFFF).

#### 2.2.4. Instrucción Actual

Casilla con fondo oscuro que muestra el mnemónico de la instrucción a la que apunta actualmente el PC. Ejemplo: `LDA #0xFF`. Esta visualización con resaltado amarillo dorado facilita el seguimiento de la ejecución.

#### 2.2.5. Flags (Señaladores)

Tres indicadores visuales que muestran el estado de los flags del procesador:

- **N (Negativo):** Se enciende en azul cuando el resultado de la última operación es negativo (bit 7 = 1).
- **Z (Cero):** Se enciende en azul cuando el resultado de la última operación es cero.
- **C (Acarreo / Carry):** Se enciende en azul cuando hay un desbordamiento/acarreo en la última operación aritmética.

#### 2.2.6. Puertos de Entrada/Salida

Interfaz simulada de periféricos con cuatro componentes:

- **Banner - Texto:** Pantalla de texto ancha que muestra caracteres ASCII enviados por la instrucción OUT 3. Soporta múltiples líneas y texto bidireccional. Ejemplo: *"Sapiens 2.0"*.
- **Entrada (IN) - Hex/Bin:** Campo de texto donde el usuario escribe valores hexadecimales (00-FF) o binarios (8 bits) que serán leídos por la instrucción IN 0. Presione ENTER después de escribir para confirmar el valor. Un LED verde se enciende cuando hay datos disponibles.
- **Salida (OUT) - Hex/Bin:** Pantalla hexadecimal/binaria que muestra el último valor enviado por la instrucción OUT 0. Formato: XX o XXXXXXXX.
- **LED de Estado:** Indicador verde que se enciende cuando hay un dato escrito y confirmado en la entrada, disponible para su lectura a través de IN 1 (puerto de estado).

### 2.3. Panel Derecho - Visualización de la Memoria

Muestra el contenido de la memoria RAM en formato hexadecimal con navegación:

#### 2.3.1. Barra de Navegación

Controles en la parte superior del panel de memoria:

- **Botón ‹ (Anterior):** Retrocede 256 bytes (32 líneas) en la visualización.
- **Campo de Dirección:** Casilla de texto central que muestra la dirección inicial de la visualización en hexadecimal (formato: XXXX). Puede escribir una dirección y presionar ENTER para navegar directamente.
- **Botón › (Siguiente):** Avanza 256 bytes (32 líneas) en la visualización.
- **Botón < (Anterior):** Recula 256 bytes (32 líneas) en la visualización.
- **Botón PC:** Navega automáticamente a la dirección actual del Program Counter, centrando la visualización en la instrucción que se está ejecutando.
- **Botón SP:** Navega automáticamente a la dirección actual del Stack Pointer, centrando la visualización en la pila del programa.

#### 2.3.2. Cuadrícula de Memoria

Visualización en una cuadrícula hexadecimal con las siguientes características:

- Muestra 32 líneas de 8 bytes cada una (256 bytes totales por pantalla).
- La columna de la izquierda muestra la dirección base de cada línea en hexadecimal.
- El encabezado superior indica el desplazamiento (+0 a +7) para cada columna.
- Los bytes con valor 00 se muestran en gris claro para facilitar su identificación.
- El byte apuntado por el PC está resaltado con fondo amarillo.
- El byte apuntado por el SP está resaltado con fondo lila.
- La fuente monoespaciada garantiza una alineación perfecta de los valores.

---

## 3. Barra de Herramientas de Archivo

Ubicada en la parte superior del panel izquierdo, ofrece botones para la gestión de archivos y ventanas auxiliares:

- **📂 Abrir:** Abre un archivo assembly desde el disco (.txt, .asm, .sap). El contenido se carga en el editor, reemplazando el código actual. El nombre del archivo se muestra en la pestaña del Editor.
- **💾 Guardar Como...:** Guarda el código actual del editor en un archivo en el disco. Abre el diálogo del navegador para elegir el nombre y la ubicación. Extensión por defecto: .asm.
- **✔ Compilar:** Compila el código assembly en el editor. Si hay errores, la pestaña Errores se activa automáticamente con la lista de problemas. Si la compilación es exitosa, el código compilado se carga en la memoria y se muestra la pestaña Ejecución. El PC se posiciona en la dirección definida por la directiva ORG.
- **Terminal:** Muestra u oculta la ventana emergente de la consola de texto. La ventana se puede mover arrastrando su barra de título.
- **Video:** Muestra u oculta la ventana emergente del display gráfico virtual. Esta ventana también se puede mover arrastrando su barra de título.

### 3.1. Ventanas Emergentes

Las ventanas Terminal y Video son ventanas flotantes independientes. Para reposicionarlas, haga clic y arrastre la barra superior de la ventana. El botón circular rojo de la barra de título cierra/oculta la ventana.

---

## 4. Flujo de Trabajo Típico

Siga estos pasos para desarrollar y ejecutar programas en SimuS:

1. **Editar el Código:** En la pestaña Editor, escriba su programa en assembly. Use comentarios (;) para documentar el código. Recuerde incluir la directiva ORG para definir la dirección inicial y END para marcar el fin del programa.
2. **Compilar:** Haga clic en el botón ✔ Compilar. Si hay errores, corríjalos como se indica en la pestaña Errores y compile de nuevo.
3. **Definir Breakpoints (Opcional):** En la pestaña Ejecución, haga clic en las líneas donde desea pausar la ejecución. Aparecerá un círculo rojo en la dirección.
4. **Ejecutar:** Elija un modo de ejecución:
   - Paso: Para una depuración detallada, instrucción por instrucción.
   - Ejecutar: Para una velocidad normal con visualización.
   - Turbo: Para programas largos, ejecución a máxima velocidad.
5. **Seguir la Ejecución:** Observe cómo los registros, flags, memoria y puertos de E/S se actualización en tiempo real. La línea actual se resalta en amarillo en la pestaña Ejecución.
6. **Interactuar con la E/S:** Cuando el programa ejecute IN 0, escriba un valor hexadecimal en el campo Entrada (Hex) y presione ENTER. Los valores enviados a través de OUT se muestran automáticamente.
7. **Finalizar:** El programa se detiene automáticamente al encontrar HLT. Use el botón Reset para reiniciar y ejecutar nuevamente.
8. **Guardar:** Use 💾 Guardar Como... para guardar su trabajo en un archivo.

---

## 5. Conjunto de Instrucciones Sapiens

El procesador Sapiens implementa las siguientes categorías de instrucciones:

### 5.1. Instrucciones de Transferencia de Datos

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| LDA | Load Accumulator | Carga el AC con un valor de la memoria o inmediato |
| STA | Store Accumulator | Almacena el AC en la memoria |
| LDS | Load Stack Pointer | Carga el SP con un valor de 16 bits |
| STS | Store Stack Pointer | Almacena el SP en la memoria (16 bits) |

### 5.2. Instrucciones Aritméticas

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| ADD | Addition | AC = AC + operando (actualiza flags) |
| ADC | Add with Carry | AC = AC + operando + C (actualiza flags) |
| SUB | Subtraction | AC = AC - operando (actualiza flags) |
| SBC | Subtract with Carry | AC = AC - operando - C (actualiza flags) |

### 5.3. Instrucciones Lógicas

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| AND | Logical AND | AC = AC & operando (actualiza flags) |
| OR | Logical OR | AC = AC \| operando (actualiza flags) |
| XOR | Exclusive OR | AC = AC ^ operando (actualiza flags) |
| NOT | Logical NOT | AC = ~AC (actualiza flags) |

### 5.4. Instrucciones de Desplazamiento

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| SHL | Shift Left | Desplaza el AC 1 bit a la izquierda (bit 0 = 0, C recibe el bit 7) |
| SHR | Shift Right | Desplaza el AC 1 bit a la derecha lógico (bit 7 = 0, C recibe el bit 0) |
| SRA | Shift Right Arithmetic | Desplaza el AC 1 bit a la derecha aritmético (mantiene el bit 7) |

### 5.5. Instrucciones de Control de Flujo

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| JMP | Jump | Salta incondicionalmente a una dirección |
| JZ | Jump if Zero | Salta si el flag Z = 1 |
| JNZ | Jump if Not Zero | Salta si el flag Z = 0 |
| JN | Jump if Negative | Salta si el flag N = 1 |
| JP | Jump if Positive | Salta si el flag N = 0 |
| JC | Jump if Carry | Salta si el flag C = 1 |
| JNC | Jump if No Carry | Salta si el flag C = 0 |

### 5.6. Instrucciones de Subrutina

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| JSR | Jump to Subroutine | Guarda el PC en la pila y salta a la subrutina |
| RET | Return | Retorna de la subrutina (recupera el PC de la pila) |

### 5.7. Instrucciones de Pila

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| PUSH | Push to Stack | Empuja el AC en la pila (mem[SP] = AC, luego SP--) |
| POP | Pop from Stack | Saca de la pila hacia el AC (SP++, luego AC = mem[SP]) |

### 5.8. Instrucciones de Entrada/Salida

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| IN | Input | Lee datos de la puerta especificada hacia el AC |
| OUT | Output | Envía el AC a la puerta especificada |

#### Puertos de E/S Disponibles:

| Instrucción | Función |
|-----------|--------|
| IN 0 | Lee el valor hexadecimal escrito por el usuario |
| IN 1 | Lee el estado de la entrada (1 = dato disponible, 0 = sin dato) |
| OUT 0 | Envía el AC a la pantalla hexadecimal de salida |
| OUT 2 | Limpia el banner de texto |
| OUT 3 | Envía un carácter ASCII al banner de texto (lo añade al final) |

### 5.9. Instrucciones Especiales

| Mnemónico | Nombre | Descripción |
|-----------|------|-----------|
| NOP | No Operation | No hace nada (puede usarse para temporización) |
| HLT | Halt | Detiene la ejecución del procesador |
| TRAP | Trap | Genera una llamada de servicio |

#### Operaciones de TRAP Disponibles:

- El número del TRAP se pasa en el acumulador. Los parámetros adicionales se pasan en la dirección de memoria del operando.
- La instrucción `TRAP` devuelve códigos de resultado en el acumulador, pero no actualiza los flags. Antes de probar el retorno con `JZ` o `JNZ`, use una instrucción que actualice los flags sin cambiar el valor, como `OR #0`:

```asm
LDA #20
TRAP VIDEO_CONFIG
OR #0
JNZ ERROR
```

| Instrucción | Función |
|-----------|--------|
| #0 | Limpia la terminal de la consola |
| #1 | Lee un carácter de la terminal y lo guarda en el acumulador y en la dirección de memoria del operando |
| #2 | Escribe un carácter desde la dirección de memoria del operando en la terminal |
| #3 | Lee una cadena de la terminal y la guarda en la dirección de memoria del operando |
| #4 | Escribe una cadena a partir de la dirección del operando (hasta encontrar un NULL) |
| #5 | Delay (Espera de 0 a 65535 ms) |
| #6 | Beep (Sintetizador de Audio). Recibe frecuencia y duración como parámetros |
| #7 | Devuelve un número pseudoaleatorio entre 0 y 99 en el acumulador |
| #20 | Configura el display gráfico virtual. El operando apunta a un bloque `DW base`, donde `base` es el inicio de la memoria de video. |
| #21 | Limpia la memoria de video con un color. El operando apunta a `DB color`. |
| #22 | Dibuja un pixel. El operando apunta a `DB x, y, color`. |
| #23 | Dibuja una línea. El operando apunta a `DB x0, y0, x1, y1, color`. |
| #24 | Dibuja un rectángulo. El operando apunta a `DB x, y, ancho, alto, color, relleno`. |
| #25 | Dibuja un círculo. El operando apunta a `DB cx, cy, radio, color, relleno`. |

#### Display Gráfico Virtual

El display gráfico virtual tiene resolución de 128 × 64 pixels. La memoria de video ocupa 8192 bytes consecutivos, con 1 byte por pixel. La `TRAP #20` define qué región de la memoria de 64 KB se usará como buffer. La dirección base debe estar alineada a un múltiplo de 256, y el área `base + 8192` no puede superar el límite de la memoria.

La distribución de los pixels es lineal:

```text
dirección = base + (y * 128) + x
```

Los colores usan el formato de 8 bits `RRRGGGBB`:

| Valor | Color aproximado |
|-------|------------------|
| `224` / `0xE0` | Rojo |
| `28` / `0x1C` | Verde |
| `3` / `0x03` | Azul |
| `252` / `0xFC` | Amarillo |
| `255` / `0xFF` | Blanco |

Valores principales de retorno de la `TRAP #20`:

| AC | Significado |
|----|-------------|
| 0 | Éxito |
| 1 | La dirección base no está alineada a 256 bytes |
| 2 | El área de video supera el límite de la memoria |
| 4 | Usado por las TRAPs gráficas cuando el video aún no fue configurado |

---

## 6. Modos de Direccionamiento

El Sapiens soporta cuatro modos de direccionamiento, identificados por los 2 bits más significativos del opcode:

| Bits | Modo | Ejemplo | Operación | Descripción |
|------|------|---------|----------|-----------|
| 00 | Directo | `LDA 50` | `AC = mem[50]` | El operando es la dirección en memoria del dato |
| 01 | Indirecto | `LDA @50` | `AC = mem[mem[50]]` | El operando apunta a la dirección que contiene la dirección final del dato |
| 10 | Inmediato 8 bits | `LDA #10` | `AC = 10` | El operando es el byte siguiente a la instrucción |
| 11 | Inmediato 16 bits| `LDS #1000` | `SP = 1000` | El operando son los dos bytes siguientes a la instrucción |

### Observaciones sobre Direccionamiento:

- Las instrucciones sin operando (NOP, RET, PUSH, POP, etc.) ignoran el modo de direccionamiento.
- El Modo Indexado no está completamente implementado; utilícelo con precaución.
- El prefijo `@` indica indirecto, `#` indica inmediato y la ausencia indica directo.

---

## 7. Formato de los Operandos

El Sapiens soporta varios tipos de formatos para los operandos de las instrucciones:

- Decimal: 10 - El número sin decoradores.
- Binario: 0b01010101 o 01010101B.
- Hexadecimal: 0x05 o 05H (debe comenzar con un dígito).

---

## 8. Directivas del Ensamblador

El ensamblador de SimuS reconoce las siguientes directivas:

| Directiva | Descripción | Ejemplo | Efecto |
|----------|-------------|---------|--------|
| `ORG dirección` | Define la dirección inicial del programa | `ORG 0` | El programa se inicia en la dirección 0 |
| `END` | Marca el fin del código fuente | `END` | Última línea del archivo |
| `DB valor[, valor...]` | Define uno o más bytes (8 bits) | `DB 0xFF, 10, 1010B` | Almacena la lista de bytes en la memoria |
| `DW valor[, valor...]` | Define una o más palabras / words (16 bits) | `DW 0x1234, 1000` | Almacena words en formato little-endian |
| `DS cantidad` | Define espacio (reserva bytes) | `DS 10` | Reserva 10 bytes en cero |
| `LABEL EQU valor` | Define una constante | `TESTE EQU 10` | TESTE será igual a 10 |

> **Atención:** para constantes, use `LABEL EQU valor` sin dos puntos. La forma `LABEL: EQU valor` crea primero una etiqueta en la dirección actual y puede no definir la constante como se espera.
>

### Uso de Etiquetas (Labels):

Las etiquetas se pueden definir antes de cualquier instrucción o directiva, terminando con dos puntos:

```assembly
LOOP:
    LDA VALOR
    JNZ LOOP

```

* Las etiquetas deben comenzar con una letra y pueden contener letras, números y guion bajo (_).
* El montador las convierte automáticamente a mayúsculas.
* Se pueden usar como operandos en instrucciones de salto y acceso a la memoria.
* Se puede usar `ETIQUETA+desplazamiento` para acceder a los bytes siguientes a una etiqueta. El rango de desplazamiento aceptado actualmente es de 1 a 8. Por ejemplo, si `PALABRA: DW 0x1234`, entonces `PALABRA` apunta al byte bajo (`0x34`) y `PALABRA+1` apunta al byte alto (`0x12`).

---

## 9. Ejemplos de Programas

### 9.1. Eco Simple

Programa que espera la entrada del usuario y devuelve el valor:

```assembly
; Programa de Eco
ORG 0
LOOP:
    IN 1          ; Lee el estado
    JZ LOOP       ; Espera el dato
    IN 0          ; Lee el valor
    OUT 0         ; Muestra el valor
    HLT
END

```

### 9.2. Contador de 0 a 9

Cuenta de 0 a 9 y se detiene:

```assembly
; Contador
ORG 0
    LDA #0        ; Inicia en 0
LOOP:
    OUT 0         ; Muestra el valor
    ADD #1        ; Incrementa
    SUB #10       ; Compara con 10
    JNZ LOOP      ; Continúa si != 10
    HLT
END

```

### 9.3. Subrutina con Pila

Demuestra el uso de JSR, RET y PUSH/POP:

```assembly
; Subrutina
ORG 0
    LDA #42
    JSR SALVAR    ; Llama a la subrutina
    OUT 0         ; Muestra el resultado
    HLT

SALVAR:
    PUSH          ; Guarda el AC
    LDA #99
    OUT 0         ; Muestra 99
    POP           ; Restaura el AC (42)
    RET
END

```

---

### 9.4. Display Gráfico Virtual

Configura la memoria de video en `0x4000`, limpia la pantalla, dibuja un rectángulo relleno, una línea y un círculo:

```assembly
ORG 0

MAIN:
    LDA #20
    TRAP VIDEO_CONFIG
    OR #0
    JNZ ERROR

    LDA #21
    TRAP LIMPIAR

    LDA #24
    TRAP RECTANGULO

    LDA #23
    TRAP LINEA

    LDA #25
    TRAP CIRCULO

    HLT

ERROR:
    HLT

VIDEO_CONFIG:
    DW VIDEO_BASE

LIMPIAR:
    DB 3              ; azul

RECTANGULO:
    DB 48, 16, 32, 32, 224, 1

LINEA:
    DB 0, 63, 127, 0, 28

CIRCULO:
    DB 64, 32, 18, 252, 0

VIDEO_BASE EQU 16384 ; 0x4000

END MAIN
```

---

## 10. Resolución de Problemas Comunes

### Error: "Instrucción Inválida"

* Verifique si el mnemónico está escrito correctamente. Recuerde que el ensamblador no diferencia entre mayúsculas y minúsculas.

### Error: "Etiqueta No Definida"

* Asegúrese de que la etiqueta utilizada en la instrucción se haya definido en alguna parte del código con dos puntos (:).

### El programa no se ejecuta después de compilar

* Verifique si hizo clic en Compilar antes de intentar ejecutar. La luz verde de estado debe mostrar "Cargado" en el mensaje.

### El Breakpoint no funciona

* Los puntos de interrupción solo funcionan en líneas con instrucciones ejecutables. Las líneas vacías, los comentarios y las directivas no pueden tener breakpoints.

### La memoria no se actualiza durante la ejecución

* En el modo Turbo, la interfaz no se cambia en cada instrucción para mantener la velocidad máxima. Use el modo Ejecutar o Paso para ver los cambios en tiempo real.

### IN no lee el valor escrito

* Recuerde presionar ENTER después de escribir el valor hexadecimal. El LED verde debe encenderse indicando que el dato está listo.

### El display gráfico no muestra el dibujo

* Verifique que el programa haya ejecutado `TRAP #20` antes de las demás TRAPs gráficas.
* Después de `TRAP #20`, use `OR #0` o `SUB #0` antes de `JZ/JNZ` para probar correctamente el valor devuelto en AC.
* La base de la memoria de video debe ser múltiplo de 256. Un valor recomendado es `0x4000` (`16384`).
* Use `VIDEO_BASE EQU 16384` sin dos puntos para definir la constante.
* Haga clic en el botón **Video** si la ventana no está visible.

---

## 11. Consejos y Buenas Prácticas

* **Use comentarios generosamente:** Documente el propósito de cada sección del código con líneas iniciadas por punto y coma (;).
* **Organice con etiquetas:** Use nombres descriptivos para las etiquetas (LOOP, INICIO, FIM, CALCULAR, etc.) para que el código sea más legible.
* **Pruebe de forma incremental:** Compile y pruebe pequeñas partes del programa antes de añadir más funcionalidades.
* **Use breakpoints estratégicamente:** Coloque puntos de interrupción en lugares críticos (inicio de bucles, llamadas a subrutinas, decisiones) para facilitar la depuración.
* **Monitoree los flags:** Observe N, Z y C durante la ejecución para entender cómo las operaciones afectan el estado del procesador.
* **Siempre termine con HLT:** Garantice que todo camino de ejecución termine con HLT para evitar comportamientos impredecibles.
* **Guarde su trabajo frecuentemente:** Use el botón 💾 Guardar Como... regularmente para no perder el progreso.
* **Verifique la pestaña Memoria:** Durante la depuración, use el botón PC para navegar rápidamente hasta la instrucción actual en la vista de memoria.

---

## 12. Conclusión

SimuS es una herramienta completa para el aprendizaje de arquitectura de computadores y programación en assembly. A través de su interfaz intuitiva y funciones avanzadas de depuración, los estudiantes pueden experimentar conceptos fundamentales como:

* Ciclo de búsqueda-decodificación-ejecución.
* Funcionamiento de registros y flags.
* Organización de la memoria.
* Pila y llamadas a subrutinas.
* Entrada y salida de datos.
* Diferentes modos de direccionamiento.

Este manual cubre los aspectos esenciales del simulador. Para preguntas adicionales o soporte técnico, consulte la documentación del procesador Sapiens o póngase en contacto con el desarrollador.

**¡Buenos estudios y buena programación!**
