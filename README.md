# Arquitectura de Computadores  
## Unidad 3: Manejo del DEBUG — Post-Contenido 2  
### Ingeniería de Sistemas — 2026  

---

## Descripción del laboratorio

En este laboratorio se utilizó el programa DEBUG dentro de DOSBox para practicar el ensamblado de instrucciones directamente en memoria y su ejecución paso a paso. El objetivo fue entender cómo cambian los registros del procesador durante la ejecución de un programa, cómo se modifican las banderas y cómo funciona un bucle usando la instrucción LOOP.

Se trabajaron dos programas principales: una suma simple con registros y un programa con bucle controlado por CX. Además, se usó la ejecución paso a paso con el comando T para observar el comportamiento del procesador.

---

# Parte A — Programa de suma

Se ensambló un programa que realiza operaciones básicas entre registros:

asm
MOV AX, 000A
MOV BX, 0005
MOV CX, 0003
ADD AX, BX
ADD AX, CX
INT 20

Este programa permite ver cómo AX cambia después de cada operación.

Tabla de traza — Programa de suma

Tabla de traza — Programa de suma

| Instrucción | AX   | BX   | CX   | IP siguiente | ZF | CF | SF |
| ----------- | ---- | ---- | ---- | ------------ | -- | -- | -- |
| MOV AX,000A | 000A | 0000 | 0000 | 0103         | 0  | 0  | 0  |
| MOV BX,0005 | 000A | 0005 | 0000 | 0106         | 0  | 0  | 0  |
| MOV CX,0003 | 000A | 0005 | 0003 | 0109         | 0  | 0  | 0  |
| ADD AX,BX   | 000F | 0005 | 0003 | 010B         | 0  | 0  | 0  |
| ADD AX,CX   | 0012 | 0005 | 0003 | 010D         | 0  | 0  | 0  |
| INT 20      | 0012 | 0005 | 0003 | ----         | -  | -  | -  |


Checkpoint 1

Captura: capturas/CP1_traza_suma.png

Observaciones:

AX inicia en 000A.
Se incrementa primero con BX y luego con CX.
El resultado final es AX = 0012.
Las banderas cambian dependiendo del resultado de cada operación.
Parte B — Programa con bucle LOOP

Se utilizó un bucle controlado por CX para repetir una suma de 2 en 2:

MOV AX, 0000
MOV CX, 0004
ADD AX, 0002
LOOP 0106
INT 20

El objetivo fue observar cómo CX disminuye en cada iteración y cómo LOOP regresa a la instrucción ADD.

Tabla de traza — Bucle LOOP

Checkpoint 2

Captura: capturas/CP2_traza_loop.png

Observaciones:

CX se decrementa en cada iteración.
LOOP controla el ciclo del programa.
AX aumenta progresivamente hasta 0008.
Cuando CX llega a 0, el programa termina.
Parte C — Análisis de código máquina

Se utilizó el comando D en DEBUG para observar cómo las instrucciones se representan en memoria.

Se identificó que:

MOV usa 3 bytes
ADD usa 3 bytes
LOOP usa 2 bytes
INT 20 usa 2 bytes

Esto permitió entender la relación entre ensamblador y código máquina.

Conclusión

Este laboratorio ayudó a entender cómo funciona la ejecución de instrucciones a nivel de procesador. Usando DEBUG se pudo observar cómo cambian los registros en tiempo real y cómo el sistema ejecuta instrucciones paso a paso.

También se entendió cómo funciona un bucle a nivel de máquina y cómo el registro CX controla la repetición de instrucciones con LOOP.

En general, fue una práctica útil para comprender mejor la arquitectura interna del procesador.

Estructura del repositorio
apellido-post2-u3/
│
├── README.md
└── capturas/
    ├── CP1_traza_suma.png
    └── CP2_traza_loop.png
