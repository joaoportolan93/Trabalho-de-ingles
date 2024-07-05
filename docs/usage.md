# Uso

Para utilizar o somador de 4 bits com carry, siga as instruções abaixo:

1. Conecte os pinos de entrada conforme especificado no código.
2. O bit de carry é inicializado e atualizado automaticamente pelo código.
3. O resultado da soma será exibido nos pinos de saída especificados.

Os pinos utilizados são:

- Entradas: 0 a 7
- Saídas: 8 a 12

## Código Completo (for nerds): 
//Variable declarations
int sum = 13; // Pin for sum operation trigger
int carry Bit = 0; // Variable to store the carry bit
int nib1a, nib1b, nib1c, nib1d = 0; // Variables to store the first 4-bit number
int nib2a, nib2b, nib2c, nib2d = 0; // Variables to store the second 4-bit number
int res1a, res1b, res1c, res1d = 0; // Variables to store the result of the 4-bit sum

//Configuration function to initialize the pins
empty configuration() {
 pinMode(0, INPUT); //First bit of first number
 pinMode(1, INPUT); // Second bit of the first number
 pinMode(2, INPUT); // Third bit of the first number
 pinMode(3, INPUT); //Fourth bit of the first number
 pinMode(4, INPUT); //First bit of second number
 pinMode(5, INPUT); 
 pinMode(6, INPUT); 
 pinMode(7, INPUT); 
 pinMode(8, OUTPUT); 
 pinMode(9, OUTPUT); 
 pinMode(10, OUTPUT); 
 pinMode(11, OUTPUT); 
 pinMode(12, OUTPUT); 
 pinMode(13, INPUT); // Set to trigger the sum operation
}

//Function to add two bits with a carry
int sumBit(int b1a, int b2a, int cBit) {
 int bitResult = 0; //Variable to store the result of the sum of the bits
 int aux1, aux2 = 0; //Auxiliary variables (unused)

 //Performs bitwise XOR to calculate the sum of the bits and transport
 if ((b1a ^ b2a) ^ cBit) {
 bitResult = 1;
 } other {
 bitResult = 0;
 }
 return bitResult; //Returns the result of the sum
}

//Function to calculate the carry bit from the sum of two bits and one carry bit
int sumCarryBit(int b1a, int b2a, int cBit) {
 int aux1, aux2 = 0; //Auxiliary variables (unused)

 // Perform bitwise AND and OR to calculate the carry bit
 if ((b1a && b2a) || (b1a && cBit) || (b2a && cBit)) {
 cBit = 1;
 } other {
 cBit = 0;
 }
 return cBit; //Returns the carry bit
}

// Main loop function to perform the sum operation
empty loop() {
 // Read sum trigger pin state
 sum = digitalRead(13);

 //Read the bits of the first 4-bit number
 nib1a = digitalRead(0);
 nib1b = digitalRead(1);
 nib1c = digitalRead(2);
 nib1d = digitalRead(3);

 //Read the bits of the second 4-bit number
 nib2a = digitalRead(4);
 nib2b = digitalRead(5);
 nib2c = digitalRead(6);
 nib2d = digitalRead(7);

 //If the sum trigger is activated
 if (sum == 1) {
 carryBit = 0; // Initialize the transport bit
 
 // Performs the bitwise sum, updating the carry bit
 res1a = sumBit(nib1a, nib2a, carryBit);
 carryBit = sumCarryBit(nib1a, nib2a, carryBit);
 res1b = sumBit(nib1b, nib2b, carryBit);
 carryBit = sumCarryBit(nib1b, nib2b, carryBit);
 res1c = sumBit(nib1c, nib2c, carryBit);
 carryBit = sumCarryBit(nib1c, nib2c, carryBit);
 res1d = sumBit(nib1d, nib2d, carryBit);
 carryBit = sumCarryBit(nib1d, nib2d, carryBit);
 }
 // Write result bits to output pins
 digitalWrite(8, res1a);
 digitalWrite(9, res1b);
 digitalWrite(10, res1c);
 digitalWrite(11, res1d);
 digitalWrite(12, carryBit); // Write the final carry bit to the output pin
}
