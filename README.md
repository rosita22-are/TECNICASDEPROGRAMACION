# TECNICASDEPROGRAMACION
 Ejemplos de Técnicas de Programación  Este repositorio contiene ejemplos prácticos de las principales técnicas de programación vistas en clase:  - **Abstracción** - **Encapsulación** - **Herencia** - **Polimorfismo**  Cada técnica incluye un archivo Java con un ejemplo simple y funcional.   📁 Estructura del Repositorio
class Personaje:
    def __init__(self, nombre, ataque, defensa, vida):
        self.nombre = nombre
        self._ataque = ataque
        self._defensa = defensa
        self._vida = vida

    # Encapsulación
    @property
    def vida(self):
        return self._vida

    @vida.setter
    def vida(self, valor):
        if valor < 0:
            self._vida = 0
        else:
            self._vida = valor

    def atributos(self):
        print(f"\n{self.nombre}")
        print(f"Ataque: {self._ataque}")
        print(f"Defensa: {self._defensa}")
        print(f"Vida: {self._vida}")

    def esta_vivo(self):
        return self._vida > 0

    def morir(self):
        print(f"{self.nombre} ha muerto.")

    # Polimorfismo
    def calcular_daño(self, enemigo):
        return self._ataque - enemigo._defensa

    def atacar(self, enemigo):
        daño = self.calcular_daño(enemigo)

        if daño < 0:
            daño = 0

        enemigo.vida -= daño
        print(f"{self.nombre} ha hecho {daño} puntos de daño a {enemigo.nombre}.")

        if not enemigo.esta_vivo():
            enemigo.morir()


class Arquero(Personaje):
    def __init__(self, nombre, ataque, defensa, vida, precision):
        super().__init__(nombre, ataque, defensa, vida)
        self.precision = precision

    def atributos(self):
        super().atributos()
        print(f"Precisión: {self.precision}")

    def calcular_daño(self, enemigo):
        return (self._ataque * self.precision) - enemigo._defensa


class Paladin(Personaje):
    def __init__(self, nombre, ataque, defensa, vida, bendicion):
        super().__init__(nombre, ataque, defensa, vida)
        self.bendicion = bendicion

    def atributos(self):
        super().atributos()
        print(f"Bendición: {self.bendicion}")

    def calcular_daño(self, enemigo):
        return self._ataque + self.bendicion - enemigo._defensa

    def atacar(self, enemigo):
        super().atacar(enemigo)
        self.vida += 2
        print(f"{self.nombre} se cura 2 puntos. Vida actual: {self.vida}")


def combate(j1, j2):
    ronda = 1
    print("Comienza el combate")

    while j1.esta_vivo() and j2.esta_vivo():
        print(f"\nRonda {ronda}")

        j1.atacar(j2)
        if not j2.esta_vivo():
            break

        j2.atacar(j1)
        ronda += 1

    print("\nFin del combate")
    if j1.esta_vivo():
        print(f"Ganador: {j1.nombre}")
    else:
        print(f"Ganador: {j2.nombre}")


# Ejemplo de uso
arquero = Arquero("Legolas", ataque=15, defensa=4, vida=90, precision=2)
paladin = Paladin("Uther", ataque=10, defensa=8, vida=120, bendicion=5)

arquero.atributos()
paladin.atributos()

combate(arquero, paladin)
