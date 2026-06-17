# Solución — Clase 03: Funciones y Manejo de Errores

> ⚠️ **Intentá resolver los ejercicios antes de mirar esto.**

### Ejercicio 1 — Tu primera función 
 
```python
def calcular_salario_neto(salario_bruto, retencion=0.17):
    return salario_bruto * (1 - retencion)
 
salario_ana   = calcular_salario_neto(85000)
salario_luis  = calcular_salario_neto(120000)
salario_clara = calcular_salario_neto(67000)
 
print(f"Ana:   ${salario_ana:,.2f}")
print(f"Luis:  ${salario_luis:,.2f}")
print(f"Clara: ${salario_clara:,.2f}")
 
# Si la tasa cambia, solo modificás la definición de la función:
salario_ana   = calcular_salario_neto(85000, retencion=0.20)
salario_luis  = calcular_salario_neto(120000, retencion=0.20)
salario_clara = calcular_salario_neto(67000, retencion=0.20)
```
 
**La respuesta a la pregunta:** antes de refactorizar, cambiar la tasa requería modificar tres líneas — y encontrarlas todas. Después, una sola. En un programa real con cincuenta empleados, la diferencia entre modificar una línea y modificar cincuenta es también la diferencia entre un bug posible y un bug inevitable.
 
 
### Ejercicio 2 — Función con múltiples retornos 
 
```python
def calcular_orden(precio_unitario, cantidad, descuento=0):
    subtotal        = precio_unitario * cantidad
    monto_descuento = subtotal * descuento
    total           = subtotal - monto_descuento
    return subtotal, monto_descuento, total
 
# Caso 1
subtotal, descuento, total = calcular_orden(12000, 3)
print(f"Subtotal: ${subtotal:,.2f} | Descuento: ${descuento:,.2f} | Total: ${total:,.2f}")
 
# Caso 2
subtotal, descuento, total = calcular_orden(8500, 5, descuento=0.10)
print(f"Subtotal: ${subtotal:,.2f} | Descuento: ${descuento:,.2f} | Total: ${total:,.2f}")
 
# Caso 3
subtotal, descuento, total = calcular_orden(45000, 2, descuento=0.25)
print(f"Subtotal: ${subtotal:,.2f} | Descuento: ${descuento:,.2f} | Total: ${total:,.2f}")
```
 
**Cómo funciona el retorno múltiple:** `return subtotal, monto_descuento, total` empaqueta los tres valores en una tupla. Al asignar `subtotal, descuento, total = calcular_orden(...)` Python los desempaqueta en orden. Si solo necesitaras uno de los valores, podrías usar `_` para los que no te interesan: `_, _, total = calcular_orden(8500, 5, 0.10)`.
 

 
### Ejercicio 3 — El código que explota 
 
```python
def convertir_temperatura(registro):
    try:
        celsius = float(registro["valor"])
        return (celsius * 9/5) + 32
    except ValueError:
        return None
 
sensores = [
    {"id": "S-01", "valor": "87.3"},
    {"id": "S-02", "valor": "N/A"},
    {"id": "S-03", "valor": "92.1"},
    {"id": "S-04", "valor": ""},
    {"id": "S-05", "valor": "88.7"},
]
 
for sensor in sensores:
    fahrenheit = convertir_temperatura(sensor)
    if fahrenheit is not None:
        print(f"{sensor['id']}: {fahrenheit:.1f}°F")
    else:
        print(f"{sensor['id']}: sin lectura")
```
 
**La respuesta a la reflexión:** antes del cambio, el pipeline procesaba correctamente solo el primer sensor — `S-01` — y se detenía en `S-02`. `S-03`, `S-04` y `S-05` nunca se procesaban. Después del cambio, los cinco sensores se procesan: tres con valor y dos con `"sin lectura"`. Un solo `try/except` en el lugar correcto cambia completamente el comportamiento del sistema ante datos imperfectos.
 
 
 
## Ejercicio 4 — Pipeline modular
 
```python
def limpiar_registro(r):
    if r["producto"] == "":
        raise ValueError("nombre vacío")
 
    precio = float(r["precio"])
    if precio <= 0:
        raise ValueError(f"precio inválido: {r['precio']}")
 
    stock = int(r["stock"])
 
    return {
        "producto":  r["producto"],
        "precio":    precio,
        "stock":     stock,
        "categoria": r["categoria"],
    }
 
def calcular_valor(registro):
    return registro["precio"] * registro["stock"]
 
def agrupar_por_categoria(registros):
    grupos = {}
    for r in registros:
        cat = r["categoria"]
        if cat not in grupos:
            grupos[cat] = []
        grupos[cat].append(r)
    return grupos
 
def procesar_dataset(registros):
    procesados = []
    errores    = []
 
    for r in registros:
        try:
            limpio = limpiar_registro(r)
            limpio["valor"] = calcular_valor(limpio)
            procesados.append(limpio)
        except (ValueError, KeyError) as e:
            errores.append({"producto": r.get("producto", "?"), "error": str(e)})
 
    return procesados, errores
 
 
# --- Programa principal ---
 
registros = [
    {"producto": "Notebook",   "precio": "320000", "stock": "5",   "categoria": "tech"},
    {"producto": "Escritorio", "precio": "85000",  "stock": "N/A", "categoria": "muebles"},
    {"producto": "Mouse",      "precio": "-8500",  "stock": "42",  "categoria": "tech"},
    {"producto": "",           "precio": "45000",  "stock": "8",   "categoria": "muebles"},
    {"producto": "Monitor",    "precio": "210000", "stock": "0",   "categoria": "tech"},
    {"producto": "Auriculares","precio": "32000",  "stock": "11",  "categoria": "tech"},
]
 
procesados, errores = procesar_dataset(registros)
grupos = agrupar_por_categoria(procesados)
 
print(f"Procesados: {len(procesados)} | Errores: {len(errores)}")
 
for categoria, items in grupos.items():
    total = sum(r["valor"] for r in items)
    print(f"\n{categoria.capitalize()} — valor total: ${total:,}")
 
for e in errores:
    print(f"  ✗ {e['producto']}: {e['error']}")
```
 
**Por qué importa la separación:** el código original y este producen exactamente el mismo resultado. La diferencia no es lo que hace — es lo que permite hacer después. Si mañana el criterio de validación cambia, modificás solo `limpiar_registro`. Si la fórmula de valor cambia, modificás solo `calcular_valor`. Si necesitás agrupar por vendedor en lugar de categoría, modificás solo `agrupar_por_categoria`. Ningún cambio toca el resto. Eso es lo que hace que el código pueda crecer.
 
 
← [Volver a ejercicios](./ejercicios_clase03.md)
 