# Reto-3-POO
# Diagrama de Clase
  En el siguiente diagrama de clase se presenta la estrucutura del sistema de gestión del menú de un restaurante
 ```mermaid
  classDiagram   
  class MenuItem {
        - nombre: str
        - precio: float
        + calcular_precio(): float
    }
    
    class Bebida {
        + calcular_precio(): float
    }
    
    class Aperitivo {
        + calcular_precio(): float
    }
    
    class PlatoPrincipal {
        + calcular_precio(): float
    }
    
    class Pedido {
        - items: list~MenuItem~
        + agregar_item(item: MenuItem)
        + calcular_total(): float
    }
    
    MenuItem <|-- Bebida
    MenuItem <|-- Aperitivo
    MenuItem <|-- PlatoPrincipal
    Pedido --> MenuItem : usa
```
# Código 
  A continuación el código al cual representa el diagrama de clase anterior
  ```python
# Clase base MenuItem
class MenuItem:
    def __init__(self, nombre: str, precio: float):
        self.nombre = nombre
        self.precio = precio

    def calcular_precio(self) -> float:
        return self.precio


# Subclase Bebida
class Bebida(MenuItem):
    def __init__(self, nombre: str, precio: float, tamano: str):
        super().__init__(nombre, precio)
        self.tamano = tamano


# Subclase Aperitivo
class Aperitivo(MenuItem):
    def __init__(self, nombre: str, precio: float, para_compartir: bool):
        super().__init__(nombre, precio)
        self.para_compartir = para_compartir


# Subclase PlatoPrincipal
class PlatoPrincipal(MenuItem):
    def __init__(self, nombre: str, precio: float, es_vegetariano: bool):
        super().__init__(nombre, precio)
        self.es_vegetariano = es_vegetariano


# Clase Pedido
class Pedido:
    def __init__(self):
        self.items = []

    def agregar_item(self, item: MenuItem):
        self.items.append(item)

    def calcular_total(self) -> float:
        return sum(item.calcular_precio() for item in self.items)


# Crear un menú
menu = [
    Bebida("Coca Cola", 1.5, "500ml"),
    Bebida("Agua Mineral", 1.0, "500ml"),
    Bebida("Café", 2.0, "Taza"),
    Aperitivo("Papas Fritas", 3.5, True),
    Aperitivo("Nachos", 5.0, True),
    Aperitivo("Alitas de Pollo", 6.0, False),
    PlatoPrincipal("Hamburguesa", 8.5, False),
    PlatoPrincipal("Ensalada César", 7.0, True),
    PlatoPrincipal("Pasta Carbonara", 9.0, False),
    PlatoPrincipal("Pizza Margarita", 10.0, True),
]

pedido = Pedido()
pedido.agregar_item(menu[0])  # Coca Cola
pedido.agregar_item(menu[3])  # Papas Fritas
pedido.agregar_item(menu[6])  # Hamburguesa

# Calcular total del pedido
total = pedido.calcular_total()
print(f"Total del pedido: ${total:.2f}")
```
