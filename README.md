# INTEGRATED-SOLAR-PANEL
//#include <SoftwareSerial.h> 
//SoftwareSerial zigbee(2,3);//
#include <Servo.h>

#define m21 2
#define m22 3
#define rain 4
Servo tilt;
Servo clean;

int pos1 = 90,i=0;

/////////////////////////////////
void setup() {
  pinMode(m21,INPUT);
  pinMode(m22,INPUT);
  pinMode(rain,INPUT);
  tilt.attach(11);
  tilt.write(90);
  clean.attach(5);
  clean.write(0);
  Serial.begin(9600);
  delay(2000);
}
///////////////////////////////////
void loop() {
  if(digitalRead(rain)==LOW){
    Serial.println("cleaning");
    for(i=0;i<150;i++){
      clean.write(i);
      delay(20);
      }
      delay(500);
    for(i=150;i>=0;i--){
      clean.write(i);
      delay(20);
      }
      delay(500);
    }
   if(digitalRead(m21)==LOW){ 
    Serial.println("TILT --");
    pos1=pos1-2; 
    if(pos1<=45){
      pos1 = 45;
      }
    tilt.write(pos1);
    delay(100);
  }
   if(digitalRead(m22)==LOW){ 
    Serial.println("TILT ++");
    pos1=pos1+2; 
     if(pos1>=135){
      pos1 = 135;
      }
    tilt.write(pos1);
    delay(100); 
  }
}
