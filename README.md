# Documentación sobre la Arquitectura Hexagonal para la Plataforma de Comercio Electrónico del Cubo Rubik

La arquitectura hexagonal, también conocida como "arquitectura de puertos y adaptadores", es un patrón de diseño que se basa en separar el núcleo de la aplicación de sus interacciones externas. En el caso de una plataforma de comercio electrónico dedicada al cubo Rubik, esto significa que la lógica de negocio estará aislada de las interfaces de usuario, bases de datos y otros sistemas externos.

## Ventajas de la Arquitectura Hexagonal

1. **Independencia**: La lógica de negocio no depende de las tecnologías externas.
2. **Facilidad de prueba**: Es más fácil probar el núcleo de la aplicación sin interferencias externas.
3. **Flexibilidad**: Permite cambiar las tecnologías externas sin afectar el núcleo.

## Componentes de la Arquitectura Hexagonal

### 1. Núcleo de la Aplicación
El núcleo contiene la lógica de negocio de la plataforma. Aquí es donde se gestionan las reglas de venta, la logística del cubo Rubik y las interacciones con los usuarios. Este componente no debería tener acceso directo a los elementos externos.

### 2. Puertos
Los puertos son interfaces que definen cómo interactuar con el núcleo. Pueden ser de entrada (para recibir comandos) o de salida (para enviar información a sistemas externos).

### 3. Adaptadores
Los adaptadores son implementaciones de los puertos. Permiten que la aplicación se comunique con el mundo exterior. Por ejemplo:
- Un adaptador HTTP para recibir solicitudes de un front-end.
- Un adaptador de base de datos para gestionar la persistencia de datos.

## Ejemplo de Implementación

### Núcleo
Aquí se define la clase de producto del cubo Rubik:
```python
class RubikCube:
    def __init__(self, color_config):
        self.color_config = color_config
        self.solved = False

    def solve(self):
        # Lógica para resolver el cubo
        pass
```

### Puerto de Entrada (Comando)
Definimos un puerto para agregar un producto:
```python
class ProductCommandPort:
    def add_product(self, product_info):
        pass
```

### Adaptador de Entrada
Un adaptador HTTP para agregar un producto:
```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/add_product', methods=['POST'])
def add_product():
    product_info = request.json
    # Lógica para usar el puerto de entrada
    return "Producto agregado"
```

## Conclusión
La arquitectura hexagonal proporciona un diseño flexible y mantenible para aplicaciones complejas. En la plataforma de comercio electrónico del cubo Rubik, esta arquitectura permite una clara separación de preocupaciones, facilitando tanto el desarrollo como el mantenimiento a largo plazo.