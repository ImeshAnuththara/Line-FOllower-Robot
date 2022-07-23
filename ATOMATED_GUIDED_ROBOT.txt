#include <AFMotor.h>

int Echo = A2; //LEFT SENSOR ECHO
int Trig = A3; //LEFT SENSOR TRIG

#define left A0 //LEFT IR SENSOR
#define right A1//RIGHT IR SENSOR

//const int buzzer = A4;
long duration;
int distance;

//defining motors
AF_DCMotor motor1(1); 
AF_DCMotor motor2(2);
AF_DCMotor motor3(3);
AF_DCMotor motor4(4);

void setup() {
  //declaring pin types
  pinMode(Echo, INPUT);
  pinMode(Trig, OUTPUT);
  pinMode(left,INPUT);
  pinMode(right,INPUT);
//  pinMode(buzzer, OUTPUT); 
  Serial.begin(9600);  
}

void loop(){
digitalWrite(Trig, LOW);
delayMicroseconds(2);
digitalWrite(Trig, HIGH);
delayMicroseconds(10);
digitalWrite(Trig, LOW);
duration = pulseIn(Echo, HIGH);
distance = duration*0.034/2;
Serial.println ("Distance\n");
Serial.print(distance);
Serial.print("cm\t\t");
if (distance < 12){
    Stop();
    delay(800);
    Left1();
    delay(325);
    forward1();
    delay(260);
    Right1();
    delay(325);
    forward1();
    delay(355);
    Right1();
    delay(200);
    } 
 if(distance > 12){
  if(!digitalRead(left)==1 && !digitalRead(right)==1){forward();}
  if(!digitalRead(left)==1 && digitalRead(right)==1){Right1();}
  if(digitalRead(left)==1 && !digitalRead(right)==1){Left1();}
  if(!digitalRead(left)==0 && !digitalRead(right)==0){
   // Stop();
   forward();
  //  delay(2000);
//    inform(); // buzzer
//    delay(500);
 //   Left1();
 //   delay(580); 
  }  
  } 
}
void forward(){
    motor1.run(FORWARD);
    motor1.setSpeed(60);
    motor2.run(FORWARD);
    motor2.setSpeed(60);
    motor3.run(FORWARD);
    motor3.setSpeed(60);
    motor4.run(FORWARD);
    motor4.setSpeed(60);
  }
void forward1(){
    motor1.run(FORWARD);
    motor1.setSpeed(100);
    motor2.run(FORWARD);
    motor2.setSpeed(100);
    motor3.run(FORWARD);
    motor3.setSpeed(100);
    motor4.run(FORWARD);
    motor4.setSpeed(100);
  }
void Left1(){
    motor1.run(BACKWARD);
    motor1.setSpeed(150);
    motor2.run(BACKWARD);
    motor2.setSpeed(150);
    motor3.run(FORWARD);
    motor3.setSpeed(150);
    motor4.run(FORWARD);
    motor4.setSpeed(150);
  }

void Right1(){
    motor1.run(FORWARD);
    motor1.setSpeed(150);
    motor2.run(FORWARD);
    motor2.setSpeed(150);
    motor3.run(BACKWARD);
    motor3.setSpeed(150);
    motor4.run(BACKWARD);
    motor4.setSpeed(150);
  }
void Stop(){
    motor1.run(RELEASE);
    motor1.setSpeed(0);
    motor2.run(RELEASE);
    motor2.setSpeed(0);
    motor3.run(RELEASE);
    motor3.setSpeed(0);
    motor4.run(RELEASE);
    motor4.setSpeed(0);
  }
//void inform(){tone(buzzer,500,500);}
