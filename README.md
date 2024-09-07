# ¡Hola y bienvenidos al repositorio oficial de clases CR2! 🎉

👉 **Recomendación:** Instala lo que se indica en el README para usar correctamente los códigos del proyecto. De lo contrario, no se garantiza su funcionamiento. Sin embargo, puedes leer todo sin problema. 📖

- [Lee el README aquí](/src/modules/1-entorno_virtual/README.md) 📚

## Recursos 📚

- [Snippets de código](/src/utils/snippets.ipynb) 📦

## QR del repositorio
<div style="text-align: center;">
  <img src="./public/repo-qr.png" alt="QR del repositorio" width="300"/>
</div>

# Snippets de Código para tu Robot con `cyberpi` y `mbot2`

## 1. Librerías
```python
import cyberpi as cy
from cyberpi import mbot2 as m
import time
```

## 2. Movimientos de Motores

### Ajustar la velocidad de los motores
```python
def ajustar_motores(velocidad_izquierda: int, velocidad_derecha: int):
    """
    Ajusta las velocidades de los motores.
    
    @param velocidad_izquierda (int): Velocidad del motor izquierdo.
    @param velocidad_derecha (int): Velocidad del motor derecho.
    """
    m.drive_power(velocidad_izquierda, velocidad_derecha)
```

### Detener el robot
```python
def detener_robot():
    """
    Detiene el robot.
    """
    m.drive_power(0, 0)
```

### Ajustar motores por un tiempo específico
```python
def ajustar_motores_durante(velocidad_izquierda: int, velocidad_derecha: int, tiempo: float):
    """
    Ajusta las velocidades de los motores durante un tiempo específico.
    
    @param velocidad_izquierda (int): Velocidad del motor izquierdo.
    @param velocidad_derecha (int): Velocidad del motor derecho.
    @param tiempo (float): Tiempo en segundos durante el cual los motores funcionarán.
    """
    ajustar_motores(velocidad_izquierda, velocidad_derecha)
    time.sleep(tiempo)
    detener_robot()
```

## 3. Sensor Ultrasonido

### Obtener la distancia del sensor
```python
def obtener_distancia(sensor_index=1):
    """
    Obtener la distancia del sensor ultrasónico.
    
    @param sensor_index: Índice del sensor ultrasónico a usar.
    """
    return cy.ultrasonic2.get(sensor_index)
```

### Imprimir la distancia del sensor
```python
def obtener_distancia_imprimir():
    """
    Obtener la distancia del sensor ultrasónico y mostrarla en la consola.
    """
    cy.console.log(obtener_distancia())
```

### Activar motores si la distancia es mayor a 10 cm
```python
def obtener_distancia_activar_motor():
    """
    Activar los motores si la distancia es mayor a 10 cm.
    """
    while True:
        distancia = obtener_distancia()
        if distancia > 10:
            ajustar_motores(50, -50)
        else:
            detener_robot()
        cy.console.log(distancia)
```

### Encender luces en el sensor de ultrasonido
```python
def luces_ultrasonido(emotion):
    """
    Encender las luces del sensor de ultrasonido según una emoción específica.
    
    @param emotion: Emoción a utilizar (sleepy, happy, dizzy, wink, thinking).
    """
    cy.ultrasonic2.play(emotion, index=1)
```

## 4. Eventos

### Función principal
```python
def main():
    """
    Función principal.
    """
    pass
```

### Iniciar función principal al presionar un botón
```python
@cy.event.is_press("a")
def start_main():
    """
    Inicia la función principal al presionar el botón 'a'.
    """
    main()
```

### Recibir un evento
```python
@cy.event.receive("funcion_receive")
def funcion_receive():
    """
    Función para recibir el evento 'funcion_receive'.
    """
    pass
```

### Enviar un evento
```python
def funcion_broadcast():
    """
    Función para enviar el evento 'funcion_receive'.
    """
    cy.broadcast("funcion_receive")
```

## 5. Seguidor de Líneas

### Seguir una línea
```python
def seguir_linea(velocidad_base: int = 40):
    """
    Controla el movimiento del robot basado en la desviación del sensor de línea.
    
    @param velocidad_base (int): Velocidad base de los motores.
    """
    offset = cy.quad_rgb_sensor.get_offset_track(index=1)
    factor = (offset / 2) * -1
    
    motor_derecho = velocidad_base - factor
    motor_izquierdo = velocidad_base + factor
    
    m.drive_speed(motor_izquierdo, -motor_derecho)
```

### Romper un ciclo de seguimiento de línea
```python
def main():
    """
    Función principal.
    """
    while True:
        seguir_linea()
        if obtener_distancia() < 10:
            ajustar_motores(0, 0)
            break
```

## 6. Servomotores

### Mover un servomotor
```python
def mover_servo(posicion: int, motor_index: int = 1):
    """
    Mover el servomotor a una posición específica.
    
    @param posicion (int): Posición a la que se moverá el servo.
    @param motor_index (int): Índice del motor al que se moverá el servo.
    """
    m.servo_set(posicion, motor_index)
```

## 7. Luces LED

### Ajustar el color de los LEDs
```python
def ajustar_led(red: int = 0, green: int = 0, blue: int = 0):
    """
    Ajustar el color de los LEDs.
    
    @param red (int): Valor de intensidad del color rojo.
    @param green (int): Valor de intensidad del color verde.
    @param blue (int): Valor de intensidad del color azul.
    """
    cy.led.on(red, green, blue)
```

### Ajustar el color de los LEDs con animación
```python
def ajustar_led_animado(animation: str = "rainbow"):
    """
    Ajustar el color de los LEDs de forma animada.
    
    @param animation (str): Nombre de la animación a mostrar.
    """
    cy.led.play(animation)
```
