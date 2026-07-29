# critical-edition

**`critical-edition.sty`** es un paquete simple y "minimalista" para componer ediciones críticas en LaTeX, desarrollado a través de prompts y programación asistida por IA. Provee a los usuarios de cuatro tipos de **footnotes** (`\footT`, testimonios; `\footA`, aparato crítico o de variantes; `\footE`, explicaciones; y `footC`, comentarios/adiciones) y un **entorno numerado**.

## Lista de macros

### 1) Estructura y entornos de texto numerado

**`\bnum` ... `\enum`**  
  Entorno/llave global que abre y cierra un bloque de edición numerada. Reinicia internamente los contadores de líneas y notas al comenzar una nueva sección.

**`\nstart` ... `\nend`**  
  Abre y cierra un bloque de texto numerado a ancho completo de caja (`\textwidth`). Sirve para usarse mayormente en textos en **prosa**.

**`\postart` ... `\poend`**  
  Abre y cierra un bloque numerado para textos poéticos, con centrado parcial respecto a la página. Opcionalmente acepta un parámetro de ancho (ej. `\postart[0.90\textwidth]`). Por defecto usa un dimensionador `\pwidth=0.65\textwidth`, que se puede modificar en el preámbulo del archivo `.tex` con `\setlength{\pwidth}{Nº\textwidth}`.

---

### 2) Contro de Numeración de Líneas y Márgenes

**`\linenummargin{left|right|inner|outer}`**  
  Define la posición marginal de los números de línea. Opciones disponibles: `left` (izquierda), `right` (derecha), `inner` (margen interior) u `outer` (margen exterior).

**`\nummarginsep{distancia izquierda}{distancia derecha}`**
  Ajusta la distancia/separación entre la numeración del margen y el bloque de texto (ej. `\nummarginsep{10pt}{-40pt}`). Si una de las variables queda sin contenido, por defecto usará la definida en el paquete, que es 6pt en ambos lados.

**`\setotherline{Nº}`**
  Ajusta manualmente el contador de líneas para que la siguiente línea inicie en la cifra indicada. Sirve para marcar lagunas o saltos de fragmentos.

**`\printlinenum{Nº}`**
  Fuerza la impresión marginal de una línea específica aunque no corresponda a la frecuencia regular (múltiplos de 5), pero no condiciona a que las siguientes continúen irregularmente si se utiliza nuevamente `\setotherline{}`.

---

### 3) Pies de página

**`\footT{Texto}`**  
  Registra una entrada en la **footnoteT**, cuya función es referenciar manuscritos, pasajes paralelos o testimonios.
  
**`\footA[ad=Nº]{texto|lemma\lemma{}}{variante}`**  
  Registra una entrada en la **footnoteA**, que corresponde al *apparatus criticus* con las variantes. Esta footnote depende exclusivamente del entorno numerado.
  **Lema alternativo:** Se puede usar `\lemma{texto_lema}` dentro de la llave para fijar un *lemma* distinto al texto. **Aclaración →** por defecto, el texto encerrado en la primera llave de `\footA{}` se copia en el aparato de variantes tal cual figura.
  **Rango de líneas:** Admite el parámetro opcional `[ad=línea]` cuando una variante abarca múltiples líneas, por ejemplo: si la línea desde la que se referencia es la 140, pero precisa un apunte hasta la 190, entonces → `\footA[ad=190]{lema}{variante}` indicaría que desde la línea 140 hasta la 190 hay un apunte. Además, no fuerza la presencia del `\samelineseparatorA` si se añadiera otra referencia a la línea 140.

**`\footE{Texto}`**  
  Registra una entrada en la **footnoteE** para explicaciones y otros usos generales. La `\footE` en este paquete tiene la función corriente de la clásica `\footnote`.
  
**`\footC{Texto}`**
  Registra una entrada en la **footnote**, cuya función es introducir explicaciones detalladas que, según la edición, suelen figurar tras cada capítulo/parte o luego del propio libro, previo al *Apéndice*. A diferencia del resto de footnotes, esta en particular debe ser impresa manualmente durante la compilación tras recoger las entradas, y para hacerlo se debe utilizar el comando `\printfootC` para volcar las entradas donde se prefiera.

---

### 4- Modificación de la apariencia del cuerpo de footnotes

**`\foottype[T|E|C]{quad|block}`**  
  Configura la disposición visual de las footnotes T, E o C:
  `block`: Imprime cada footnote como un párrafo independiente (por defecto).
  `quad`: Empaqueta todas las footnotes en un único párrafo horizontal.

**`\footindent[T|A|E|C]{par|none}`**  
  Activa (`par`) o desactiva (`none`) la sangría de párrafo en el aparato seleccionado. Por defecto está en `par`.

**`\footAmark{}`**  
  Controla la apariencia del número/rango de línea en la `\footA` (por defecto: `\textbf{#1}`).

**`\footTmark{}` / `\footEmark{<texto>}`**  
  Controlan el formato del número en el pie de página para las entradas T y E (por defecto: `\textsuperscript{#1}`).

**`\footTcall{}` / `\footEcall{}`**  
  Controlan el formato de la llamada o número referencial en el cuerpo del texto para las entradas T y E (por defecto: `\textsuperscript{#1}`).
  
**`\footCcall{}` / `\footCmark`**
  Controlan el formato de la llamada o número referencial en el cuerpo del texto para la entrada C y el formato del número en el pie de página, respectivamente. Por defecto, para diferenciarse en el cuerpo del texto de las `\footT` y `\footE`, ambas macros están definidas como `\textsuperscript{#1)}`, siendo `)` el diferenciador en ambos casos.

**`\samelineseparatorA`**  
  Define el símbolo separador entre variantes que pertenecen a la misma línea en el aparato crítico, que por defecto es: `\char"02016` (si la tipografía utilizada no contiene el caracter y no hay intenciones de añadirlo, puede modificarse este símbolo separador en el preámbulo con `\renewcommand{\samelineseparatorA}{**nuevo símbolo**}`.

**`\lemmaseparatorA`**  
  Define el símbolo separador entre el lema y la variante en el aparato de variantes. Por defecto es `]` (se puede modificar con `\renewcommand{\lemmaseparatorA}{**nuevo símbolo**}`.

---

### 5) Edición de fragmentos o antologías (`critgroup`)

**`\begin{critgroup}` ... `\end{critgroup}`**  
  Entorno para la edición de fragmentos o textos de antologías (ej. Safo, Píndaro, Presocráticos, etc.), cuya función es aislar el contador y producir un cuerpo de footnotes propio impreso inmediatamente debajo del fragmento.

**`\grouplinenummargin{left|right|inner|outer}`**  
  Establece la ubicación del margen de numeración exclusivamente dentro del entorno `critgroup`.

**`\groupnummarginsep{distancia izquierda}{distancia derecha}`**  
  Ajusta la separación del margen de numeración exclusivamente dentro del entorno `critgroup`.


#### Este paquete está bajo la licencia → **The LaTeX Project Public License**.
