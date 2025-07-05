# Definición de la Clase Base: Vehiculo
# Esta clase representa un vehículo genérico con atributos básicos.
class Vehiculo:
    def __init__(self, marca, modelo, anio):
        self.marca = marca      # Atributo público
        self.modelo = modelo    # Atributo público
        self.anio = anio        # Atributo público

    def describir(self):
        """Método que describe el vehículo."""
        return f"Marca: {self.marca}, Modelo: {self.modelo}, Año: {self.anio}"

    def encender(self):
        """Método genérico para encender el vehículo."""
        return "El vehículo ha sido encendido."

# ---

# Definición de la Clase Derivada: Coche
# La clase Coche hereda de Vehiculo y añade atributos y métodos específicos,
# además de implementar encapsulación y polimorfismo.
class Coche(Vehiculo):
    def __init__(self, marca, modelo, anio, color, _velocidad_maxima):
        # Llama al constructor de la clase base (Vehiculo)
        super().__init__(marca, modelo, anio)
        self.color = color  # Atributo público
        # Encapsulación: _velocidad_maxima es un atributo "protegido" (por convención)
        # Esto indica que no debería ser accedido directamente desde fuera de la clase.
        self._velocidad_maxima = _velocidad_maxima

    # Polimorfismo por sobrescritura de método:
    # El método encender() de Coche sobrescribe al de Vehiculo.
    def encender(self):
        """Método específico para encender un coche."""
        return "El coche ruge al encenderse. ¡Listo para la carretera!"

    def describir_coche(self):
        """Método que describe el coche con sus atributos específicos."""
        # Se reutiliza el método describir de la clase base para la información común.
        return f"{super().describir()}, Color: {self.color}, Velocidad Máxima (interna): {self._velocidad_maxima} km/h"

    # Encapsulación: Métodos "getter" y "setter" para acceder/modificar _velocidad_maxima
    def get_velocidad_maxima(self):
        """Método para obtener la velocidad máxima (ejemplo de getter)."""
        return self._velocidad_maxima

    def set_velocidad_maxima(self, nueva_velocidad):
        """Método para establecer una nueva velocidad máxima (ejemplo de setter)."""
        if nueva_velocidad > 0:
            self._velocidad_maxima = nueva_velocidad
            return f"Velocidad máxima actualizada a {nueva_velocidad} km/h."
        else:
            return "La velocidad máxima debe ser un valor positivo."

# ---

# Demostración de las Clases y Conceptos de POO

print("--- Demostración de Vehiculo (Clase Base) ---")
# Creación de una instancia de la clase Vehiculo (Objeto)
mi_bicicleta = Vehiculo("BMX", "Street", 2023)
print(mi_bicicleta.describir())
print(mi_bicicleta.encender())
print("-" * 40)

print("--- Demostración de Coche (Clase Derivada) ---")
# Creación de una instancia de la clase Coche (Objeto)
mi_coche = Coche("Toyota", "Corolla", 2024, "Rojo", 180)
print(mi_coche.describir_coche())
print(mi_coche.encender()) # Demostración de polimorfismo (método sobrescrito)
print("-" * 40)

print("--- Demostración de Encapsulación en Coche ---")
# Acceso al atributo encapsulado a través de un "getter"
print(f"Velocidad máxima inicial del coche: {mi_coche.get_velocidad_maxima()} km/h")

# Modificación del atributo encapsulado a través de un "setter"
print(mi_coche.set_velocidad_maxima(200))
print(f"Nueva velocidad máxima del coche: {mi_coche.get_velocidad_maxima()} km/h")

# Intento de modificar con un valor inválido
print(mi_coche.set_velocidad_maxima(-50))
print("-" * 40)

print("--- Demostración Adicional de Polimorfismo (Argumentos variables) ---")
# Polimorfismo a través de funciones que pueden manejar diferentes tipos de objetos.
# Aunque no es polimorfismo de métodos sobrescritos, esta función puede operar
# con cualquier objeto que tenga un método 'encender()'.
def arrancar_vehiculo(vehiculo_a_arrancar):
    print(f"Intentando arrancar: {vehiculo_a_arrancar.describir()}")
    print(vehiculo_a_arrancar.encender())

print("\nArrancando la bicicleta:")
arrancar_vehiculo(mi_bicicleta)

print("\nArrancando el coche:")
arrancar_vehiculo(mi_coche)
print("-" * 40)
