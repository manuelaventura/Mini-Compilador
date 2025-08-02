# GUÍA DE PRUEBAS DEL MINI COMPILADOR

## INSTRUCCIONES RÁPIDAS

### **1. Abrir el Compilador:**
```bash
# Abrir el archivo en el navegador
MiniCompilador.html
```

### **2. Ejecutar Pruebas:**
1. **Escribir código** en el editor
2. **Hacer clic** en "▶ Ejecutar"
3. **Verificar** todos los paneles

---

## PRUEBAS BÁSICAS

### **Prueba 1: Variables Simples**
```javascript
let x = 5;
let y = 10;
print(x);
print(y);
```

**Resultado esperado:**
- **Salida:** `5` y `10`
- **Tabla de Símbolos:** `x` y `y` declaradas

### **Prueba 2: Operaciones Aritméticas**
```javascript
let a = 5;
let b = 3;
let suma = a + b;
let resta = a - b;
let multiplicacion = a * b;
print(suma);
print(resta);
print(multiplicacion);
```

**Resultado esperado:**
- **Salida:** `8`, `2`, `15`

### **Prueba 3: Strings**
```javascript
let mensaje = "Hola mundo";
print(mensaje);
let saludo = "Bienvenido";
print(saludo);
```

**Resultado esperado:**
- **Salida:** `Hola mundo` y `Bienvenido`

---

## PRUEBAS DE CONTROL DE FLUJO

### **Prueba 4: Condicional If**
```javascript
let x = 5;
if (x > 3) {
  print("x es mayor que 3");
} else {
  print("x es menor o igual a 3");
}
```

**Resultado esperado:**
- **Salida:** `x es mayor que 3`

### **Prueba 5: Condicional If-Else**
```javascript
let edad = 15;
if (edad >= 18) {
  print("Eres mayor de edad");
} else {
  print("Eres menor de edad");
}
```

**Resultado esperado:**
- **Salida:** `Eres menor de edad`

### **Prueba 6: Bucle While**
```javascript
let contador = 3;
while (contador > 0) {
  print(contador);
  let contador = contador - 1;
}
```

**Resultado esperado:**
- **Salida:** `3`, `2`, `1`

---

## PRUEBAS DE OPERADORES LÓGICOS

### **Prueba 7: Operadores de Comparación**
```javascript
let a = 5;
let b = 3;
print(a > b);
print(a == b);
print(a != b);
```

**Resultado esperado:**
- **Salida:** `true`, `false`, `true`

### **Prueba 8: Operadores Lógicos**
```javascript
let x = 5;
let y = 3;
if (x > y && x < 10) {
  print("x está entre y y 10");
}
if (x > 10 || y < 5) {
  print("Al menos una condición es verdadera");
}
```

**Resultado esperado:**
- **Salida:** `x está entre y y 10` y `Al menos una condición es verdadera`

---

## PRUEBAS AVANZADAS

### **Prueba 9: Expresiones Complejas**
```javascript
let x = 10;
let y = 5;
let resultado = (x + y) * 2;
print(resultado);

if (resultado > 20) {
  print("El resultado es mayor que 20");
}
```

**Resultado esperado:**
- **Salida:** `30` y `El resultado es mayor que 20`

### **Prueba 10: Múltiples Variables**
```javascript
let a = 1;
let b = 2;
let c = 3;
let suma = a + b + c;
print(suma);

let promedio = suma / 3;
print(promedio);
```

**Resultado esperado:**
- **Salida:** `6` y `2`

---

## PRUEBAS DE OPTIMIZACIÓN

### **Prueba 11: Constant Folding**
```javascript
let x = 5 + 3;
print(x);
```

**Verificar en AST Transformado:**
- Debe mostrar optimización `constante_folding`
- El valor debe ser `8` en lugar de `5 + 3`

### **Prueba 12: Múltiples Optimizaciones**
```javascript
let a = 2;
let b = 3;
let c = a * b;
print(c);

if (c > 5) {
  print("c es mayor que 5");
}
```

