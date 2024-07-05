# Uso

Para utilizar o somador de 4 bits com carry, siga as instruções abaixo:

1. Conecte os pinos de entrada conforme especificado no código.
2. O bit de carry é inicializado e atualizado automaticamente pelo código.
3. O resultado da soma será exibido nos pinos de saída especificados.

Os pinos utilizados são:

- Entradas: 0 a 7
- Saídas: 8 a 12

## Código Completo (for nerds): 
```
int sum = 13; 
int carry Bit = 0; 
int nib1a, nib1b, nib1c, nib1d = 0; 
int nib2a, nib2b, nib2c, nib2d = 0; 
int res1a, res1b, res1c, res1d = 0;

empty configuration() {
 pinMode(0, INPUT); 
 pinMode(1, INPUT); 
 pinMode(2, INPUT); 
 pinMode(3, INPUT); 
 pinMode(4, INPUT);
 pinMode(5, INPUT); 
 pinMode(6, INPUT); 
 pinMode(7, INPUT); 
 pinMode(8, OUTPUT); 
 pinMode(9, OUTPUT); 
 pinMode(10, OUTPUT); 
 pinMode(11, OUTPUT); 
 pinMode(12, OUTPUT); 
 pinMode(13, INPUT);
}

int sumBit(int b1a, int b2a, int cBit) {
 int bitResult = 0; 
 int aux1, aux2 = 0; 
 
 if ((b1a ^ b2a) ^ cBit) {
 bitResult = 1;
 } other {
 bitResult = 0;
 }
 return bitResult; //Returns the result of the sum
}

int sumCarryBit(int b1a, int b2a, int cBit) {
 int aux1, aux2 = 0; //Auxiliary variables (unused)

 if ((b1a && b2a) || (b1a && cBit) || (b2a && cBit)) {
 cBit = 1;
 } other {
 cBit = 0;
 }
 return cBit; //Returns the carry bit
}
empty loop() {
 sum = digitalRead(13);
 nib1a = digitalRead(0);
 nib1b = digitalRead(1);
 nib1c = digitalRead(2);
 nib1d = digitalRead(3);
 nib2a = digitalRead(4);
 nib2b = digitalRead(5);
 nib2c = digitalRead(6);
 nib2d = digitalRead(7);
 if (sum == 1) {
 carryBit = 0;
 
 res1a = sumBit(nib1a, nib2a, carryBit);
 carryBit = sumCarryBit(nib1a, nib2a, carryBit);
 res1b = sumBit(nib1b, nib2b, carryBit);
 carryBit = sumCarryBit(nib1b, nib2b, carryBit);
 res1c = sumBit(nib1c, nib2c, carryBit);
 carryBit = sumCarryBit(nib1c, nib2c, carryBit);
 res1d = sumBit(nib1d, nib2d, carryBit);
 carryBit = sumCarryBit(nib1d, nib2d, carryBit);
 }
 digitalWrite(8, res1a);
 digitalWrite(9, res1b);
 digitalWrite(10, res1c);
 digitalWrite(11, res1d);
 digitalWrite(12, carryBit);
}
```
