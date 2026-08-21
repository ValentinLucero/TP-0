# Aplicando lo Aprendido 0 — Paradigmas, lenguajes y programas

Nombre y Apellido: Valentin Lucero

Fecha: 20 de agosto de 2026

Lenguaje elegido: C

---

## Ejercicio 1



### 1. Generalización simbólica: ¿cuáles son las reglas escritas del lenguaje?

Entre las reglas escritas más importantes se encuentran:

- Un conjunto reducido de tipos de datos primitivos (int, char, float, double, void, y sus variantes con calificadores como unsigned, long, short).
- Estructuras de control propias de la programación estructurada: secuencia, selección (if/else, switch) e iteración (for, while, do-while), sin necesidad de GOTO para organizar el flujo (aunque goto sigue existiendo como reliquia del paradigma no estructurado).
- El procedimiento/función como unidad de modularización: todo programa en C se organiza en funciones, con una función main como punto de entrada obligatorio.
- Reglas de ámbito (scope) de variables locales, globales y estáticas, y de tiempo de vida (lifetime) del almacenamiento.
- Un modelo explícito de memoria basado en punteros y gestión manual (malloc, free), sin recolector de basura.
- Un preprocesador independiente del compilador, con directivas propias (#include, #define, #ifdef) que constituyen casi un mini-lenguaje textual previo a la compilación.
- Reglas de compilación separada (archivos .c y .h) y de enlazado (linking) que permiten construir programas grandes a partir de módulos independientes.

### 2. Creencias de los profesionales: ¿Qué características particulares del lenguaje se cree que sean "mejores" que en otros lenguajes?

Dentro de la comunidad de C existen una serie de creencias fuertemente arraigadas:

- Que C ofrece el mejor equilibrio entre control de bajo nivel y legibilidad de alto nivel: permite manipular memoria y bits casi como el ensamblador, pero con una sintaxis mucho más manejable.
- Que su eficiencia en tiempo de ejecución es difícilmente superada por lenguajes con recolector de basura o máquinas virtuales, porque compila directamente a código nativo y no impone overhead de runtime.
- Que su minimalismo (pocas palabras clave, poca "magia" oculta del compilador) es una virtud: "lo que ves es lo que se ejecuta", sin capas de abstracción que oculten el costo real de una operación.
- Que su portabilidad a nivel de código fuente entre arquitecturas y sistemas operativos es excelente, gracias a la estandarización y a la disponibilidad de compiladores en prácticamente cualquier plataforma (desde microcontroladores hasta supercomputadoras).
- En contrapartida, también es una creencia extendida que esa libertad tiene un costo: se considera un lenguaje "peligroso" porque confía plenamente en quien programa (sin verificación de límites de arrays, sin manejo de excepciones nativo), lo que se ve tanto como ventaja (control total) como desventaja (errores de memoria, buffer overflows, undefined behavior).

### 3. Valores: ¿qué pensamiento o estilo de programación consideraron mejor los creadores?

C fue diseñado por Dennis Ritchie (con aportes de Ken Thompson) en los Laboratorios Bell a comienzos de los años 70, con el objetivo original de reescribir el sistema operativo UNIX (hasta entonces en ensamblador) en un lenguaje portable. Los valores que guiaron su diseño fueron:

- Simplicidad y minimalismo: un núcleo de lenguaje pequeño, dejando la mayor parte de la funcionalidad (E/S, manejo de cadenas, matemática) a bibliotecas estándar en lugar de al lenguaje mismo.
- Cercanía al hardware: se valoró que el programador pudiera razonar directamente en términos de memoria, direcciones y representación de datos, siguiendo el modelo de la máquina de Turing/Von Neumann.
- Confianza en quien programa ("trust the programmer"): el lenguaje no impone restricciones de seguridad por defecto; se prioriza la libertad y el control sobre la protección automática.
- Portabilidad: escribir un compilador relativamente simple de adaptar a nuevas arquitecturas, para que el mismo código fuente (o con mínimos cambios) funcionara en máquinas distintas — algo revolucionario frente al ensamblador de la época.
- Eficiencia por sobre la comodidad sintáctica: se prefirió un estilo de programación estructurado e imperativo, cercano a "cómo" se realiza el cálculo (cambios de estado, secuencias de instrucciones) antes que a un estilo declarativo.

En síntesis, el estilo que los creadores consideraron mejor fue el paradigma imperativo estructurado en bloques, con procedimientos como unidad de modularización, priorizando el control explícito del programador sobre el estado de la máquina.

### 4. Ejemplares: ¿Qué clase de problemas pueden resolverse más fácilmente en el lenguaje?

C es el ejemplar por excelencia para problemas que requieren control fino sobre el hardware y máximo rendimiento, entre ellos:

- Sistemas operativos y núcleos (el kernel de Linux, gran parte de UNIX/BSD, Windows en su núcleo).
- Controladores de dispositivo (drivers) y firmware, donde se necesita acceso directo a registros de memoria y periféricos.
- Sistemas embebidos y microcontroladores, con recursos de memoria y procesamiento muy limitados.
- Compiladores e intérpretes de otros lenguajes (por ejemplo, CPython —el intérprete de referencia de Python— está escrito en C).
- Motores de bases de datos y software de infraestructura donde el rendimiento es crítico (por ejemplo, SQLite).
- Software de tiempo real, donde la latencia debe ser predecible y mínima.

---

## Ejercicio 2

### 1. ¿Tiene una sintaxis y una semántica bien definida? ¿Existe documentación oficial?

Sí. C cuenta con una sintaxis y semántica formalmente especificadas en el estándar ISO/IEC 9899, mantenido por el comité WG14, con revisiones periódicas (C89/C90, C99, C11, C17, C23). Cada revisión define de manera precisa la gramática del lenguaje y el comportamiento esperado de cada construcción, incluyendo casos de comportamiento indefinido (undefined behavior), no especificado (unspecified behavior) y definido por la implementación (implementation-defined behavior), lo cual es una particularidad importante de C: no todo está 100% definido de forma unívoca, y eso queda documentado explícitamente. Además del estándar, existe abundante documentación oficial y de referencia (manuales de gcc/clang, la biblioteca estándar documentada en man pages, y el propio libro de K&R como referencia histórica).

### 2. ¿Es posible comprobar el código producido en ese lenguaje?

Es posible, aunque con limitaciones inherentes al diseño del lenguaje. Existen herramientas maduras de comprobación: analizadores estáticos (Clang Static Analyzer, cppcheck), sanitizers en tiempo de ejecución (AddressSanitizer, UndefinedBehaviorSanitizer, Valgrind) y frameworks de pruebas unitarias (Unity, CMocka, Check). Sin embargo, dado que C no verifica límites de arrays ni tiene un sistema de tipos tan estricto como otros lenguajes, demostrar formalmente que un programa es correcto (en el sentido de "probar con certeza matemática") resulta más difícil que en lenguajes con tipado fuerte, inmutabilidad o verificación de memoria en tiempo de compilación. Por eso, en dominios críticos (aviónica, automotriz) se recurre a subconjuntos restringidos y verificables como MISRA-C.

### 3. ¿Es confiable?

Depende fuertemente de la disciplina de quien programa. C no ofrece manejo de excepciones nativo (se recurre a códigos de retorno o a setjmp/longjmp), no tiene recolector de basura (la gestión manual de memoria con malloc/free es una fuente clásica de memory leaks, dangling pointers y buffer overflows), y permite comportamientos indefinidos que pueden causar fallos silenciosos difíciles de depurar. Por diseño, no es "seguro por defecto": prioriza la eficiencia y el control por sobre la protección automática. Dicho esto, cuando se programa siguiendo buenas prácticas, estándares como MISRA-C, y se usan herramientas de análisis, C puede alcanzar niveles de confiabilidad muy altos — de hecho es la base de sistemas críticos como el software de vuelo o el firmware médico.

### 4. ¿Es ortogonal?

Solo parcialmente. C presenta varias combinaciones de características que no son del todo independientes entre sí. Un ejemplo clásico es la relación entre arrays y punteros: un array "decae" (decays) a un puntero a su primer elemento en la mayoría de los contextos, lo que genera casos especiales y confusiones (por ejemplo, sizeof se comporta distinto sobre un array que sobre el puntero al que decae). Otro ejemplo es que las funciones no pueden devolver arrays directamente, o que la sintaxis de punteros a función es notoriamente compleja y poco composicional. Esto contrasta con lenguajes diseñados explícitamente para maximizar la ortogonalidad, donde tipos y funciones son plenamente independientes entre sí.

### 5. ¿Cuáles son sus características de consistencia y uniformidad?

C es razonablemente uniforme en sus reglas básicas: toda sentencia termina en ";", los bloques se delimitan siempre con "{}", y la estructura general de declaración de variables y funciones sigue un patrón consistente (tipo nombre). Sin embargo, existen inconsistencias históricas conocidas: la declaración de arrays multidimensionales, la precedencia de operadores (por ejemplo, entre operadores bit a bit y de comparación, una fuente frecuente de errores), y la ya mencionada sintaxis de punteros a función, que rompe la intuición de "leer la declaración como el uso" en casos anidados.

### 6. ¿Es extensible? ¿Hay subconjuntos de ese lenguaje?

Sí, en ambos sentidos. Es extensible mediante bibliotecas: la biblioteca estándar (stdio.h, stdlib.h, string.h, etc.), extensiones POSIX, y una enorme cantidad de bibliotecas de terceros amplían sus capacidades sin modificar el núcleo del lenguaje. El preprocesador y las macros también funcionan como mecanismo de extensión textual. Además, los compiladores suelen ofrecer extensiones propias (por ejemplo, las extensiones GNU de gcc, o el ensamblador en línea).

En cuanto a subconjuntos, existen varios reconocidos formalmente: las distintas versiones del estándar (C89/C90 como núcleo mínimo histórico, ampliado progresivamente por C99, C11, C17 y C23), variantes orientadas a sistemas embebidos ("Embedded C"), y subconjuntos restringidos por normas de seguridad como MISRA-C, que prohíben ciertas construcciones del lenguaje completo para reducir el riesgo de errores.

### 7. El código producido, ¿es transportable?

En gran medida sí, a nivel de código fuente: un programa escrito siguiendo el estándar ISO puede compilarse en compiladores conformes (gcc, clang, y con matices MSVC) para arquitecturas muy distintas (x86, ARM, RISC-V, microcontroladores de 8 bits) sin reescribir el código. Esto fue, de hecho, uno de los objetivos originales de su diseño. No obstante, la transportabilidad no es absoluta: el tamaño de tipos como int o long, el orden de bytes (endianness), la alineación de memoria y detalles de la ABI (Application Binary Interface) pueden variar entre plataformas, lo cual puede introducir comportamientos distintos si el código no se escribe con cuidado. Para mitigar esto, el propio estándar (desde C99) incorpora stdint.h, con tipos de tamaño fijo (int32_t, uint8_t, etc.) que mejoran la portabilidad real del código.

