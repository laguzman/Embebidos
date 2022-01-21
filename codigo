  
#include <LiquidCrystal.h> 
// Se definen los pines en el Arduino correspondientes a cada componente
const int bulb_pin = 6; // Pin de relé de los focos
const int fan_pin = 7;  // Pin de relé de ventiladores
int extractor=9;
// Variables sensor y pantalla
LiquidCrystal lcd(12, 11, 5, 4, 3, 2); // Pantalla LCD
// Variables para Temperatura y Humedad Relativa
float temp = 0; // Temperatura
float rh = 0;   // Humedad Relativa (sin uso práctico)
k=0
void setup() {
   pinMode(A0, INPUT);
   pinMode(A1, INPUT);
   pinMode(extractor, INPUT);
  Serial.begin(9600);       // Inicializa comunicación serial
  lcd.begin(16, 2);         // Inicializa pantalla LCD 16x2
  delay(1000);
  
}
void loop() {
  // Lectura de Datos
  float valor =analogRead(A0);
  float valor2 =analogRead(A1);
  float hum=map(valor2, 155, 803, 0, 100);
  temp = valor * 5 * 100 / 1024 ;
  String temps = (String) temp;
   String hums = (String) hum;
  Serial.println(temps+","+hums);
  if (Serial.available() > 0) {
    String data = Serial.readStringUntil('\n');
    Serial.print("You sent me: ");
    Serial.println(data);
  }
  k =hum;
  lcd.clear();              // Limpia pantalla LCD
    lcd.begin(16, 2);         // Inicializa nuevamente pantall LCD 16x2
    lcd.print("T:     °C H:");  // Imprime C: y H: para presentar datos
    lcd.setCursor(0, 1);      // Cursor de pantalla en columna=0, fila=1 (1er
                              // caracter de la 2da columna)
    lcd.print("Temperatura"); // Imprime "Temperatura"
    lcd.setCursor(2, 0);  // Mueve el cursor a la 3era columna de la 1era fila
    lcd.print(temp);      // Imprime el valor de la temperatura en Celsius
    lcd.setCursor(12, 0); // Mueve el cursor a la 11va columna de 1era fila
    lcd.print(k);         // Imprime el valor de la temperatura en Kelvin
     lcd.setCursor(14, 0); // Mueve el cursor a la 11va columna de 1era fila
      lcd.print("%");    
  delay(3000); // Espera 900ms para poder apreciar lectura en pantalla LCD
  
  if (temp > 37.9) {
    // Si la temperatura en celsius es mayor a 37.9:
    analogWrite(bulb_pin, 0);  // Apaga ambos focos
    analogWrite(fan_pin, 255); // Enciende ambos ventiladores
    delay(1000); // Espera 900ms para poder apreciar lectura en pantalla LCD
    
    lcd.clear();                 // Limpia pantalla LCD
    lcd.begin(16, 2);            // Inicializa nuevamente pantalla LCD 16x2
    lcd.setCursor(0, 0);         // Mueve el cursor al inicio de la 1era fila
    lcd.print("ALERTA!");        // Imprime "ALERTA!" en la pantalla LCD
    lcd.setCursor(0, 1);         // Mueve el cursor al inicio de la 2da fila
    lcd.print("TEMP. MUY ALTA"); // Imprime "TEMP. MUY ALTA" en la pantalla LCD
    delay(1000); // Espera 1000ms para poder apreciar lectura en pantalla LCD
    
  } 
   else if (temp < 36.0) {
    // Caso contrario (temperatura menor o igual a 36.0)
    analogWrite(bulb_pin, 255); // Enciende ambos focos
    analogWrite(fan_pin, 0);    // Apaga ambos ventiladores++
    delay(900); // Espera 900ms para poder apreciar lectura en pantalla LCD
    
    lcd.clear();                 // Limpia pantalla LCD
    lcd.begin(16, 2);            // Inicializa nuevamente pantalla LCD 16x2
    lcd.setCursor(0, 0);         // Mueve el cursor al inicio de la 1era fila
    lcd.print("ALERTA!");        // Imprime "ALERTA!" en la pantalla LCD
    lcd.setCursor(0, 1);         // Mueve el cursor al inicio de la 2da fila
    lcd.print("TEMP. MUY BAJA"); // Imprime "TEMP. MUY BAJA" en la pantalla LCD
    delay(1000); // Espera 1000ms para poder apreciar lectura en pantalla LCD
    }
    else {
    analogWrite(bulb_pin, 0); // Enciende ambos focos
    analogWrite(fan_pin, 0);    // Apaga ambos ventiladores
     lcd.clear();                 // Limpia pantalla LCD
    lcd.begin(16, 2);            // Inicializa nuevamente pantalla LCD 16x2
    lcd.setCursor(0, 0);         // Mueve el cursor al inicio de la 1era fila
    lcd.print("TEMPERATURA:");        // Imprime "TEMPERATURA!" en la pantalla LCD
    lcd.setCursor(0, 1);         // Mueve el cursor al inicio de la 2da fila
    lcd.print(" ESTABLE"); // Imprime "ESTABLE" en la pantalla LCD
    delay(900);
    }
    if (hum > 85) {
    analogWrite(extractor, 255); // Enciende  extractor
    lcd.clear();                 // Limpia pantalla LCD
    lcd.begin(16, 2);            // Inicializa nuevamente pantalla LCD 16x2
    lcd.setCursor(0, 0);         // Mueve el cursor al inicio de la 1era fila
    lcd.print("ALERTA!:");        // Imprime "ALERTA!" en la pantalla LCD
    lcd.setCursor(0, 1);         // Mueve el cursor al inicio de la 2da fila
    lcd.print("HUMEDAD MUY ALTA"); // Imprime "HUMEDAD MUY ALTA" en la pantalla LCD
    delay(900);
    }
    else if(hum<80){
    analogWrite(extractor, 0); // Enciende  extractor
    lcd.clear();                 // Limpia pantalla LCD
    lcd.begin(16, 2);            // Inicializa nuevamente pantalla LCD 16x2
    lcd.setCursor(0, 0);         // Mueve el cursor al inicio de la 1era fila
    lcd.print("ALERTA!:");        // Imprime "ALERTA!" en la pantalla LCD
    lcd.setCursor(0, 1);         // Mueve el cursor al inicio de la 2da fila
    lcd.print("HUMEDAD MUY BAJA"); // Imprime "HUMEDAD MUY BAJA" en la pantalla LCD
    delay(900);
    }
  delay(10000); // Espera 10000ms antes de realizar la siguiente lectura
  }
