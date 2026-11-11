# UNIVERSIDAD DE CALDAS
## Módulo: Programación Creativa II
### PARCIAL UNIDAD 2: Herencia y Polimorfismo
**Docente:** Andrés Felipe Osorio Quintero  

---

## SECCIÓN I. SELECCIÓN MÚLTIPLE

1. **B. Crear una superclase Enemigo con lo común y hacer que ambas la extiendan, dejando en cada una solo lo específico.**
   * *Justificación:* Aplica el principio de reutilización mediante una relación "es un".

2. **C. Una Onda es un Elemento visual que comparte posición y ciclo de vida con los demás tipos de elemento.**
   * *Justificación:* Representa una relación genuina de herencia ("es un tipo de elemento visual"). Las demás opciones expresan composición/agregación (relación "tiene un").

3. **D. Se lanza un ReferenceError, porque `this` se usa antes de que `super(...)` haya creado el objeto.**
   * *Justificación:* En subclases de JavaScript, `this` no está inicializado ni disponible en el constructor hasta que `super()` es ejecutado.

4. **A. JavaScript genera un constructor que llama a `super(...)` con los mismos argumentos, y `x`, `y` y `color` quedan inicializados.**
   * *Justificación:* Si una subclase no define `constructor`, JS crea uno por defecto implícito: `constructor(...args) { super(...args); }`.

5. **B. Amplía el comportamiento heredado: reutiliza el texto de Forma y le añade el dato propio del cuadrado.**
   * *Justificación:* Al invocar `super.describir()`, mantiene la lógica de la clase base y la complementa.

6. **C. Composición: el robot contiene un objeto por cada capacidad y puede cambiarlos cuando sea necesario.**
   * *Justificación:* Favorece la flexibilidad en tiempo de ejecución ("tiene un") frente a una explosión de clases por herencia rígida.

7. **A. Cada objeto responde a la misma llamada con su propia versión de `mostrar()`, sin que el ciclo conozca su clase.**
   * *Justificación:* Definición directa del comportamiento polimórfico.

8. **D. Nada: el bucle sigue funcionando, porque el polimorfismo permite incorporar nuevos tipos sin tocar el código existente.**
   * *Justificación:* Cumple con el principio *Open/Closed* (Abierto a extensión, cerrado a modificación).

9. **B. Evita el polimorfismo con condicionales: cada nuevo tipo obliga a modificar el bucle en lugar de definir su propio método.**
   * *Justificación:* El uso excesivo de `instanceof` acopla el código a clases concretas y rompe la ventaja del polimorfismo.

10. **C. Impedir que la clase se instancie directamente, simulando el carácter abstracto que JavaScript no ofrece de forma nativa.**
    * *Justificación:* `if (new.target === Clase) throw new Error(...)` previene la instanciación directa de una superclase en JS.

11. **A. Se lanza el error `Linea debe implementar area()`, porque `describir()` invoca la versión abstracta de `area()`.**
    * *Justificación:* Al llamar a `.describir()`, este método invoca `this.area()`. Como `Linea` no lo sobrescribió, se ejecuta la versión abstracta heredada que lanza la excepción.

12. **D. `Rectangulo (ámbar): área 360.0`, porque el método concreto usa el `area()` de la subclase del objeto.**
    * *Justificación:* `this.constructor.name` da `"Rectangulo"`, `this.color` es `"ámbar"` y `this.area()` resuelve dinámicamente $30 \times 12 = 360$.

13. **B. Una clase puede cumplir varias interfaces, pero solo puede heredar de una superclase, sea abstracta o no.**
    * *Justificación:* La herencia simple limita a una sola clase base, mientras que se pueden implementar/cumplir múltiples contratos (interfaces).

14. **C. `true`, porque la tipificación estructural solo exige tener los métodos del contrato, sin importar la jerarquía.**
    * *Justificación:* JS usa tipificación estructural (*duck typing*): si cumple con tener la estructura requerida (métodos), es válido sin importar su árbol de herencia.

15. **D. `random(TIPOS)` devuelve una clase al azar y `new Tipo(...)` crea una instancia de esa clase en la posición del clic.**
    * *Justificación:* En JavaScript las clases son funciones/objetos de primera clase que pueden almacenarse en arreglos e instanciarse dinámicamente con `new`.

