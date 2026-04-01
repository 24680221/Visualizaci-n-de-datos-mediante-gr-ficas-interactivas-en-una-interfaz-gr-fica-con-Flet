# Visualizaci-n-de-datos-mediante-gr-ficas-interactivas-en-una-interfaz-gr-fica-con-Flet

El siguiente código se enfoca en la visualización de datos dentro de una interfaz gráfica, utilizando la librería Flet en conjunto con Matplotlib. Su objetivo es permitir la interacción del usuario mediante botones que generan diferentes tipos de gráficas (barras, circular, líneas y dispersión), aplicando el uso de componentes, librerías y manejo de eventos. Este desarrollo se relaciona principalmente con la Unidad 2: Componentes y librerías, ya que integra herramientas externas para ampliar las funcionalidades de una aplicación gráfica.

Importación de librerías
-

Se utilizan varias librerías:

- Flet → para crear la interfaz gráfica.
- Matplotlib → para generar las gráficas.
- flet_charts → para integrar gráficas de Matplotlib dentro de Flet.
- random → para generar datos aleatorios en la gráfica de dispersión.
```
import flet as ft
import matplotlib.pyplot as plt
import flet_charts as fch
import random
```

Función: Gráfica de barras
-

Se definen datos de productos y ventas, se usa ax.bar() para crear la gráfica y se agrega título y etiquetas
```
# 📊 Gráfica de barras
def crear_barras():
    nombres = ["A", "B", "C", "D"]
    ventas = [15, 30, 45, 10]

    fig, ax = plt.subplots()
    ax.bar(nombres, ventas) # crea las graficas
    ax.set_title("Ventas por producto")
    ax.set_xlabel("Productos")
    ax.set_ylabel("Ventas")

    return fig
```

Función: Gráfica circular
-

Se definen datos de productos y ventas,se usa ax.pie() y se incluye porcentajes automáticos (autopct)
```
#  Gráfica circular
def crear_circular():
    nombres = ["Ana", "Carlos", "Luis", "Sofia"]
    ventas = [10, 15, 7, 12]

    fig, ax = plt.subplots()
    ax.pie(ventas, labels=nombres, autopct="%1.1f%%") #crea las graficas
    ax.set_title("Distribución de ventas")

    return fig
```

Función: Gráfica de líneas
-

Se definen datos de productos y ventas,Usa ax.plot() y se agrega puntos (marker="o") y cuadrícula
```
# 📈 Gráfica de líneas
def crear_lineas():
    meses = ["Ene", "Feb", "Mar", "Abr", "May"]
    rendimiento = [10, 25, 18, 40, 35]

    fig, ax = plt.subplots()
    ax.plot(meses, rendimiento, marker="o") #crea la grafica
    ax.set_title("Tendencia de rendimiento")
    ax.set_xlabel("Meses")
    ax.set_ylabel("Rendimiento")
    ax.grid(True)

    return fig
```

Función: Gráfica de dispersión
-

Se definen datos de productos y ventas, y se usa ax.scatter() que crea las graficas, y se agregan los titulos y etiquetas.
```
# Gráfica de dispersión
def crear_dispersion():
    x = list(range(20))
    y = [random.randint(10, 50) for _ in range(20)]

    fig, ax = plt.subplots()
    ax.scatter(x, y) #crea las graficas
    ax.set_title("Muestreo de  sensores")
    ax.set_xlabel("Tiempo")
    ax.set_ylabel("Valor")

    return fig
```

Función principal
-

Es el punto de entrada de la aplicación.
```
def main(page: ft.Page):
```

Configuración de la ventana
-

Se define el titulo y se centran los elementos.
```
    page.title = "Gráficas con Flet"
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER
```

Contenedor para la gráfica
-

Espacio donde se mostrarán las gráficas y se actualizará dinámicamente
  ```  grafica = ft.Container(width=400, height=300) #el espacio de grafica
```

Funciones para mostrar gráficas (eventos)
-

Cada botón ejecuta una función:
```
    # mostrar barras
    def mostrar_barras(e):
        fig = crear_barras()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    # mostrar circular
    def mostrar_circular(e):
        fig = crear_circular()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    # mostrar líneas
    def mostrar_lineas(e):
        fig = crear_lineas()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    # mostrar dispersión
    def mostrar_dispersion(e):
        fig = crear_dispersion()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)
```
- Proceso:

- Se crea la gráfica (crear_barras)
- Se inserta en el contenedor (MatplotlibChart)
- Se actualiza la página (page.update())
- Se libera memoria (plt.close(fig))

Esto se repite para:
- Circular
- Barras
- Líneas
- Dispersión

