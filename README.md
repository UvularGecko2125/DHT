DHT22  
工作一  
功能:溫溼度感測 顯示溫度和濕度 溫度大於等於20度時 讓蜂鳴器響起  
輸出腳:2(溫溼度感測器輸出),3(蜂鳴器輸入)  
```c++
#include <Adafruit_Sensor.h>
#include <DHT.h>
#include <DHT_U.h>

#define DHTPIN 2 
#define DHTTYPE    DHT22     // DHT 22 (AM2302)
DHT_Unified dht(DHTPIN, DHTTYPE);

uint32_t delayMS;
int a;

void setup() {
  Serial.begin(9600);
  dht.begin();
    sensor_t sensor;
  delayMS = sensor.min_delay / 1000;
}

void loop() {
  delay(delayMS);
  sensors_event_t event;
  dht.temperature().getEvent(&event);
  if (isnan(event.temperature)) {
    Serial.println(F("Error reading temperature!"));
  }
  else {
    Serial.print(F("Temperature: "));
    Serial.print(event.temperature);
    Serial.println(F("°C"));
    a=event.temperature;
  }
  dht.humidity().getEvent(&event);
  if (isnan(event.relative_humidity)) {
    Serial.println(F("Error reading humidity!"));
  }
  else {
    Serial.print(F("Humidity: "));
    Serial.print(event.relative_humidity);
    Serial.println(F("%"));
  }

  if(a>=20)
{
   tone(3,1500);
   delay(150);
   noTone(3);
   delay(150);
   Serial.print(F("a=:"));
   Serial.print(a);
   Serial.println(F("°C"));
}
}
```
![image](https://github.com/UvularGecko2125/DHT/blob/main/DSC_0023.JPG)![image](https://github.com/UvularGecko2125/DHT/blob/main/DSC_0024.JPG)  
加裝風扇(溫度大於20度時開啟)  
輸出腳:N1(5),N2(6),N3(GND)