16. **A. Para eliminar un elemento sin alterar los índices de los que aún faltan por recorrer, evitando que se salte alguno.**
    * *Justificación:* Al eliminar elementos con `splice()` mientras se itera de $0$ a $N$, el reíndice de los elementos causa que el elemento contiguo sea omitido. Iterar en orden inverso evita este problema.

17. **C. El anillo se desvanece al bajar vida (canal alfa) y, cuando `vida <= 0`, el ciclo `draw()` puede eliminarlo del arreglo.**
    * *Justificación:* Vincula la renderización del canal alfa a `vida` y su posterior descarte/eliminación del arreglo cuando `vida <= 0`.

18. **D. Crear `LectorXML extends Lector` que implemente `leer()` y devuelva el mismo formato, sin modificar el flujo existente.**
    * *Justificación:* Respeta la polimorfia y la extensión sin modificar el código cliente.

19. **A. Hacer que `dibujar()` en Marca lance un error descriptivo, que aparece al usarlo en una subclase que no lo redefine.**
    * *Justificación:* Es el mecanismo clásico de simulación de métodos abstractos en JavaScript: `dibujar() { throw new Error("Método 'dibujar()' debe ser implementado."); }`.

20. **B. Mantener una sola clase `Chispa` con atributos de color, tamaño y velocidad, evitando jerarquías por cada pequeña variación.**
    * *Justificación:* Evita la sobreingeniería y la proliferación innecesaria de subclases para simples variaciones de estado/propiedades.

---

## SECCIÓN II. RESPUESTA ABIERTA

### 21. Evaluación de Herencia vs. Composición
La afirmación es **falsa**. La herencia representa una relación rígida tipo *"es un"* ($A$ es un $B$), donde la subclase hereda todo el estado y comportamiento de la superclase. La composición representa una relación flexible tipo *"tiene un"* ($A$ tiene un $B$), donde una clase delega comportamiento a objetos contenidos.

* **Cuándo conviene la herencia:** Cuando existe una jerarquía conceptual natural clara y fuerte, y las subclases comparten estado, código y ciclo de vida identitarios (ej. `Onda extends ElementoVisual`).
* **Cuándo conviene la composición:** Cuando se busca combinar capacidades dinámicas que pueden cambiar en tiempo de ejecución o evitar jerarquías profundas y acopladas.
* **Ejemplo:** En un videojuego, si creamos un `Personaje`, usar herencia para crear `PersonajeConEspada`, `PersonajeConArco`, etc., generaría una explosión de clases rígidas. En su lugar, es preferible la **composición**: `Personaje` *tiene un* atributo `arma` (que puede ser una instancia de `Espada` o `Arco` y cambiarse dinámicamente con `personaje.setArma(...)`).

---

### 22. Uso de `super(...)` antes de `this`
En JavaScript, cuando una clase extiende a otra mediante `extends`, el motor de ejecución asigna la responsabilidad de instanciar y vincular el objeto (`this`) al constructor de la superclase. Por tanto, `this` no existe ni está asignado en la subclase hasta que `super(...)` es ejecutado.

* **Consecuencia de incumplimiento:** Si se intenta acceder a `this` antes de llamar a `super()`, JavaScript lanza inmediatamente un `ReferenceError: Must call super constructor in derived class before accessing 'this'`.
* **Subclase sin constructor explícito:** Si no se define un constructor en la subclase, JavaScript inserta implícitamente un constructor por defecto que llama a la superclase pasando todos los argumentos recibidos:
  ```javascript
  constructor(...args) {
    super(...args);
  }
  ```

---

### 23. Sobrescritura de métodos y Polimorfismo
La **sobrescritura (*overriding*)** es la técnica donde una subclase proporciona su propia implementación de un método ya definido en su superclase. Es el pilar fundamental que permite el **polimorfismo**: la capacidad de que objetos de distintas clases respondan a la misma invocación de un método ejecutando su propia lógica interna.

