# Clase 1 — Introducción al Data Analysis, tu entorno de trabajo y las primeras líneas de Python


En 2012, el diario The New York Times publicó un artículo sobre un rol que casi nadie conocía: el *data scientist*. Lo describieron como "el trabajo más sexy del siglo XXI". Una década después, el mercado explotó, pero también quedó claro que no toda empresa necesita un científico de datos. Lo que *toda* empresa necesita es alguien que pueda tomar un archivo lleno de números y responder una pregunta concreta.

Antes de ver cualquier herramienta, piensa en esto **¿qué harías si tu jefe te manda un Excel con 50.000 filas de ventas y te pide saber cuáles son los tres productos que más se devuelven, en qué zonas, y en qué meses del año?**

Podrías hacerlo a mano. Podrías filtrar, ordenar, hacer tablas dinámicas durante horas o podrías escribir diez líneas de Python y tener la respuesta en segundos, junto con un gráfico que puedes pegar directo en la presentación. Eso es exactamente lo que vas a poder hacer al terminar este curso.


## Qué vamos a ver hoy

- Qué es el Data Analysis y qué hace realmente un analista de datos
- Cómo configurar tu entorno de trabajo en Jupyter y Google Colab
- Cómo usar Git y GitHub para guardar y publicar tu trabajo
- Variables y tipos de datos en Python

Al final de esta clase vas a tener tu entorno configurado, tu primer repositorio en GitHub, y tus primeras líneas de código escritas y guardadas. No es poco para el primer día.


## ¿Qué hace un analista de datos?

Hay una imagen popular del analista de datos, alguien frente a pantallas con gráficos que parpadean en tiempo real, tomando decisiones millonarias. La realidad es más interesante y más útil que eso. Un analista de datos toma información que existe en archivos, bases de datos, planillas, APIs y la convierte en respuestas. No en datos más ordenados, no en tablas más lindas sino en *respuestas a preguntas de negocio*. Ejemplo: ¿Por qué cayeron las ventas en marzo? ¿Qué tipo de cliente se va después del primer mes? ¿En qué barrio conviene abrir el próximo local? ¿Cuál de estos dos precios genera más ingresos?. Para responder esas preguntas, el analista hace cuatro cosas en orden:

- **Obtiene los datos.** Los busca, los descarga, los conecta desde una base de datos, los limpia cuando llegan sucios y casi siempre llegan sucios.

- **Los transforma.** Filtra lo que no sirve, combina tablas, calcula columnas nuevas, agrupa por categorías. Convierte el caos en algo que se puede analizar.

- **Los analiza.** Aplica estadística, busca patrones, compara períodos, detecta anomalías. Encuentra lo que no es obvio a simple vista.

- **Comunica los resultados.** Crea visualizaciones, escribe conclusiones, presenta insights de forma que alguien sin conocimientos técnicos pueda tomar una decisión.

Python es la herramienta que mejor acompaña ese proceso completo, de principio a fin.

### ¿Por qué Python y no Excel?

Excel no es una herramienta mala. Pero tiene un límite práctico alrededor de las 100.000 filas antes de volverse lento e impredecible. No tiene forma de documentar qué hiciste paso a paso. No podés automatizar un análisis para que se repita solo el mes siguiente. Y cuando cometés un error, muchas veces no sabés dónde.

Python resuelve todos esos problemas. Un script de Python es reproducible cualquier persona puede correrlo y obtener el mismo resultado. Es escalable, funciona igual con 1.000 filas que con 10.000.000. Y es auditable, cada transformación que haces queda escrita y documentada. Ojo! no vas a abandonar Excel para siempre. Vas a entender cuándo usar cada herramienta.


## Tu entorno de trabajo

### Qué es Jupyter

Cuando escribes código Python en un archivo `.py` normal, tienes que ejecutarlo entero cada vez que quieres ver qué pasa. Para el análisis de datos, eso es un problema, quieres ver los resultados intermedios, explorar, probar, equivocarte sin perder todo el trabajo anterior.

