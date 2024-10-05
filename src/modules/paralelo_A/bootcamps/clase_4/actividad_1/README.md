```python
# Hola mundo

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
            
@cyberpi.event.is_press("a")
def event_is_press_a():
    main()
```