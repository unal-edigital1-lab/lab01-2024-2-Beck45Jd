# lab01- sumador 
## Juan David Saldaña E

## Informe de Laboratorio 

### Sumador de 1 Bit

#### Entregable 1
```Verilog
module sum1bcc_primitive (A, B, Ci,Cout,S);
  //Se definen las entradas
  input  A;
  input  B;
  input  Ci;***

  //Se definen las salidas
  output Cout;
  output S;

  //Se definen los cables para conexiones
  wire a_ab;
  wire x_ab;
  wire cout_t;

  //Se definen compuertas lógicas: <Tipo_de_Compuerta>(Salida, Entrada 1, Entrada 2)
  and(a_ab,A,B);
  xor(x_ab,A,B);

  xor(S,x_ab,Ci);
  and(cout_t,x_ab,Ci);

  or (Cout,cout_t,a_ab);

endmodule
```
#### Entregable 2
```Verilog
module sum1bcc (A, B, Ci,Cout,S);
  //Definimos Entradas
  input  A;
  input  B;
  input  Ci;

  //Definimos Salidas
  output Cout;
  output S;

  reg [1:0] st;   // Registro que guarda el resultado de suma 
  assign S = st[0]; // Salida asignada para el Bit menos significativo. 
  assign Cout = st[1]; // Salida asignada para el Bit más signficativo.

  //Bloque de Operación para el Sumador 
  always @ ( * ) begin
  	st  = 	A+B+Ci;
  end
  
endmodule
```
Diferencias entre códigos:
Para el primer modelo del sumador, se puede notar que usamos elementos como cables y compuertas lógicas para la operación que necesitamos. Mientras que el siguiente modelo se trabaja con una simplificación del problema, usando un bloque de sensibilidad completa (incluye todas las señales de entrada), que se ejecuta siempre que cambie cualquiera de las señales que afectan su comportamiento.


#### Entregable 3
Sum1bcc_primitive
![Imagen de WhatsApp 2025-01-02 a las 18 20 50_5ea21cb8](https://github.com/user-attachments/assets/c40a4748-570f-49bd-b2cf-35ae51788a4d)

Sum1bcc
![Imagen de WhatsApp 2025-01-02 a las 18 28 29_8b435c32](https://github.com/user-attachments/assets/e02b3342-f4ce-42f7-947a-eecaa4b63a97)

Como podemos ver en la simulación, los resultados son los esperados. Ambos modelos funcionan correctamente y arrojan resultados correctos que se pueden visualizar en la siguiente tabla de verdad:

| A | B | Cin | S | Cout |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |
