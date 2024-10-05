```python
# Hola mundo 2

import cyberpi
from cyberpi import mbot2
import time


# FUNCIONES DEL REPOSITORIO

def seguir_linea(velocidad_base: int = 40):
    offset = cyberpi.quad_rgb_sensor.get_offset_track(index=1)
    factor = (offset / 2) * -1
    
    motor_derecho = velocidad_base - factor
    motor_izquierdo = velocidad_base + factor
    
    mbot2.drive_speed(motor_izquierdo, -motor_derecho)

def obtener_distancia(sensor_index=1):
    return cyberpi.ultrasonic2.get(sensor_index)

def encender_led(color: str = "red", intervalo: int = 0):
    cyberpi.led.on(color, "all")
    
    if (intervalo != 0):
        time.sleep(intervalo)
        cyberpi.led.off()

# FIN CODIGOS REPOSITORIO

VELOCIDAD_SL_GLOBAL = 40

def main():
    global VELOCIDAD_SL_GLOBAL
    while True:
        # (1) Seguir la linea
        seguir_linea(VELOCIDAD_SL_GLOBAL)
        
        # (2) Obtener la distancia del sensor ultrasonido
        distancia_obtenida = obtener_distancia()
        
        # (3.1) ¿La distancia es menor a 8?
        if (distancia_obtenida < 8):
            VELOCIDAD_SL_GLOBAL = 0
            encender_led("r")
        
        # (3.2) ¿La distanca esta entre 8 y 15?
        elif (distancia_obtenida < 15):
            VELOCIDAD_SL_GLOBAL = 20
            encender_led("y")
        
        # (3.3) No se cumple ninguna condicion
        else :
            VELOCIDAD_SL_GLOBAL = 40
            encender_led("g")
            
# Hola mundo 2

import cyberpi
from cyberpi import mbot2
import time


# FUNCIONES DEL REPOSITORIO

def seguir_linea(velocidad_base: int = 40):
    offset = cyberpi.quad_rgb_sensor.get_offset_track(index=1)
    factor = (offset / 2) * -1
    
    motor_derecho = velocidad_base - factor
    motor_izquierdo = velocidad_base + factor
    
    mbot2.drive_speed(motor_izquierdo, -motor_derecho)

def detectar_color(sensor_index = 1) -> str:
    return cyberpi.quad_rgb_sensor.get_color_sta(2, sensor_index)

def mover_servomotor(angulo: int = 90, puerto: int = 3, intervalo: int = 0):
    
    mbot2.servo_set(angulo, puerto)
    time.sleep(intervalo)

# FIN CODIGOS REPOSITORIO

MOVER_SERVOMOTOR_GLOBAL = False

def girar_360():
    mbot2.drive_power(20, 20)
    time.sleep(1.5)
    mbot2.drive_power(0, 0)
    
def girar_180():
    mbot2.drive_power(20, 20)
    time.sleep(0.75)
    mbot2.drive_power(0, 0)

# Servomotor de la mano
@cyberpi.event.receive("servomotor")
def servomotor_primero(): 
    
    global MOVER_SERVOMOTOR_GLOBAL
    
    lista_angulos = [170, 90, 100]
    
    while True:
        for angulo in lista_angulos:
            mover_servomotor(angulo, 4, 0.5)
        
        if (not MOVER_SERVOMOTOR_GLOBAL):
            break

# Servomotor del brazo
@cyberpi.event.receive("servomotor")
def servomotor_segundo():
    
    global MOVER_SERVOMOTOR_GLOBAL
    
    lista_angulos = [60, 110, 30]
    
    while True:
        for angulo in lista_angulos:
            mover_servomotor(angulo, 3, 0.5)
            
        if (not MOVER_SERVOMOTOR_GLOBAL):
            break

@cyberpi.event.receive("servomotor")
def servomotor_termino():
    global MOVER_SERVOMOTOR_GLOBAL
    
    time.sleep(5)
    
    MOVER_SERVOMOTOR_GLOBAL = False

def main():
    while True:
        
        global MOVER_SERVOMOTOR_GLOBAL
        
        # (1) Seguimos lineas
        seguir_linea()
        
        # (2) Detectamos los colores
        color_detectado = detectar_color()
        
        # (3) Tomamos decisiones
        
        # (3.1) ¿Estoy detectando rojo?
        if (color_detectado == "red"):
            girar_360()
            # * Otras funciones
        
        # (3.2) ¿Estoy detectando amarillo?
        if (color_detectado == "yellow"):
            girar_180()
        
        # (3.3) ¿Estoy detectando verde?
        if (color_detectado == "green"):
            MOVER_SERVOMOTOR_GLOBAL = True
            
            cyberpi.broadcast("servomotor")
            
@cyberpi.event.is_press("a")
def event_is_press_a():
    main()
```