Jupyter Notebook resuelve eso con un concepto simple, el archivo se divide en *celdas*. Cada celda puede tener código o texto, y puedes ejecutar cada celda de forma independiente. Ejecutas una celda, ves el resultado debajo, ajustas, sigues. El resultado es algo que se parece más a un cuaderno de laboratorio que a un archivo de código. De hecho, "Jupyter" viene de **Ju**lia, **Pyt**hon y **R**, los tres lenguajes científicos que originalmente soportaba.

### Jupyter local vs Google Colab

Vamos a trabajar con dos versiones de Jupyter a lo largo del curso.

**Jupyter local** corre en tu computadora. Necesitás instalarlo, pero tiene la ventaja de que funciona sin internet y te da control total sobre tu entorno. Lo instalás a través de Anaconda, que además incluye todas las librerías que vamos a usar.

**Google Colab** es Jupyter en el navegador, sin instalar nada. Google te provee una máquina virtual gratuita con Python, las librerías principales, y hasta acceso a GPU si la necesitás. Es ideal para empezar rápido o para trabajar desde cualquier máquina.

Para esta clase, vas a usar Colab. Para el resto del curso, vas a tener los dos disponibles.

### Cómo abrir tu primer notebook en Colab

Entra a [colab.research.google.com](https://colab.research.google.com). Si tienes cuenta de Google, ya puedes empezar. Haz clic en *New notebook*. Lo que ves es tu primer notebook en blanco. Tiene una celda vacía esperando código. Antes de escribir código, entendé la interfaz:

La barra de herramientas superior tiene botones para agregar celdas de código (`+ Code`) y celdas de texto (`+ Text`). A la izquierda de cada celda de código hay un botón ▶ para ejecutarla. El atajo de teclado que más vas a usar es `Shift + Enter`: ejecuta la celda actual y pasa a la siguiente.

Escribí esto en la primera celda y ejecutala:

```python
print("Hola, mundo del análisis de datos")
```

Deberías ver el texto impreso debajo de la celda. Acabás de ejecutar tu primer programa.

### Instalación local con Anaconda

Si quieres trabajar sin depender de internet, instala Anaconda. Es una distribución de Python que incluye todo lo que necesitas, el intérprete de Python, Jupyter, y las librerías científicas principales (Pandas, NumPy, Matplotlib y más).

Descargalo desde [anaconda.com/download](https://www.anaconda.com/download). Elige la versión para tu sistema operativo y sigue el instalador. Una vez instalado, abre *Anaconda Navigator* y haz clic en *Launch* bajo Jupyter Notebook. Se va a abrir una pestaña en tu navegador con el explorador de archivos de Jupyter. Desde ahí podés crear un notebook nuevo con *New → Python 3*.


## Git y GitHub para analistas

### Por qué un analista de datos necesita Git

Git es un sistema de control de versiones. Eso significa que registra cada cambio que hacés en tu código, cuándo lo hiciste, y te permite volver a cualquier versión anterior. Para un analista, Git resuelve tres problemas concretos:

- El primero es el problema del `analisis_final_v3_ESTEESELFINAL.ipynb`. Sin Git, guardas versiones manualmente y en algún momento pierdes el hilo de cuál es cuál. Con Git, hay una sola versión del archivo y el historial completo de cambios está guardado automáticamente.

- El segundo es la reproducibilidad. Si alguien quiere verificar tu análisis o retomarlo seis meses después, puede clonar tu repositorio y tener exactamente lo mismo que vos tenías.

- El tercero es el portfolio. GitHub es donde los reclutadores técnicos van a buscar evidencia de tu trabajo. Un repositorio bien organizado con commits regulares dice más que un CV.

### La diferencia entre Git y GitHub

Git es el software que corre en tu computadora y registra los cambios. GitHub es la plataforma online donde subes esos cambios para que queden guardados en la nube y sean accesibles para otros. La relación es simple, Git es la herramienta, GitHub es el lugar donde guardás el resultado.

![git-vs-github](../../assets/clase-01/git-vs-github.jpg)

### Cómo crear tu primer repositorio

**Paso 1: Crear una cuenta en GitHub**

Si no tienes cuenta, entra a [github.com](https://github.com) y regístrate. Elige un nombre de usuario profesional — esto aparecerá en tu portafolio.

**Paso 2: Instalar Git**

En Windows: descarga el instalador desde [git-scm.com](https://git-scm.com).  
En Mac: abre la terminal y ejecuta `git --version`. Si no está instalado, el sistema te ofrecerá instalarlo.  
En Linux: `sudo apt install git`.

Verifica que quedó instalado:

```bash
git --version
```

**Paso 3: Configurar tu identidad**

Git necesita saber quién está haciendo los cambios. Ejecuta esto en tu terminal, reemplazando con tus datos:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

Usa el mismo correo electrónico que registraste en GitHub.

**Paso 4: Crear el repositorio en GitHub**

Entra a GitHub y haz clic en el botón verde *New* (o el ícono `+` arriba a la derecha → *New repository*).

Completa el formulario:
- **Repository name:** `data-analysis-curso` (sin espacios, todo en minúsculas)
- **Description:** "Mi progreso en el curso de Data Analysis con Python"
- **Visibility:** Public
- Marca *Add a README file*

Haz clic en *Create repository*.

**Paso 5: Clonar el repositorio en tu máquina**

En la página de tu repositorio, haz clic en el botón verde *Code* y copia la URL HTTPS.

En tu terminal, navega a la carpeta donde quieres guardar el proyecto y ejecuta:

```bash
git clone https://github.com/tu-usuario/data-analysis-curso.git
cd data-analysis-curso
```

**Paso 6: Tu primer commit**

Crea un archivo nuevo dentro de la carpeta:

```bash
echo "# Mi primer análisis" > clase-01.md
```

Ahora le indica a Git que registre ese cambio:

```bash
git add clase-01.md
git commit -m "clase 01: primer archivo del curso"
git push origin main
```

Entra a GitHub y actualiza la página de tu repositorio. Tu archivo ya está ahí.

Has completado el ciclo completo de Git: crear un archivo → agregarlo al staging (`git add`) → confirmar el cambio (`git commit`) → subirlo a GitHub (`git push`).

### El flujo que vas a usar en cada clase

A partir de ahora, al final de cada clase, vas a hacer esto:

```bash
git add .
git commit -m "clase XX: descripción de lo que hiciste"
git push origin main
```

Eso es todo lo que necesitás saber de Git por ahora. Hay mucho más — ramas, merges, pull requests — pero eso viene después. Por el momento, con este flujo alcanza.


## Variables y tipos de datos

Cuando analizas datos, necesitas guardar información temporalmente para poder usarla más adelante. Una variable es simplemente un nombre que le pones a un valor para poder referenciarlo después.

En Python, crear una variable es directo:

```python
ciudad = "Buenos Aires"
temperatura = 22.5
cantidad_usuarios = 1500
activo = True
```

No necesitas declarar el tipo de la variable de antemano — Python lo deduce solo a partir del valor que le asignas. Esto se llama *tipado dinámico* y hace que el código sea más rápido de escribir, aunque también requiere más atención para no mezclar tipos sin querer.

El nombre que le das a una variable importa. `x` funciona técnicamente, pero `precio_unitario` le dice a cualquiera que lea el código — incluido quien lo lea dentro de unas semanas — qué contiene esa variable.

### Los tipos de datos fundamentales

Python tiene varios tipos de datos básicos. En el análisis de datos, estos cuatro aparecen constantemente.

**Strings (`str`)** — texto entre comillas simples o dobles.

```python
nombre_producto = "Zapatillas Running"
categoria = 'Deportes'
```

Los strings son el tipo de dato más común cuando trabajas con datos reales: nombres de clientes, descripciones de productos, ciudades, categorías. También son el tipo que más limpieza necesita — vienen con espacios de más, mayúsculas inconsistentes, caracteres raros.

**Enteros (`int`)** — números sin decimales.

```python
cantidad_ventas = 342
año = 2024
codigo_sucursal = 7
```

**Flotantes (`float`)** — números con decimales.

```python
precio = 15990.50
tasa_conversion = 0.034
temperatura_promedio = 18.7
```

La diferencia entre `int` y `float` importa cuando haces operaciones. `10 / 3` en Python devuelve `3.3333...` (float). `10 // 3` devuelve `3` (división entera).

**Booleanos (`bool`)** — solo dos valores posibles: `True` o `False`.

```python
es_cliente_premium = True
tiene_descuento = False
mayor_de_edad = True
```

Los booleanos son el resultado de cualquier comparación. Cuando más adelante filtres datos — "dame todas las ventas donde el precio es mayor a 1000" — el resultado de cada comparación va a ser un booleano.

### Cómo verificar el tipo de una variable

Python tiene una función incorporada llamada `type()` que te dice exactamente qué tipo es cada variable:

```python
precio = 15990.50
print(type(precio))   # <class 'float'>

nombre = "Ana García"
print(type(nombre))   # <class 'str'>

cantidad = 42
print(type(cantidad)) # <class 'int'>
```

Esto parece trivial ahora, pero se vuelve crítico cuando recibes datos de fuentes externas. Un CSV puede traerte precios como strings ("15990.50" con comillas), y si intentas sumarlos sin convertirlos primero, Python te va a dar un error. `type()` es tu primer diagnóstico.

### Operaciones básicas con cada tipo

Con números puedes hacer las operaciones aritméticas esperadas:

```python
precio_unitario = 1200
cantidad = 5
descuento = 0.10

subtotal = precio_unitario * cantidad
descuento_aplicado = subtotal * descuento
total = subtotal - descuento_aplicado

print(total)  # 5400.0
```

Con strings, la operación más común es la concatenación — unir dos textos:

```python
nombre = "María"
apellido = "González"
nombre_completo = nombre + " " + apellido
print(nombre_completo)  # María González
```

Pero en análisis de datos rara vez concatenas strings con `+`. Vas a usar f-strings, que son más limpias y legibles:

```python
producto = "Notebook"
precio = 450000
print(f"El {producto} cuesta ${precio:,}")  # El Notebook cuesta $450,000
```

### Conversión entre tipos

Transformar un valor de un tipo a otro se llama *casting*. Es una operación que vas a hacer constantemente al limpiar datos.

```python
# String a número
precio_texto = "1500"
precio_numero = int(precio_texto)
print(precio_numero + 500)  # 2000

# Número a string
codigo = 42
codigo_texto = str(codigo)
print("Código: " + codigo_texto)  # Código: 42

# String a float
tasa_texto = "3.5"
tasa_numero = float(tasa_texto)
print(tasa_numero * 100)  # 350.0
```

Cuando un casting falla — porque el string tiene texto que no es un número — Python lanza un `ValueError`. En la Clase 3 vas a aprender a manejar esos errores con `try/except`. Por ahora, asegúrate de que los valores que conviertes tengan el formato correcto.


## Recursos adicionales

- [Documentación oficial de Python — Tipos de datos](https://docs.python.org/es/3/library/stdtypes.html)
- [Google Colab — Guía de inicio](https://colab.research.google.com/notebooks/intro.ipynb)
- [Git — Guía de inicio rápido (GitHub)](https://docs.github.com/es/get-started/quickstart)
- [Anaconda — Descarga](https://www.anaconda.com/download)

---

## Práctica

→ [Ver ejercicios](https://github.com/rosinni/data-analysis-course/blob/main/modulo-1-python/clase-01/practica/notebook.ipynb)

---

*[Módulo 1](../README.md) · [Clase 2 — Control de flujo y estructuras de datos →](../clase-02/)*
