# DOCUMENTACIÓN COMPLETA DEL MINI COMPILADOR

## INFORMACIÓN GENERAL

**Nombre:** Mini Compilador  
**Versión:** 1.0  
**Lenguaje de Programación:** JavaScript (HTML/CSS/JS)  
**Fecha de Creación:** 2024  
**Propósito:** Compilador educativo con todas las etapas de compilación

---

## ARQUITECTURA DEL COMPILADOR

### **Flujo de Compilación:**
```
Código Fuente → Análisis Léxico → Análisis Sintáctico → Transformación AST → Análisis Semántico → Código Intermedio → Generación JavaScript → Ejecución
```

### **Componentes Principales:**
1. **Analizador Léxico** - Tokenización del código fuente
2. **Analizador Sintáctico** - Construcción del AST
3. **Transformador de AST** - Optimizaciones y transformaciones
4. **Analizador Semántico** - Tabla de símbolos y validaciones
5. **Generador de Código Intermedio** - Código de tres direcciones
6. **Generador de JavaScript** - Código final ejecutable
7. **Intérprete** - Ejecución del código generado

---

## LENGUAJE DE PROGRAMACIÓN

### **Nombre:** MiniLang
**Descripción:** Lenguaje de programación simple y educativo diseñado para demostrar los conceptos de compilación.

### **Características del Lenguaje:**

#### **Tipos de Datos Soportados:**
- **Números:** `123`, `456`, `789`
- **Strings:** `"Hola mundo"`, `"Texto entre comillas"`
- **Booleanos:** `true`, `false`

#### **Identificadores:**
- **Reglas:** Deben comenzar con letra o guión bajo
- **Ejemplos válidos:** `x`, `y`, `variable`, `miVariable`, `_temp`
- **Ejemplos inválidos:** `123var`, `-variable`

#### **Operadores Aritméticos:**
```javascript
+  // Suma
-  // Resta
*  // Multiplicación
/  // División
```

#### **Operadores de Comparación:**
```javascript
==  // Igual
!=  // Diferente
<   // Menor que
>   // Mayor que
<=  // Menor o igual
>=  // Mayor o igual
```

#### **Operadores Lógicos:**
```javascript
&&  // AND lógico
||  // OR lógico
!   // NOT lógico
```

#### **Palabras Clave:**
```javascript
let     // Declaración de variable
print   // Instrucción de impresión
if      // Estructura condicional
else    // Rama alternativa
while   // Bucle while
```

---

## SINTAXIS DEL LENGUAJE

### **1. Declaración de Variables:**
```javascript
let variable = valor;
let x = 5;
let y = x + 3;
let mensaje = "Hola mundo";
```

### **2. Instrucción Print:**
```javascript
print(expresion);
print(x);
print("Texto");
print(x + y);
```

### **3. Estructura Condicional:**
```javascript
if (condicion) {
    // código si es verdadero
} else {
    // código si es falso
}

// Ejemplo:
if (x > 3) {
    let z = x * 2;
    print(z);
} else {
    print("x es menor o igual a 3");
}
```

### **4. Bucle While:**
```javascript
while (condicion) {
    // código a repetir
}

// Ejemplo:
while (x > 0) {
    print(x);
    let x = x - 1;
}
```

### **5. Expresiones:**
```javascript
// Expresiones aritméticas
x + y
x - y
x * y
x / y

// Expresiones lógicas
x > y
x == y
x && y
x || y
!x

// Expresiones con strings
"texto"
"texto" + "otro"
```

---

## ANÁLISIS LÉXICO

### **Tipos de Tokens Reconocidos:**