* **Determinación del método a ejecutar:** Se determina dinámicamente en tiempo de ejecución (*dynamic dispatch*) según el tipo real del objeto instanciado, no por la referencia o el contenedor donde guardemos dicho objeto.
* **Ejemplo:** Superclase `Vehiculo` con método `arrancar()`. Subclase `AutoElectrico` sobrescribe `arrancar()` imprimiendo *"Iniciando sistemas eléctricos..."*. Subclase `AutoGasolina` sobrescribe `arrancar()` imprimiendo *"Encendiendo motor de combustión..."*.
* **Ventaja:** El módulo cliente que utiliza los objetos solo necesita hacer `vehiculo.arrancar()` dentro de un bucle sobre un arreglo de vehículos. Quien usa estos objetos escribe código desacoplado, limpio y fácilmente extensible a nuevos vehículos sin requerir modificadores ni condicionales (`if`/`else`).

---

### 24. Clase Abstracta vs. Interfaz en JavaScript
* **Clase Abstracta:** Aporta una plantilla base con estado compartido (atributos) y métodos concretos con lógica reutilizable, además de declarar métodos abstractos (sin cuerpo) que las subclases están obligadas a implementar.
* **Interfaz:** Define puramente un contrato o protocolo de comunicación (nombres de métodos y firmas) sin proveer implementación ni estado heredable.
* **Simulación en JS:**
  * *Clase Abstracta:* Se simula validando `if (new.target === ClaseBase) throw new Error(...)` en el constructor y haciendo que los métodos abstractos lancen un `Error("Debe ser implementado")`.
  * *Interfaz:* Se simula revisando mediante tipificación estructural (*duck typing*) si un objeto contiene un conjunto de métodos requeridos mediante funciones auxiliares (ej. `if (typeof obj.mostrar === 'function')`).
* **Elección / Caso práctico:** Para un sistema bancario, elegimos **Clase Abstracta** `CuentaBancaria` (con saldo, historial y método abstracto `calcularComision()`) cuando las cuentas comparten datos y lógica. Elegimos **Interfaz** `Notificable` (con el método `enviarNotificacion()`) cuando queremos que clases sin relación jerárquica (`Usuario`, `Transaccion`, `AlertaSeguridad`) puedan ser notificadas por email/SMS sin forzarlas a compartir una superclase.

---

### 25. Responsabilidades en la jerarquía `Elemento`
* **Responsabilidades fijas (Superclase `Elemento`):** Maneja el comportamiento común transversal. Define el método concreto `haTerminado()` (por ejemplo, evaluando si `this.vida <= 0`), controlando el ciclo de vida estandarizado del objeto. También maneja la inicialización de coordenadas genéricas (`x`, `y`) y la gestión del nivel de vida.
* **Responsabilidades delegadas (Subclases `Onda`, `Chispa`, etc.):** Implementan la lógica específica de actualización y renderizado mediante los métodos abstractos `actualizar()` (animación, física, aceleración) y `mostrar()` (formas visuales, colores, efectos con p5.js/canvas).
* **Funcionamiento uniforme en `draw()`:** El ciclo `draw()` solo necesita iterar sobre el arreglo general de elementos invocando:
  ```javascript
  elem.actualizar();
  elem.mostrar();
  if (elem.haTerminado()) { /* eliminar */ }
  ```
  Esto funciona porque la superclase garantiza la existencia de la interfaz pública, permitiendo un tratamiento polimórfico sin importar la representación gráfica interna de cada subclase.

---

## SECCIÓN III. APLICACIÓN MEDIANTE EJEMPLOS

### 26. Diseño de Extracción ETL
* **Superclase Abstracta / Contrato:** `ExtractorDatos`
  * *Método común/abstracto:* `extraer()` (devuelve un arreglo normalizado de objetos con las ventas).
* **Subclases:**
  1. `ExtractorCSV extends ExtractorDatos`: Lee y parsea texto plano delimitado por comas.
  2. `ExtractorJSONAPI extends ExtractorDatos`: Realiza solicitudes HTTP y procesa la respuesta JSON.
  3. `ExtractorSQL extends ExtractorDatos`: Ejecuta una consulta SQL en la base de datos relacional.
* **Procesamiento uniforme en el flujo principal:**
  ```javascript
  const fuentes = [
    new ExtractorCSV('ventas.csv'),
    new ExtractorJSONAPI('https://api.empresa.com/ventas'),
    new ExtractorSQL('DB_PROD')
  ];

  let todasLasVentas = [];
  for (const fuente of fuentes) {
    // El flujo principal desconoce el origen técnico; extrae de forma polimórfica
    const registros = fuente.extraer();
    todasLasVentas.push(...registros);
  }
  ```

---

