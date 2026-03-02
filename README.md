This system can be used in several fields, for example in the agricultural field to check the degree of ripeness of vegetables/fruits, in cosmetics to be able to differentiate between certain very appropriate shades, and in many other fields, making people's work easier.

Resources:
    1. Microcontroller esp32;
    2. TCS3200 color detection sensor;
    3. Arduino IDE;
    4. LCD1602 Display; 
    5. Plusivo Kit (for components: 15 father-father cables, 20 mother-father cables, 10k Potentiometer for LCD's brightness);
    6. Laptop/PC;
    7. Soldering iron with tin;

Tcs3200 - Esp32 connections: 
    -S0 -> D34;
	  -S1 -> D25;
	  -S2 -> D14;
	  -S3 -> D27;
	  -OUT -> D26;
	  -GND -> GND;
	  -VCC -> VIN;

Display - Esp32/Potentiometer connections:
    -GND -> GND;
	  -VDD -> VIN;
	  -V0 -> Potentiometer's central pin;
	  -RS -> D19;
	  -RW -> GND;
	  -E -> D23;
	  -D4 -> D16;
	  -D5 -> D17;
	  -D6 -> D5;
	  -D7 -> D18;
	  -BLA -> VIN;
	  -BLK -> GND;

Potentiometer - Display connections:
    -central Potentiometer's pin -> V0(Display);
    -the side Potentiometer's pins -> one to GND, one to VIN;


CODE :
-------------------------------------
#define S0 34

#define S1 25

#define S2 14

#define S3 27

#define sensorOut 26

LiquidCrystal lcd(19, 23, 16, 17, 5, 18);

int redColor = 0;

int greenColor = 0;

int blueColor = 0;

void setup() {

  pinMode(S0, OUTPUT);
  
  pinMode(S1, OUTPUT);
  
  pinMode(S2, OUTPUT);
  
  pinMode(S3, OUTPUT);
  
  pinMode(sensorOut, INPUT);
  
  digitalWrite(S0,HIGH);
  
  digitalWrite(S1,LOW);
  
  Serial.begin(9600);
  
  lcd.begin(16, 2);
  
  lcd.print("Culoarea este: ");
  
}

void loop() {

  lcd.setCursor(0, 1);
  
  digitalWrite(S2,LOW);
  
  digitalWrite(S3,LOW);
  
  redColor = pulseIn(sensorOut, LOW);
  
  redColor = map(redColor, 25,72,255,0);
  
  Serial.print("R= ");
  
  Serial.print(redColor);
  
  Serial.print("  ");
  
  delay(100);
  
  digitalWrite(S2,HIGH);
  
  digitalWrite(S3,HIGH);
  
  greenColor = pulseIn(sensorOut, LOW);
  
  greenColor = map(greenColor, 30,90,255,0);
  
  Serial.print("G= ");
  
  Serial.print(greenColor)
  
  Serial.print("  ");
  
  delay(100);

  digitalWrite(S2,LOW);
  
  digitalWrite(S3,HIGH);
  
  blueColor = pulseIn(sensorOut, LOW);
  
  blueColor = map(blueColor, 25,70,255,0);
  
  Serial.print("B= ");
  
  Serial.print(blueColor);
  
  if(redColor > greenColor && redColor > blueColor)
  
{

      lcd.print("Rosu!");
      
  }
  
  if(greenColor > redColor && greenColor > blueColor)
  
{

    lcd.print("Verde!");
    
  }
  
  if(blueColor > redColor && blueColor > greenColor)
  
{

    lcd.print("Albastru!");
    
  }
  
  lcd.println("  ");
  
  delay(100);
  
} 
------------------------------------------------------
  Color Reading: Pins S2 and S3 are set to select the corresponding filters for the photodiodes for red, green and blue. The sensor generates a frequency which is measured using pulseIn(sensorOut, LOW);
  Value Mapping: The read values ​​are mapped to a range from 0 to 255 using the map() function, so that they are compatible with the RGB model generally used in computer science.
  Color Display and Determination: Color values ​​are displayed on the serial monitor. The code determines the predominant color and displays the corresponding text on the LCD.


Developed a microcontroller-based color detection system
Integrated sensor communication with ESP32
Gained practical experience working with hardware components and embedded programming
I uploaded the documentation in Romanian. It can be translated to English