**Verificar optimizaciones:**
- Variables optimizadas
- Estructura if optimizada
- Expresiones evaluadas

---

## PRUEBAS DE ERRORES

### **Prueba 13: Sintaxis Incorrecta**
```javascript
let x = 5
print(x
```

**Resultado esperado:**
- Error en análisis sintáctico
- Paneles pueden estar vacíos o mostrar error

### **Prueba 14: Variables No Declaradas**
```javascript
print(y);
```

**Resultado esperado:**
- La variable `y` no estará en la tabla de símbolos
- Puede causar error en ejecución

---

## VERIFICACIÓN DE PANELES

### **Panel Tokens:**
- Debe mostrar array de objetos con `tipo` y `valor`
- Ejemplo: `[{"tipo": "PALABRA_CLAVE", "valor": "let"}]`

### **Panel AST:**
- Debe mostrar estructura JSON con nodos
- Debe tener `tipo: "PROGRAMA"` como raíz

### **Panel AST Transformado:**
- Debe mostrar optimizaciones aplicadas
- Debe tener `tipo: "PROGRAMA_OPTIMIZADO"`

### **Panel Tabla de Símbolos:**
- Debe mostrar variables declaradas
- Ejemplo: `{"x": {"nombre": "x", "inicializada": true}}`

### **Panel Código Intermedio:**
- Debe mostrar código simplificado
- Ejemplo: `x = 5` y `print x`

### **Panel Código JavaScript:**
- Debe mostrar código JavaScript válido
- Ejemplo: `let x = 5;` y `console.log(x);`

### **Panel Salida:**
- Debe mostrar resultado de la ejecución
- Números, strings o booleanos según el código

---

## PRUEBAS INTERACTIVAS

### **Prueba 15: Código Completo**
```javascript
let contador = 5;
print("Iniciando cuenta regresiva:");

while (contador > 0) {
  print(contador);
  let contador = contador - 1;
}

print("¡Despegue!");
```

**Resultado esperado:**
```
Iniciando cuenta regresiva:
5
4
3
2
1
¡Despegue!
```

### **Prueba 16: Condicionales Anidadas**
```javascript
let edad = 20;
let tienePermiso = true;

if (edad >= 18) {
  if (tienePermiso) {
    print("Acceso permitido");
  } else {
    print("Necesitas permiso");
  }
} else {
  print("Eres menor de edad");
}
```

**Resultado esperado:**
- **Salida:** `Acceso permitido`

---

## DIAGNÓSTICO DE PROBLEMAS

### **Si los paneles están vacíos:**
1. **Usar botón "Probar"** para diagnóstico
2. **Verificar sintaxis** del código
3. **Revisar consola** del navegador para errores

### **Si hay errores:**
1. **Verificar que todas las líneas terminen con `;`**
2. **Verificar que las llaves `{}` estén balanceadas**
3. **Verificar que los strings usen comillas dobles `""`**

### **Si el código no se ejecuta:**
1. **Usar código simple** para probar
2. **Verificar que no haya caracteres especiales**
3. **Revisar que las variables estén declaradas**

---

## CHECKLIST DE VERIFICACIÓN

- [ ] **Compilador se abre** en el navegador
- [ ] **Botón "Ejecutar"** funciona
- [ ] **Panel Tokens** muestra tokens correctos
- [ ] **Panel AST** muestra estructura JSON válida
- [ ] **Panel AST Transformado** muestra optimizaciones
- [ ] **Panel Tabla de Símbolos** muestra variables
- [ ] **Panel Código Intermedio** muestra código simplificado
- [ ] **Panel Código JavaScript** muestra código JS válido
- [ ] **Panel Salida** muestra resultado correcto
- [ ] **Botón "Probar"** funciona para diagnóstico
- [ ] **Ejecución automática** funciona al cargar

---

## CONCLUSIÓN

**Si todas las pruebas pasan:** Tu compilador está funcionando correctamente

**Si hay problemas:** Revisar la sección de diagnóstico y troubleshooting

**¡Tu mini compilador está listo para usar!** 