Diseño de la interfaz
-

```page.add(```
Se agregan los elementos:
- titulo -> ``` ft.Text("Selecciona el tipo de gráfica", size=25, weight="bold"), ```
- botones -> los botones son para cada tipo de grafica y cada uno con su evento onclick.
``` ft.Row(
            [
                ft.ElevatedButton("Barras", on_click=mostrar_barras),
                ft.ElevatedButton("Circular", on_click=mostrar_circular),
                ft.ElevatedButton("Líneas", on_click=mostrar_lineas),
                ft.ElevatedButton("Dispersión", on_click=mostrar_dispersion),
            ],
            alignment=ft.MainAxisAlignment.CENTER,
        ),
```

- Área de visualización
Aquí se muestran las gráficas generadas.
```grafica```

Ejecución
-

Inicia la aplicación.
```
ft.app(target=main)
```
Acontinuacion se muestra el codigo completo:

```
import flet as ft
import matplotlib.pyplot as plt
import flet_charts as fch
import random


# 📊 Gráfica de barras
def crear_barras():
    nombres = ["A", "B", "C", "D"]
    ventas = [15, 30, 45, 10]

    fig, ax = plt.subplots()
    ax.bar(nombres, ventas) # crea las graficas
    ax.set_title("Ventas por producto")
    ax.set_xlabel("Productos")
    ax.set_ylabel("Ventas")

    return fig


#  Gráfica circular
def crear_circular():
    nombres = ["Ana", "Carlos", "Luis", "Sofia"]
    ventas = [10, 15, 7, 12]

    fig, ax = plt.subplots()
    ax.pie(ventas, labels=nombres, autopct="%1.1f%%") #crea las graficas
    ax.set_title("Distribución de ventas")

    return fig


# 📈 Gráfica de líneas
def crear_lineas():
    meses = ["Ene", "Feb", "Mar", "Abr", "May"]
    rendimiento = [10, 25, 18, 40, 35]

    fig, ax = plt.subplots()
    ax.plot(meses, rendimiento, marker="o") #crea la grafica
    ax.set_title("Tendencia de rendimiento")
    ax.set_xlabel("Meses")
    ax.set_ylabel("Rendimiento")
    ax.grid(True)

    return fig


# Gráfica de dispersión
def crear_dispersion():
    x = list(range(20))
    y = [random.randint(10, 50) for _ in range(20)]

    fig, ax = plt.subplots()
    ax.scatter(x, y) #crea las graficas
    ax.set_title("Muestreo de  sensores")
    ax.set_xlabel("Tiempo")
    ax.set_ylabel("Valor")

    return fig


def main(page: ft.Page):

    page.title = "Gráficas con Flet"
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER

    grafica = ft.Container(width=400, height=300) #el espacio de grafica

    # mostrar barras
    def mostrar_barras(e):
        fig = crear_barras()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    # mostrar circular
    def mostrar_circular(e):
        fig = crear_circular()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    # mostrar líneas
    def mostrar_lineas(e):
        fig = crear_lineas()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    # mostrar dispersión
    def mostrar_dispersion(e):
        fig = crear_dispersion()
        grafica.content = fch.MatplotlibChart(figure=fig)
        page.update()
        plt.close(fig)

    page.add(
        ft.Text("Selecciona el tipo de gráfica", size=25, weight="bold"), 

        ft.Row(
            [
                ft.ElevatedButton("Barras", on_click=mostrar_barras),
                ft.ElevatedButton("Circular", on_click=mostrar_circular),
                ft.ElevatedButton("Líneas", on_click=mostrar_lineas),
                ft.ElevatedButton("Dispersión", on_click=mostrar_dispersion),
            ],
            alignment=ft.MainAxisAlignment.CENTER,
        ),

        grafica
    )


ft.app(target=main)
```

Acontinuacion se muestra la ejecucion:

<img width="1024" height="515" alt="image" src="https://github.com/user-attachments/assets/753081d7-f846-4325-93cc-50fca19b55c2" />

<img width="554" height="485" alt="image" src="https://github.com/user-attachments/assets/4c7b8a47-fb7f-4dee-9a49-c9511c5fb3f3" />

<img width="576" height="479" alt="image" src="https://github.com/user-attachments/assets/1706a67b-e437-48f8-a679-5c8cfae997b1" />

<img width="596" height="493" alt="image" src="https://github.com/user-attachments/assets/e96fad86-4210-41ff-8614-d51e48fd5644" />

<img width="559" height="483" alt="Captura de pantalla 2026-03-31 203847" src="https://github.com/user-attachments/assets/ae9498b5-57a6-4729-a77d-af081d926885" />