### 27. Componentes de Pantalla Web (UI)
* **Superclase Abstracta:** `ComponenteUI`
  * *Atributos base:* `id`, `estilos`, `visible`.
  * *Método abstracto:* `renderizar()`
* **Subclases:**
  1. `BotonUI extends ComponenteUI`: Sobrescribe `renderizar()` retornando el elemento `<button>` con sus eventos de clic.
  2. `TablaUI extends ComponenteUI`: Sobrescribe `renderizar()` construyendo una estructura HTML `<table>` a partir de sus filas y columnas.
  3. `FormularioUI extends ComponenteUI`: Sobrescribe `renderizar()` construyendo un contenedor `<form>` con sus inputs correspondientes.
* **Ventaja para la evolución del sistema:** Permite crear una clase contenedora (ej. `Dashboard`) que gestiona una lista `componentes: ComponenteUI[]`. Si en el futuro se añade un nuevo componente como `GraficoUI`, el sistema no requiere modificar el motor de renderizado de la interfaz, garantizando escalabilidad pura y bajo acoplamiento.

---

### 28. Tablero de Indicadores Financieros
* **Jerarquía de Clases:**
  * Superclase abstracta: `GraficoTablero` (posee el atributo `datos` y el método general `procesarDatos()`).
  * Subclases: `GraficoBarras`, `GraficoLíneas`, `GraficoTorta`.
* **Código que permanece igual:** El motor del tablero que itera el arreglo de gráficos, la carga de datos del backend, la disposición del canvas/contenedor en pantalla y la rutina que llama a `grafico.dibujar()`.
* **Código que varía:** La implementación específica del método `dibujar()` dentro de cada subclase:
  * `GraficoBarras` calcula anchos y alturas de rectángulos.
  * `GraficoLíneas` calcula trazados vectoriales entre coordenadas de datos.
  * `GraficoTorta` calcula ángulos y arcos radiales.

---

### 29. Contratos para Módulos de Empresa
* **Contratos (Interfaces / Duck Typing):**
  1. `Exportable`: exige el método `exportarAFormato(formato)`.
  2. `Auditable`: exige el método `obtenerRegistroAuditoria()`.
* **Aplicación en Clases:**
  * `Factura`, `Cliente` e `Inventario` implementan ambos métodos según su naturaleza de negocio.
* **Por qué es más apropiada una Interfaz que una Clase Abstracta:** `Factura`, `Cliente` e `Inventario` pertenecen a dominios conceptuales completamente ajenos dentro de la empresa; no comparten una relación del tipo *"es un"* ni lógica de código en común. Obligarlos a heredar de una superclase común rompería el principio de responsabilidad única y la jerarquía real. Las interfaces permiten dotar a clases heterogéneas de capacidades funcionales comunes (*exportable*, *auditable*) mediante herencia múltiple de contratos.

---

### 30. Limpieza de Datos ETL (Reglas de Validación)
* **Diseño del Sistema:**
  * **Composición:** El motor `ProcesadorLimpieza` *tiene una* colección de reglas (`reglas: ReglaLimpieza[]`).
  * **Herencia / Polimorfismo:** Una clase abstracta `ReglaLimpieza` con el método `aplicar(registro)` que es sobrescrito polimórficamente por cada clase concreta:
    * `ReglaValidarEmail extends ReglaLimpieza`
    * `ReglaNormalizarFechas extends ReglaLimpieza`
    * `ReglaEliminarDuplicados extends ReglaLimpieza`

* **Flujo del Procesador:**
  ```javascript
  class ProcesadorLimpieza {
    constructor() {
      this.reglas = [];
    }

    agregarRegla(regla) {
      this.reglas.push(regla);
    }

    ejecutar(registro) {
      return this.reglas.reduce((regActual, regla) => regla.aplicar(regActual), registro);
    }
  }
  ```
* **Cómo agregar una nueva regla sin modificar el flujo:** Para incorporar una nueva regla (por ejemplo, `ReglaSanitizarTelefono`), solo se crea la nueva clase `class ReglaSanitizarTelefono extends ReglaLimpieza` que implementa `aplicar(registro)`. Luego se instancia e inyecta al pipeline mediante `procesador.agregarRegla(new ReglaSanitizarTelefono())`. El código interno del `ProcesadorLimpieza` permanece 100% intacto.