# AutoTrafficBump
Senior Project


#include <Wire.h>
#include <Servo.h>
Servo motor;


byte irPinA = 3;
byte irPinB = 4;
byte irValA;
byte irValB;
float diff; // store timeScnd minus timeFirst
float vel; // calculated speed
unsigned long timeA;// IR sensor at irPinA
unsigned long timeB;// IR sensor at irPinB
float speedConst = 453.6; // ((distance between IR sensors in mm) x 3600)/1000)to convert mm/millis to km/h) 
                          // In This project we have 126mm between IR sensors







void setup()
{
motor.attach(9);
pinMode(irPinA, INPUT);
pinMode(irPinB, INPUT);

Serial.begin(9600);



}//end setup


void loop()
{
//Wait first pin to become low
while (digitalRead(irPinA) != LOW);
timeA = millis();

delay(50);

while (digitalRead(irPinB) != LOW);
timeB = millis();
diff = timeB-timeA;
vel = 453.6 / diff;//calcula a velocidade em km/h 126mm

if(vel<=1.50)
motor.write(0);
else if (vel>=2.00)
motor.write(90);
delay(2000);
motor.write(0);
     
   
    Serial.print("T1: ");
    Serial.println(timeA);
    Serial.print("T2: ");
    Serial.println(timeB);
    Serial.print("Diff: ");
    Serial.println(diff);
    Serial.print("Speed: ");
    Serial.println(vel);
    
    

       
        }