| Tipo | Descripción | Ejemplos |
|------|-------------|----------|
| `PALABRA_CLAVE` | Palabras reservadas | `let`, `print`, `if`, `else`, `while` |
| `NUMERO` | Números enteros | `123`, `456`, `789` |
| `IDENTIFICADOR` | Nombres de variables | `x`, `y`, `variable` |
| `OPERADOR` | Operadores aritméticos | `+`, `-`, `*`, `/`, `=`, `!` |
| `OPERADOR_LOGICO` | Operadores lógicos | `==`, `!=`, `<=`, `>=`, `<`, `>`, `&&`, `||` |
| `DELIMITADOR` | Delimitadores | `(`, `)`, `{`, `}`, `;`, `,` |
| `STRING` | Cadenas de texto | `"Hola mundo"` |
| `BOOLEANO` | Valores booleanos | `true`, `false` |

### **Regex de Reconocimiento:**
```javascript
/\s*(let|print|if|else|while|true|false|"[^"]*"|[a-zA-Z_]\w*|\d+|=|\+|\-|\*|\/|\(|\)|\{|\}|;|,|==|!=|<=|>=|<|>|&&|\|\||!)/g
```

### **Ejemplo de Tokenización:**
```javascript
// Código fuente:
let x = 5;

// Tokens generados:
[
  { "tipo": "PALABRA_CLAVE", "valor": "let" },
  { "tipo": "IDENTIFICADOR", "valor": "x" },
  { "tipo": "OPERADOR", "valor": "=" },
  { "tipo": "NUMERO", "valor": "5" },
  { "tipo": "DELIMITADOR", "valor": ";" }
]
```

---

## ANÁLISIS SINTÁCTICO

### **Estructura del AST (Abstract Syntax Tree):**

#### **Nodo Raíz:**
```javascript
{
  "tipo": "PROGRAMA",
  "declaraciones": [...]
}
```

#### **Tipos de Nodos:**

| Tipo de Nodo | Descripción | Estructura |
|--------------|-------------|------------|
| `DECLARACION` | Declaración de variable | `{ tipo: "DECLARACION", nombre: "x", valor: {...} }` |
| `PRINT` | Instrucción de impresión | `{ tipo: "PRINT", valor: {...} }` |
| `IF` | Estructura condicional | `{ tipo: "IF", condicion: {...}, entonces: [...], sino: [...] }` |
| `WHILE` | Bucle while | `{ tipo: "WHILE", condicion: {...}, cuerpo: [...] }` |
| `LITERAL` | Valor literal | `{ tipo: "LITERAL", valor: 123 }` |
| `STRING` | Cadena de texto | `{ tipo: "STRING", valor: "texto" }` |
| `BOOLEANO` | Valor booleano | `{ tipo: "BOOLEANO", valor: true }` |
| `IDENTIFICADOR` | Referencia a variable | `{ tipo: "IDENTIFICADOR", nombre: "x" }` |
| `EXPRESION_BINARIA` | Operación binaria | `{ tipo: "EXPRESION_BINARIA", izquierda: {...}, operador: "+", derecha: {...} }` |
| `EXPRESION_LOGICA` | Operación lógica | `{ tipo: "EXPRESION_LOGICA", izquierda: {...}, operador: ">", derecha: {...} }` |

### **Ejemplo de AST:**
```javascript
// Código fuente:
let x = 5 + 3;
print(x);

// AST generado:
{
  "tipo": "PROGRAMA",
  "declaraciones": [
    {
      "tipo": "DECLARACION",
      "nombre": "x",
      "valor": {
        "tipo": "EXPRESION_BINARIA",
        "izquierda": { "tipo": "LITERAL", "valor": 5 },
        "operador": "+",
        "derecha": { "tipo": "LITERAL", "valor": 3 }
      }
    },
    {
      "tipo": "PRINT",
      "valor": { "tipo": "IDENTIFICADOR", "nombre": "x" }
    }
  ]
}
```

---

## TRANSFORMACIÓN DE AST

### **Optimizaciones Implementadas:**

#### **1. Constant Folding:**
```javascript
// Antes:
{
  "tipo": "EXPRESION_BINARIA",
  "izquierda": { "tipo": "LITERAL", "valor": 5 },
  "operador": "+",
  "derecha": { "tipo": "LITERAL", "valor": 3 }
}

// Después:
{
  "tipo": "LITERAL",
  "valor": 8,
  "optimizacion": "constante_folding"
}
```

