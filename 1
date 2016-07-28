#include <ServoTimer2.h>
#include <SoftwareSerial.h>
#include <TinyGPS.h>
#include <SPI.h>
#include <SD.h>

#define RELAY1  7
#define ServoParachutePin 2

/*
  conections:
  MODULO   X   arduino mega pin
  -----------------------------
  sd card:
  MISO              - 50
  SCK               - 52
  MOSI              - 51
  CS                - 04
  5V                - 5v

  Relay:
  In1               - 07
  Vcc               - 5v

  gps neo6mv2:
  vcc               - 3.3v
  rx                - 18
  tx                - 10

  servo:
  signal            - 2
  vcc               - 5v
*/

int Altitude_1, Altitude_2, Difference_Altitudes, Date;
int Counter = 0; // log id number
int Altitude_Memory = 1; 
int Solenoid = 0;
int ParachuteServoPos = 0;// variable to store the servo position
int ParachuteServoPin = 2;
int CS_pin = 4;
float Speed;
bool AltTarguet = false;
String ReachedAltTarguet = "Not Reached";
String Parachute = "closed";
String Movement = " ";
unsigned long fix_age, time, date, speed, course;

static void smartdelay(unsigned long ms);
static void print_float(float val, float invalid, int len, int prec);
static void print_date(TinyGPS &gps);

ServoTimer2 ParachuteServo;  // create servo object to control a servo
TinyGPS gps;
SoftwareSerial ss(10, 18);
File myFile;

void setup()
{
 // ServoParachute.attach(ServoParachutePin);
  pinMode(RELAY1, OUTPUT);
  pinMode(CS_pin, OUTPUT);
  pinMode( ParachuteServoPin, OUTPUT) ;
  ParachuteServo.attach(ParachuteServoPin); // attaches the servo on pin 9 to the servo object

  Serial.begin(9600);
  
  Serial.println("Deflation Control and Log for Stratospheric Platform" );
  Serial.println("by Pedro Terra V:1.0");
  Serial.println(" ");
  ss.begin(9600);

  ParachuteServo.write(ParachuteServoPos);
  Serial.println("Putting Servo Paracuhte to CLOSE position");
  Serial.println(" ");

  //INICIALIZE SD CARD

  Serial.print("Initializing SD card...");
  if (!SD.begin(CS_pin)) {
    Serial.println("initialization failed!");
    return;
  }
  Serial.println("initialization done.");

  //write header to log file

  myFile = SD.open("log1.csv", FILE_WRITE);

  // if the file opened okay, write to it:
  if (myFile) {
    myFile.println(", , , ,");// just in case there is previous lines

    // setting header
    String header = "Counter, Date, Time, Lat, Lon, Altitude 1, Altitude 2, Dif Alts, movement, Speed, Altitude Targuet, solenoide, parachute";

    myFile.println(header); //print header to file
    myFile.flush(); //save file
    myFile.close(); // close file
  } else {
    Serial.println("Couldn't open log file");
  }
}

