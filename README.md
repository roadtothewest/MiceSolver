# MiceSolver

📋 Lista de tareas por hacer / diseñar

1. Elegir la batería adecuada
   - Tipo (LiPo, LiFePO4, Li-Ion)
   - Capacidad vs. peso
   - Voltaje de operación
2. Elegir el Microcontrolador (MCU)
   - Comparar precisión, velocidad y consumo
   - Selección preliminar: STM32 vs Arduino Nano (prototipo)
3. Elegir sensores IR
   - Definir cantidad, posición y diseño del módulo IR
4. Elegir motores + drivers + encoders
   - Evaluar precisión, velocidad y eficiencia
   - Considerar encoders magnéticos/ópticos
5. Diseñar el módulo de potencia (Powerbank)
   - Buck Converter (3.3V / 5V seleccionable según MCU y sensores)
   - Filtrado de ruido (bypass, ferrita, capacitores)
6. Diseñar la lógica de control en firmware
   - Control por PWM
   - Algoritmo de resolución/aprendizaje del laberinto
7. Leer e integrar las reglas oficiales
   - IEEE Micromouse Rules 2020

⚙️ Componentes y tecnologías consideradas

🔋 Batería

Opción más probable (conveniente para etapa de velocidad):
- LiPo 3S (11.1V - 12.6V), ej: Tattu 950mAh 75C
  - Tamaño: ~70x35x20mm
  - Peso: 100g - 150g
  - Ideal para motores pequeños y electrónica ligera

Otras opciones evaluadas:
- LiFePO4 4S (12.8V - 14.6V)
  - Más estable, segura y duradera
  - Más pesada
- Li-Ion 3S (11.1V - 12.6V)
  - Más compacta y liviana
  - Mejor para electrónica, menor tasa de descarga

🧠 Microcontrolador (MCU)

| MCU           | Frecuencia | Notas                                   |
|---------------|------------|------------------------------------------|
| Arduino Nano  | 16 MHz     | FTDI incorporado, útil para prototipo     |
| STM32F407/F446| 168 MHz    | Alta precisión, ideal para control PWM    |
| STM32F746/H7  | 400 MHz    | Muy potente, puede ser overkill          |

Comentario: Usar Arduino Nano solo como prototipo. Para competencia, se prefiere STM32 por su mayor control temporal y precisión en PWM.

🔧 Drivers de motor

Preferencia:
- TB67H420 o DRV8871
  - Conectados directamente a la batería
  - Bypass de 100–470μF LOW ESR (para evitar picos)

Alternativas:
- MP230 o LM2596
  - Incluir ferrita o bypass LOW ESR para filtrar el ruido de alta frecuencia (conmutaciones a 20-40kHz)

🌀 Motores y encoders

- Ideal: motores con encoder magnético u óptico
- Evaluar en función de precisión mínima requerida para las altas velocidades post-aprendizaje
- Control por PWM será más preciso con STM32 (incluso modelos de 80 MHz son suficientes)

🌐 Sensores IR

- Aún por definir cantidad y tipo
- Se debe diseñar módulo IR completo (posición, amplificación, acondicionamiento)

⚡ Regulación de voltaje / Buck Converter

- Conversión a 3.3V o 5V según la alimentación requerida por MCU y sensores
- Afecta directamente la alimentación y el nivel lógico de 1 para componentes

🧱 Restricciones del robot

- Tamaño máximo permitido: 25 cm x 25 cm
- Por lo tanto, la batería y todos los módulos deben ser livianos y compactos

🔗 Recursos

- Manual STM32F446:
  https://www.st.com/resource/en/reference_manual/rm0390-stm32f446xx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf
- Reglas Micromouse IEEE:
  https://attend.ieee.org/r2sac-2020/wp-content/uploads/sites/175/2020/01/MicroMouse_Rules_2020.pdf