#### **2. Constant Propagation:**
```javascript
// Antes:
let x = 5;
let y = x + 3;

// Después (si x es constante):
let x = 5;
let y = 8;  // x + 3 evaluado
```

#### **3. Expression Optimization:**
```javascript
// Antes:
{
  "tipo": "EXPRESION_BINARIA",
  "izquierda": {...},
  "operador": "+",
  "derecha": {...}
}

// Después:
{
  "tipo": "EXPRESION_BINARIA_OPTIMIZADA",
  "izquierda": {...},
  "operador": "+",
  "derecha": {...},
  "optimizacion": "operacion_optimizada"
}
```

### **Tipos de Nodos Optimizados:**
- `PROGRAMA_OPTIMIZADO`
- `DECLARACION_OPTIMIZADA`
- `PRINT_OPTIMIZADO`
- `IF_OPTIMIZADO`
- `WHILE_OPTIMIZADO`
- `EXPRESION_BINARIA_OPTIMIZADA`
- `EXPRESION_LOGICA_OPTIMIZADA`

---

## ANÁLISIS SEMÁNTICO

### **Tabla de Símbolos:**
```javascript
{
  "x": { "nombre": "x", "inicializada": true },
  "y": { "nombre": "y", "inicializada": true },
  "z": { "nombre": "z", "inicializada": true }
}
```

### **Funcionalidades:**
- **Detección de variables declaradas**
- **Verificación de inicialización**
- **Seguimiento del ámbito de variables**

---

## GENERACIÓN DE CÓDIGO INTERMEDIO

### **Formato de Salida:**
```javascript
// Código fuente:
let x = 5 + 3;
print(x);

// Código intermedio:
x = 8
print x
```

### **Características:**
- **Código de tres direcciones simplificado**
- **Formato legible**
- **Sin optimizaciones complejas**

---

## GENERACIÓN DE JAVASCRIPT

### **Traducciones Implementadas:**

#### **Declaraciones:**
```javascript
// MiniLang: let x = 5;
// JavaScript: let x = 5;
```

#### **Prints:**
```javascript
// MiniLang: print(x);
// JavaScript: console.log(x);
```

#### **Condicionales:**
```javascript
// MiniLang:
if (x > 3) {
  print(z);
} else {
  print("texto");
}

// JavaScript:
if (x > 3) {
  console.log(z);
} else {
  console.log("texto");
}
```

#### **Bucles:**
```javascript
// MiniLang:
while (x > 0) {
  print(x);
  let x = x - 1;
}

// JavaScript:
while (x > 0) {
  console.log(x);
  let x = x - 1;
}
```

---

## INTERPRETACIÓN

### **Operadores Soportados:**

#### **Aritméticos:**
```javascript
+  // Suma: 5 + 3 = 8
-  // Resta: 5 - 3 = 2
*  // Multiplicación: 5 * 3 = 15
/  // División: 6 / 2 = 3
```

#### **Lógicos:**
```javascript
==  // Igual: 5 == 5 = true
!=  // Diferente: 5 != 3 = true
<   // Menor: 3 < 5 = true
>   // Mayor: 5 > 3 = true
<=  // Menor igual: 3 <= 5 = true
>=  // Mayor igual: 5 >= 3 = true
&&  // AND: true && false = false
||  // OR: true || false = true
```

---

## PRUEBAS Y EJEMPLOS

### **Ejemplo 1: Variables y Operaciones Básicas**
```javascript
let x = 5;
let y = x + 3;
print(y);
```

**Salida esperada:** `8`

### **Ejemplo 2: Condicionales**
```javascript
let x = 5;
if (x > 3) {
  let z = x * 2;
  print(z);
} else {
  print("x es menor o igual a 3");
}
```

**Salida esperada:** `10`

### **Ejemplo 3: Bucles**
```javascript
let x = 5;
while (x > 0) {
  print(x);
  let x = x - 1;
}
```

**Salida esperada:**
```
5
4
3
2
1
```

