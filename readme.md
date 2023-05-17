# Sprint 2 - Edge Computing - Elite Jobs

**Anna Soto – RM550360**
**Danilo Urze – RM99456**
**Lucas Sobral – RM98188**
**Murilo Mansano – RM 98143**
**Pedro Ananias – RM550689**

## Link da simulação:

**https://www.tinkercad.com/things/gJny0iFWVw9-edge-computing-sprint-2/editel?sharecode=vmXet2_c-3oOTG7i5Xt7EeNQHUdFj8m2EHrOoEU9HuA**

## Código

#include <LiquidCrystal.h>

int ledvermelho = 13;
int ledverde = 11;
int sensortemp = A0;

float valorsensortemp;
int celcius;
float tensaotemp;

int buzzer = 10;
int ldr = A1;
int valorldr;

int valorSensorUmid;
int valorUmid;

LiquidCrystal lcd(7,6,5,4,3,2);

void setup(){
  Serial.begin(5000);
  pinMode(ledvermelho,OUTPUT);
  pinMode(ledverde,OUTPUT);
  pinMode(buzzer,OUTPUT);
  lcd.begin(16, 2);
  lcd.setCursor(0, 0);
}

void loop(){
  valorldr = analogRead(ldr);
  
  valorsensortemp = analogRead(sensortemp);
  tensaotemp = 5*valorsensortemp/1023;
  celcius = (tensaotemp - 0.5) * 100;
  
  valorSensorUmid = analogRead(A2);
  valorUmid = map(valorSensorUmid, 0, 1023, 0, 100);
  
  Serial.println("");
  Serial.print("Tensao do sensor de temperatura: ");
  Serial.print(tensaotemp);
  Serial.println(" V");
  
  Serial.print("Temperatura: ");
  Serial.print(celcius);
  Serial.println(" C");
  
  Serial.print("Valor do LDR: ");
  Serial.println(valorldr);
  
  Serial.print("Umidade: ");
  Serial.print(valorUmid);
  Serial.println("%");
  
  Serial.println("");
  Serial.println("-------------------------------");
  
  /*SÉRIE DE IFs*/
  /*Valores ideais*/
  
  if (valorldr < 200) {
   digitalWrite(ledverde,HIGH);
   digitalWrite(ledvermelho,LOW);
   digitalWrite(buzzer,LOW);
    
   lcd.setCursor(0,0);
   lcd.print("Luminosidade: OK");
   lcd.setCursor(0,1);
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  if (celcius >= 1 && celcius <= 5){
   digitalWrite(ledverde,HIGH);
   digitalWrite(ledvermelho,LOW);
   digitalWrite(buzzer,LOW);
    
   lcd.setCursor(0,0);
   lcd.print("Temperatura: OK");
   lcd.setCursor(0,1);
   lcd.print("Temp. =");
   lcd.setCursor(7,1);
   lcd.print(celcius);
   lcd.print("C");
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  if (valorUmid >= 40 && valorUmid <=70){
   digitalWrite(ledverde,HIGH);
   digitalWrite(ledvermelho,LOW);
   digitalWrite(buzzer,LOW);
    
   lcd.setCursor(0,0);
   lcd.print("Umidade OK");
   lcd.setCursor(0,1);
   lcd.print("Umid. =");
   lcd.setCursor(7,1);
   lcd.print(valorUmid);
   lcd.print("%");
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  
  
  /*Valores Baixos ou Médios*/ 
  
  if (celcius < 1){
   digitalWrite(ledvermelho,HIGH);
   digitalWrite(ledverde,LOW);
   digitalWrite(buzzer,HIGH);
    
   lcd.setCursor(0,0);
   lcd.print("Temp. BAIXA");
   lcd.setCursor(0,1);
   lcd.print("Temp. =");
   lcd.setCursor(7,1);
   lcd.print(celcius);
   lcd.print("C");
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  if (valorUmid < 40){
   digitalWrite(ledvermelho,HIGH);
   digitalWrite(ledverde,LOW);
   digitalWrite(buzzer,HIGH); 
   
   lcd.setCursor(0,0);
   lcd.print("Umidade BAIXA");
   lcd.setCursor(0,1);
   lcd.print("Umid. =");
   lcd.setCursor(7,1);
   lcd.print(valorUmid);
   lcd.print("%");
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  
  /*Valores Altos*/
  
  if (valorldr>200){
    digitalWrite(ledvermelho,HIGH);
    digitalWrite(buzzer,HIGH);
    digitalWrite(ledverde,LOW);
    
    lcd.setCursor(0,0);
    lcd.print("Lumin.: ALTA");
    lcd.setCursor(0,1);
    lcd.print("PORTA ABERTA");
    delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  if (celcius > 5){
   digitalWrite(ledvermelho,HIGH);
   digitalWrite(ledverde,LOW);
   digitalWrite(buzzer,HIGH);
    
   lcd.setCursor(0,0);
   lcd.print("Temp. ALTA");
   lcd.setCursor(0,1);
   lcd.print("Temp. =");
   lcd.setCursor(7,1);
   lcd.print(celcius);
   lcd.print("C");
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
  if (valorUmid > 70){
   digitalWrite(ledvermelho,HIGH);
   digitalWrite(ledverde,LOW);
   digitalWrite(buzzer,HIGH); 
   
   lcd.setCursor(0,0);
   lcd.print("Umidade ALTA");
   lcd.setCursor(0,1);
   lcd.print("Umid. =");
   lcd.setCursor(7,1);
   lcd.print(valorUmid);
   lcd.print("%");
   delay(2000);
    
   lcd.setCursor(0,0);
   lcd.print("                 ");
   lcd.setCursor(0,1);
   lcd.print("                 ");
  }
}