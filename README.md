#include <Servo.h>

Servo moteurD;
Servo moteurG;
int ldrD = A5;
int ldrG = A4;
int valeurD;
int valeurG;
int ledBlanc = 4;
int ledBleu = 5;
void setup()
{
  pinMode(ldrD, INPUT);
  pinMode(ldrG, INPUT);
  pinMode (ledBlanc, OUTPUT);
  pinMode (ledBleu, OUTPUT);
  moteurD.attach(6);
  moteurG.attach(7);
  Serial.begin(9600);
}
void gauche(){
  moteurD.write(180);
  moteurG.write(90);
}
void droite(){
  moteurD.write(90);
  moteurG.write(0);
}
void avancer(){
  moteurD.write(180);
  moteurG.write(0);
}
void stop() {
  moteurD.write(90);
  moteurG.write(90);
}

void loop()
{
  valeurD= analogRead(ldrD);
  valeurG= analogRead(ldrG);
  Serial.print("valeurD=");
  Serial.print(valeurD);
  avancer();
  
  Serial.print("   valeurG=");
  Serial.println(valeurG);
  
  if(500<valeurG && 500<valeurD){
    digitalWrite(ledBlanc, LOW);
    digitalWrite(ledBleu, LOW);
    stop();
      }
  else if(500>valeurG && valeurD>500){
    digitalWrite(ledBleu, LOW);
    digitalWrite(ledBlanc, HIGH);
    droite();
  }
  else if(500>valeurD && valeurG>500){
    digitalWrite(ledBleu, HIGH);
    digitalWrite(ledBlanc, LOW);
    gauche();
  }

}
