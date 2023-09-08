- 👋 Hi, I’m @sidhdhivinayakelectronics
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
sidhdhivinayakelectronics/sidhdhivinayakelectronics is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
git remote add origin https://github.com/sidhdhivinayakelectronics/sidhdhivinayakelectronics.git
git branch -M main
git push -u origin main
/* Example testing sketch for Barometric Pressure and Temperature sensor
  For more information visit us: www.electrofun.co.in
  Video explanation at: https://youtu.be/nM0v8nLDRas

  REQUIRES the following Arduino libraries:
  Adafruit-GFX-Library: https://github.com/adafruit/Adafruit-GFX-Library
  Adafruit_BMP280_Library: https://github.com/adafruit/Adafruit_BMP280_Library
*/

//Defining all the required libraries 
#include <Wire.h>
#include <SPI.h>
#include <Adafruit_BMP280.h>

//Defining the SPI pins - We are not using SPI communication here 
#define BMP_SCK  (13)
#define BMP_MISO (12)
#define BMP_MOSI (11)
#define BMP_CS   (10)

//Defining the I2C library object
Adafruit_BMP280 bmp; // I2C
//Adafruit_BMP280 bmp(BMP_CS); // hardware SPI
//Adafruit_BMP280 bmp(BMP_CS, BMP_MOSI, BMP_MISO,  BMP_SCK);

void setup() {
  Serial.begin(9600);                       //Initializing the Serial Port to Baud rate 9600
  Serial.println(F("BMP280 test"));

  if (!bmp.begin()) {                       //Initializing the BMP280 sensor
    Serial.println(F("Could not find a valid BMP280 sensor, check wiring!"));
    while (1);
  }

  /* Default settings from datasheet. */
  bmp.setSampling(Adafruit_BMP280::MODE_NORMAL,     /* Operating Mode. */
                  Adafruit_BMP280::SAMPLING_X2,     /* Temp. oversampling */
                  Adafruit_BMP280::SAMPLING_X16,    /* Pressure oversampling */
                  Adafruit_BMP280::FILTER_X16,      /* Filtering. */
                  Adafruit_BMP280::STANDBY_MS_500); /* Standby time. */
}

void loop() {

  //Reading and printing Temperature values
  Serial.print(F("Temperature = "));
  Serial.print(bmp.readTemperature());
  Serial.println(" *C");

  //Reading and printing Pressure values
  Serial.print(F("Pressure = "));
  Serial.print(bmp.readPressure());
  Serial.println(" Pa");

  //Reading and printing Altitude values
  Serial.print(F("Approx altitude = "));
  Serial.print(bmp.readAltitude(1013.25)); /* Adjusted to local forecast! */
  Serial.println(" m");

  Serial.println();
  delay(2000);
}
