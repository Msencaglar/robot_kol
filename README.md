#robot-kol

Servo servo1;      // 1. servo motor
Servo servo2;      // 2. servo motor
Servo servo3;      // 3. servo motor
Servo servo4;      // 4. servo motor

int servoDeger = 0;   // Servo motor değerini tutan değişken
char gelenVeri;       // Bluetooth sensöründen gelen veri

void setup() {
  Serial.begin(9600);   // Seri port bağlantısı
  servo1.attach(6);     // 1. servo motorun sinyal pini
  servo2.attach(9);     // 2. servo motorun sinyal pini
  servo3.attach(10);    // 3. servo motorun sinyal pini
  servo4.attach(11);    // 4. servo motorun sinyal pini
}

void servoYukari(Servo &servo) {
  servoDeger = servo.read();      
  if (servoDeger + 1 <= 180) {
    servo.write(servoDeger + 1);
    delay(15);
  }
}

void servoAsagi(Servo &servo) {
  servoDeger = servo.read();     
  if (servoDeger - 1 >= 0) {
    servo.write(servoDeger - 1);
    delay(15);
  }
}

void loop() {
  if (Serial.available()) {   
    gelenVeri = Serial.read();    

    // 1. servo motor kontrolü
    if (gelenVeri == 'F') servoYukari(servo1);
    if (gelenVeri == 'B') servoAsagi(servo1);

    // 2. servo motor kontrolü
    if (gelenVeri == 'L') servoYukari(servo2);
    if (gelenVeri == 'R') servoAsagi(servo2);

    // 3. servo motor kontrolü
    if (gelenVeri == 'G') servoYukari(servo3);
    if (gelenVeri == 'I') servoAsagi(servo3);

    // 4. servo motor kontrolü
    if (gelenVeri == 'H') servoYukari(servo4);
    if (gelenVeri == 'J') servoAsagi(servo4);
  }
}
