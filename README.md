entradas = {}
stock_total = 330

stock = {
    1: {"nombre": "Cats día Viernes", "disponibles": 150, "vendidas": 0},
    2: {"nombre": "Cats día Sábado", "disponibles": 180, "vendidas": 0}
}

def comprar_entrada():
    print("\n----- Comprar entrada a Cats -----")
    nombre = input("Nombre del comprador: ").strip()

    if nombre in entradas:
        print("Error: El comprador ya tiene una entrada registrada.")
        return
    print("\nSeleccione función:")
    print("1. Cats día Viernes (150 entradas)")
    print("2. Cats día Sábado (180 entradas)")
    try:
        función = int(input("Función (1 ó 2): "))
    except ValueError:
        print("Error: opción de función inválida.")
        return
    if función not in (1, 2):
        print("Error: opción de función inválida.")
        return
    if stock[función]["disponibles"] > 0:
        stock[función]["disponibles"] -= 1
        stock[función]["vendidas"] += 1
        entradas[nombre] = función
        print(f"\nEntrada registrada en función {función}! Stock restantes:")
        mostrar_stock()
    else:
        print("No hay stock disponible para esta función.")

def cambio_función():
    print("\n----- Cambio de función -----")
    nombre = input("Nombre del comprador: ").strip()
    if nombre not in entradas:
        print("Error: comprador no encontrado.")
        return
    actual = entradas[nombre]
    nueva = 2 if actual == 1 else 1
    confirmacion = input(f"Cambiar de función {actual} a {nueva}? (S/N): ").lower()
    if confirmacion != 's':
        print("Cambio cancelado.")
        return
    if stock[nueva]["disponibles"] > 0:
        stock[actual]["disponibles"] += 1
        stock[actual]["vendidas"] -= 1
        stock[nueva]["disponibles"] -= 1
        stock[nueva]["vendidas"] += 1
        entradas[nombre] = nueva
        print(f"Cambio exitoso. Ahora está en función {nueva}.")
    else:
        print("No hay stock disponible en la nueva función.")

def mostrar_stock():
    print("\n----- Stock de Funciones -----")
    for num, datos in stock.items():
        print(f"Función {num} ({datos['nombre'].split()[-1]}): Disponibles {datos['disponibles']}, Vendidas {datos['vendidas']}")

def main():
    while True:
        print("\n----- TOTEM AUTOATENCIÓN CAFECONLECHE -----")
        print("1.- Comprar entrada a Cats.")
        print("2.- Cambio de función.")
        print("3.- Mostrar stock de funciones.")
        print("4.- Salir.")
        opcion = input("Seleccione una opción: ").strip().lower()
        if opcion == '1':
            comprar_entrada()
        elif opcion == '2':
            cambio_función()
        elif opcion == '3':
            mostrar_stock()
        elif opcion == '4':
            print("\nPrograma terminado...")
            break
        else:
            print("\nDebe ingresar una opción válida!!")

main()