### **Ejemplo 4: Strings y Booleanos**
```javascript
let mensaje = "Hola mundo";
print(mensaje);

let esVerdadero = true;
if (esVerdadero) {
  print("La condición es verdadera");
}
```

**Salida esperada:**
```
Hola mundo
La condición es verdadera
```

### **Ejemplo 5: Operaciones Lógicas**
```javascript
let x = 5;
let y = 3;
if (x > y && x < 10) {
  print("x está entre y y 10");
}
```

**Salida esperada:** `x está entre y y 10`

---

## USO DEL COMPILADOR

### **1. Abrir el Compilador:**
- Abrir el archivo `MiniCompilador.html` en un navegador web

### **2. Escribir Código:**
- Usar el editor de texto en la parte superior
- Escribir código en el lenguaje MiniLang

### **3. Ejecutar:**
- Hacer clic en el botón "▶ Ejecutar"
- Ver los resultados en los paneles inferiores

### **4. Interpretar Resultados:**
- **Tokens:** Análisis léxico del código
- **AST:** Estructura sintáctica del código
- **AST Transformado:** Optimizaciones aplicadas
- **Tabla de Símbolos:** Variables declaradas
- **Código Intermedio:** Código de tres direcciones
- **Código JavaScript:** Código final generado
- **Salida:** Resultado de la ejecución

---

## LIMITACIONES Y RESTRICCIONES

### **Limitaciones del Lenguaje:**
- **No soporta funciones** - Solo código secuencial
- **No soporta arrays** - Solo variables simples
- **No soporta recursión** - No hay llamadas a funciones
- **Ámbito simple** - No hay bloques de ámbito anidados
- **Sin tipos estáticos** - No hay verificación de tipos

### **Limitaciones del Compilador:**
- **Sin optimizaciones avanzadas** - Solo optimizaciones básicas
- **Sin manejo de errores detallado** - Errores básicos
- **Sin generación de código nativo** - Solo JavaScript
- **Sin análisis de flujo** - No hay análisis de control de flujo

---

## TROUBLESHOOTING

### **Errores Comunes:**

#### **1. "Invalid array length"**
**Causa:** Error en el análisis léxico o sintáctico
**Solución:** Verificar la sintaxis del código

#### **2. Paneles vacíos**
**Causa:** Error en la ejecución del compilador
**Solución:** Usar el botón "🧪 Probar" para diagnóstico

#### **3. Código no se ejecuta**
**Causa:** Error de sintaxis
**Solución:** Verificar que el código siga la sintaxis correcta

### **Consejos de Uso:**
1. **Siempre terminar las líneas con `;`**
2. **Usar espacios alrededor de operadores**
3. **Verificar que las llaves `{}` estén balanceadas**
4. **Usar comillas dobles para strings**

---

## REFERENCIAS Y CONCEPTOS

### **Conceptos de Compilación:**
- **Tokenización:** Proceso de convertir texto en tokens
- **Parsing:** Proceso de construir un AST
- **Optimización:** Mejora del código para mejor rendimiento
- **Code Generation:** Generación de código ejecutable
- **Symbol Table:** Tabla que almacena información de variables

### **Conceptos de Lenguajes de Programación:**
- **Lexical Analysis:** Análisis léxico
- **Syntactic Analysis:** Análisis sintáctico
- **Semantic Analysis:** Análisis semántico
- **Intermediate Code:** Código intermedio
- **Target Code:** Código objetivo

---

## CONCLUSIÓN

Este mini compilador es una herramienta educativa completa que demuestra todos los conceptos fundamentales de la compilación de lenguajes de programación. Incluye:

- **Análisis léxico completo**
- **Análisis sintáctico con AST**
- **Optimizaciones básicas**
- **Análisis semántico**
- **Generación de código**
- **Interfaz web funcional**

**Ideal para:** Estudiantes de compiladores, programadores que quieren entender el proceso de compilación, y educadores que enseñan conceptos de lenguajes de programación.

---

*Documentación creada para el Mini Compilador v1.0*
*Fecha: 2024* 