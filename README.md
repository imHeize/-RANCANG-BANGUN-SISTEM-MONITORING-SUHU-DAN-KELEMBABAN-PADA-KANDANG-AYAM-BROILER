# -RANCANG-BANGUN-SISTEM-MONITORING-SUHU-DAN-KELEMBABAN-PADA-KANDANG-AYAM-BROILER  
Kode Skrip Wokwi

#include "DHTesp.h" #include <WiFi.h> #include <ThingSpeak.h> #include <Adafruit_Sensor.h>

const int DHT_PIN = 15; const char* ssid = "Wokwi-GUEST"; const char*pass = "";

Klien WiFiClient;

unsigned long myChannelNumber = 1; const char* myWriteAPIKey = "JAMACVFBOTU0A8US"; const char* server = "api.thingspeak.com";

unsigned long lastTime = 0; unsigned long timerDelay = 3000;

int lampu = 14; int suhu; int humi;

DHTesp dhtSensor;

pengaturan batal() { pinMode(lampu, OUTPUT); Serial.begin(115200); dhtSensor.setup(DHT_PIN, DHTesp::DHT22); dhtSensor.getPin(); penundaan (10); WiFi.mulai(ssid, lulus); while(WiFi.status() != WL_CONNECTED){ tunda(100); Serial.println("."); } Serial.println("WiFI Terhubung !"); Serial.println(WiFi.localIP());

WiFi.mode(WIFI_STA);

ThingSpeak.begin(klien); }

kekosongan loop() { temp = dhtSensor.getTemperature(); Serial.println("Temp: " + String(temp) + "°C"); if (temp < 18 ){ Serial.println("Suhu Dingin !"); } if (temp >= 18 && temp <= 24){ Serial.println("Suhu Normal"); } if (temp > 24 ){ Serial.println("Suhu Panas !"); } Serial.println("");

humi = dhtSensor.getHumidity(); Serial.println("Kelembaban: " + String(humi) + "%"); if (humi < 30 ){ Serial.println("Kelembaban Kering !"); } if (humi >= 30 && humi <= 60){ Serial.println("Kelembaban Normal"); } if (humi > 60 ){ Serial.println("kelembaban Basah !"); } Serial.println("---");

if (temp < 18 && humi > -1){ digitalWrite(lamp, HIGH); Serial.println("Lampu Nyala"); }

if (temp > 24 && humi > -1){ digitalWrite(lamp, LOW); Serial.println("Lampu Mati"); }

ThingSpeak.setField(1, temp); ThingSpeak.setField(2, humi);

int x = ThingSpeak.writeFields(MyChannelNumber, myWriteAPIKey); if (x == 200) { Serial.println("Pembaruan Saluran Berhasil"); } }
