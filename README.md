# ARQUITECTURA-DEL-COMPUTADOR
## PROYECTO FINAL
### REVISION PROYECTO FINAL ARQUITECTURA Y ORGANIZACION DEL COMPUTADOR


+ GRUPO:
+ JUAN MARTÍN SÁNCHEZ
+ DANIEL GALVIS
+ SANTIAGO CAMARGO

LINK VIDEO: https://youtu.be/xgqnusrN6qo


```
CODIGO ALGORITMO BOOTH:
; Variables
vauxi:0b00000000
A:0b00000000
M:0b00010000
Q:0b01100000
Q1:0b00000000
N:0b00000100
bit_menos_signi_A:0b00000000 ; Bit menos significativo de A
product:0 ; Producto de la multiplicación

; Inicio del programa
START:
    JMP CTE 
    ALGORITMO_BOOTH ; Salto al inicio del algoritmo de Booth

ALGORITMO_BOOTH:
    MOV ACC, N ; Cargar N en ACC
    MOV A, ACC ; Copiar ACC a A
    MOV ACC, 0b00000001 ; Inicializar el bit menos significativo
    AND ACC, A ; Verificar el bit menos significativo de N
    JZ CTE 
    FIN        ; Si es 0 fin del programa
    ; Inicializar el producto y otros registros
    MOV product, 0 ; Inicializar el producto
    MOV bit_menos_signi_A, 0 ; Inicializar el bit menos significativo de A
    
booth_loop:
    ; Desplazamiento a la derecha del multiplicando (Q) y del producto
    RSH ACC CTE 1 ; Desplazamiento aritmético a la derecha de ACC (Q >> 1)
    RSH ACC CTE product ; Desplazamiento aritmético a la derecha del producto
    ; Verificar los dos bits menos significativos de Q
    MOV ACC, Q ; Cargar Q en ACC
    MOV A, ACC ; Copiar ACC a A
    AND ACC, A ; Q AND 0b11
    ; Saltar a las operaciones correspondientes según el resultado
    JZ CTE 
    booth_no_add ; Si Q AND 0b11 es 0, no sumar
    JC CTE 
    booth_add ; Si Q AND 0b11 tiene carry, sumar
    
booth_no_add:
    ; Continuar con otras operaciones si no se suma
    JMP CTE 
    booth_loop ; Volver al bucle principal

booth_add:
    ; Sumar el multiplicando (M) al producto
    MOV ACC, M ; Cargar M en ACC
    ADD ACC, A ; Sumar M a A
    MOV A, ACC ; Copiar ACC a A
    ; Actualizar el producto
    MOV ACC, product ; Cargar el producto en ACC
    ADD ACC, A ; Sumar el resultado anterior al producto
    MOV product, ACC ; Actualizar el producto
    ; Continuar con otras operaciones
    JMP CTE 
    booth_loop ; Volver al bucle principal
FIN:
    HLT  ;Fin del programa
```
