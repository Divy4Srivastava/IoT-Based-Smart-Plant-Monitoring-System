#define BLYNK_TEMPLATE_ID "TMPLQonOn-dA"
#define BLYNK_DEVICE_NAME "Internet of Things"
#define BLYNK_AUTH_TOKEN "o_-d0vdQk0fNk2AdedWVgXW5h7vF6vI9"

#define BLYNK_PRINT Serial   
#include <SPI.h>
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <SimpleTimer.h>
#include <DHT.h>
#define BLYNK_PRINT Serial
#include <OneWire.h>
#include <DallasTemperature.h>
#define ONE_WIRE_BUS D2
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);



char auth[] ="o_-d0vdQk0fNk2AdedWVgXW5h7vF6vI9";        //Authentication code sent by Blynk
char ssid[] = "OPPO A5s";                       //WiFi SSID
char pass[] = "Password";                       //WiFi Password

#define sensorPin D3 
/*int sensorState = 0;
int lastState = 0;*/    
#define DHTTYPE DHT11     
DHT dht(5, DHTTYPE);
SimpleTimer timer;

BLYNK_WRITE(V3){
  int pinvalue = param.asInt();
  digitalWrite(D3,pinvalue);
}
void sendSensor()
{
  float h = dht.readHumidity();
  float t = dht.readTemperature();
  int moisture_sensor= analogRead(A0);
 // int analog_output = (moisture_sensor-1)/1023;
  //int moisture_in_percent = 100- (moisture_sensor*100);
 // int moisture_in_percent = 100- (analog_output*100);

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
 
  Blynk.virtualWrite(V0, h);  //V0 is for Humidity
  Blynk.virtualWrite(V1, t);  //V1 is for Temperature
  Blynk.virtualWrite(V2, moisture_sensor);  //V2 is for soil moisture
  delay(500);
}
void setup()
{
  Serial.begin(115200);
 // Blynk.begin(auth, ssid, pass);
   pinMode(sensorPin, OUTPUT);
 // dht.begin();

 // timer.setInterval(1000L, sendSensor);
 // Serial.begin(115200);
  Blynk.begin(auth, ssid, pass);
  timer.setInterval(100L, sendSensor);
 //  sensors.begin();
}
/*int sensor=0;
void sendTemps()
{
sensor=analogRead(A0);
sensors.requestTemperatures();
float temp = sensors.getTempCByIndex(0); 
Serial.println(temp);
Serial.println(sensor);
Blynk.virtualWrite(V1, temp);
Blynk.virtualWrite(V2,sensor);
delay(1000);
}*/
void loop()
{
  Blynk.run(); 
  timer.run(); 
 /* sendTemps();
  sensorState = digitalRead(sensorPin);
Serial.println(sensorState);

if (sensorState == 1 && lastState == 0) {
  Serial.println("needs water, send notification");
  Blynk.notify("Water your plants");
  lastState = 1;
  delay(1000);
//send notification
    
  } 
  else if (sensorState == 1 && lastState == 1) {
    //do nothing, has not been watered yet
  Serial.println("has not been watered yet");
  delay(1000);
  }
  else {
    //st
    Serial.println("does not need water");
    lastState = 0;
    delay(1000);
  }
  
  delay(100);*/
}
