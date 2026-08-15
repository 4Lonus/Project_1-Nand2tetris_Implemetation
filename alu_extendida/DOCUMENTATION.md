# Documentación de la ALU Extendida
La ALU Extendida, es un tipo de CHIP que en palabras simples envuelve a la ALU normal en una ALU con funciones extra y una señal para activarlas (la entrada `a`).

## Estructura del CHIP
### Entradas
- x [16]
- y [16]
- a
- zx
- nx
- zy
- ny
- f
- no

### Salidas
- out [16]
- zr
- ng

### Proceso
1. Se realiza el proceso normal de la ALU, pero esta vez, antes de enviar la salida, guardamos dicha salida en una "variable" (o simple conección, a nivel de circuito, lo llamaremos `outALU`).
2. Realizamos los procesos alternos, XOR, NAND, NOR, EQ (igualdad) & ABS (valor absoluto), y guardamos cada una de dichas operaciones en su propia variable.
3. De acuerdo a los codigos propuestos para cada funcion extra, decidimos que variable elejimos a travez de una serie de Multiplexores, y el resultado final lo almacenamos en su propia variable (`outALUext`).
4. Entonces, a través de la entrada `a` decidimos, con un Multiplexor cual entrada dejar salir; ya sea la ALU normal (`outALU`) o la extendida (`outALUext`).
5. Por ultimo, procesamos las salidas extras de la misma manera que en la ALU normal (con dos 8-way-OR unidos por un Or psteriormente negado para el zr, o indicando el MSB como ng).

## Tabla de Operaciones

| Operación | Codigo (zx-nx-zy-ny-f-no) |
| --- | :---: |
| x XOR y | 010110 |
| !(x AND y) | 000001 |
| !(x OR y) | 110100 |
| if x==y then 1, else 0 | 101000 |
| \|x\| | 100010 |

## Testing
Todos los ejemplos que se sugirieron en el trabajo original fueron probados y sus resultados se muestran en los recortes de pantallazos en esta misma carpeta.

## Otras Consideraciones
Para esta modificaion de la ALU, hice una supocision de que la entrada `a` serviría para elejir la ALU normal o extendida.