void loop()
{
  float flat, flon;
  unsigned long age, date, time, chars = 0;
  unsigned short sentences = 0, failed = 0;

  Serial.println("GPS stats:");
  Serial.println("chars - sen - fails");
  gps.stats(&chars, &sentences, &failed);
  print_int(chars, 0xFFFFFFFF, 6);
  print_int(sentences, 0xFFFFFFFF, 10);
  print_int(failed, 0xFFFFFFFF, 9);
  Serial.println("");

  //CHECK ALTITUDE MEMORY

  if (Altitude_Memory == 1) {
    // memory 1

    //SETTING COUNTER
    Serial.println("");
    Serial.println("---Memory 1---");
    Serial.print("counter: "); Serial.println(Counter);
    Counter++;

    gps.f_get_position(&flat, &flon, &age);
    Altitude_1 = gps.f_altitude(), TinyGPS::GPS_INVALID_F_ALTITUDE, 7, 2; // save altitude 1 to alt1
    Serial.print("alt1: "); Serial.println(Altitude_1); // print alt1 to check
    Serial.println("");
    delay(2000);
    Altitude_Memory = 2; // change to altitude memory 2

  } else {
    // memory 2
    Serial.println("");
    Serial.println("---Memory 2---");
    Serial.print("counter: "); Serial.println(Counter);

    gps.f_get_position(&flat, &flon, &age); // get infos from gps

    // print lat
    Serial.print("lat: ");
    Serial.println(flat == TinyGPS::GPS_INVALID_F_ANGLE ? 0.0 : flat, 6);

    // print lon
    Serial.print("lon: ");
    Serial.println(flon == TinyGPS::GPS_INVALID_F_ANGLE ? 0.0 : flon, 6);

    // print alt2
    Altitude_2 = gps.f_altitude(), TinyGPS::GPS_INVALID_F_ALTITUDE, 7, 2;// save altitude to alt2
    Serial.print("alt2: "); Serial.println(Altitude_2);

    //GET DIFALTS
    Difference_Altitudes = Altitude_2 - Altitude_1;
    Serial.print("Dif Alts: ");
    Serial.println(Difference_Altitudes);

    // SET MOVEMENT
    if (Difference_Altitudes > 0) {
      Movement = "going up";
      Serial.print("Movement: ");
      Serial.println(Movement);
    } else if (Difference_Altitudes < 0) {
      Movement = "going Down";
      Serial.print("Movement: ");
      Serial.println(Movement);
    } else {
      Movement = "Sttopped";
      Serial.print("Movement: ");
      Serial.println(Movement);
    }

    //SET SPEED
    gps.f_speed_kmph(), TinyGPS::GPS_INVALID_F_SPEED, 6, 2;
    Speed = gps.f_speed_kmph(), TinyGPS::GPS_INVALID_F_SPEED, 6, 2;
    Serial.print("Speed: "); Serial.println(Speed);

    //GETTING TIME
    // print_date(gps);
    // time in hhmmsscc, date in ddmmyy
    gps.get_datetime(&date, &time, &fix_age);
    Serial.print("date: "); Serial.println(date);
    Serial.print("time: "); Serial.println(time);

    //CHECK IF ALT TARGUET WAS REACHED?
    if (Altitude_2 > 30000) {
//      AltTarguet = true; // change status
      ReachedAltTarguet = "Reached"; 
      Serial.print("Altitude targuet: "); Serial.println(ReachedAltTarguet);
    } else {
      Serial.print("Altitude targuet: "); Serial.println(ReachedAltTarguet);
    }

    //CHECK ALTITUDE AND SEE IF SOLENOID SHOULD BE ON
    if (Altitude_2 > 30000 && Altitude_2 != 16960) {
      digitalWrite(RELAY1, 0);          // Turns ON Relays 1
      Serial.println("solenoid  ON");
      delay(100000);                      // wait leave solenoid on for one seccond
      digitalWrite(RELAY1, 1);         // Turns Relay Off
      Serial.println("solenoid OFF");
      Serial.println("");
      Solenoid++;                       // count numeber of time solenoid was on

    } else if (Altitude_2 == 16960) {
      digitalWrite(RELAY1, 1);         // Turns Relay Off
      Serial.println("solenoid OFF");
    }

    //PARACHUTE
    if (Speed > 1) {
      //ParachuteServo.attach(2);
      Parachute = "open"; // change status for open
      Serial.print("parachute: "); Serial.println(Parachute); // print open in serial monitor
      ParachuteServoPos = 165;
      ParachuteServo.write(ParachuteServoPos); //move servo for open pos 165 degrees
      delay(5000); // wait 5 seconds
      ParachuteServoPos = 0;
      ParachuteServo.write(ParachuteServoPos); // move to close position 0 degrees
      delay(500); // wait hal seccond
      // do it again in case it hasn't opened properly

    } else {
      Serial.print("parachute: "); Serial.println(Parachute);
    }

    //TEMPERATURE
    //add temperature code here

    //PRESSURE
    //add pressure code here

    // LOG DATA
    // CREATE DATASTRING to be stored in sd in CSV format
    String dataString =  String(Counter) + ", " + String(date) + ", " + String(time) + ", " + String(flat == TinyGPS::GPS_INVALID_F_ANGLE ? 0.0 : flat, 6) + ", " + String(flon == TinyGPS::GPS_INVALID_F_ANGLE ? 0.0 : flon, 6) + ", " + String(Altitude_1) + ", " + String(Altitude_2) + ", " + String(Difference_Altitudes) + ", " + String(Movement) + ", " + String(Speed) + ", " + String(ReachedAltTarguet) + ", " + String(Solenoid) + ", " + String(Parachute);

    // open the file
    myFile = SD.open("log1.csv", FILE_WRITE);

    // if the file opened okay, write to it:
    if (myFile) {
      Serial.print("Writing to log1.csv...");

      //WRITTE DATA STRING TO CARD
      myFile.println(dataString); //writte log on sd card

      // close the file:
      myFile.flush();
      myFile.close();
      Serial.println("done.");

      //print datastring in serial monitor
      Serial.print("data string: "); Serial.println(dataString);
      Serial.println("");

    } else {
      // if the file didn't open, print an error:
      Serial.println("error opening log1.csv while trying to write");
    }

    Altitude_Memory = 1; // change to memory 1

    //add 1 to counter
    Counter++;

    Serial.println("--------------------------------------------------END CYCLE---------------------------------------------------");
    Serial.println("");
  }
  smartdelay(5000);
}

static void smartdelay(unsigned long ms)
{
  unsigned long start = millis();
  do
  {
    while (ss.available())
      gps.encode(ss.read());
  } while (millis() - start < ms);
}

static void print_int(unsigned long val, unsigned long invalid, int len)
{
  char sz[32];
  if (val == invalid)
    strcpy(sz, "*******");
  else
    sprintf(sz, "%ld", val);
  sz[len] = 0;
  for (int i = strlen(sz); i < len; ++i)
    sz[i] = ' ';
  if (len > 0)
    sz[len - 1] = ' ';
  Serial.print(sz);
  smartdelay(0);
}
