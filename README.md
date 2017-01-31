//--------------------------------------------------------------------------------------------------------------------------------------

//RC KONTROLLÜ ARABA - Yavuz ERTUGRUL - 31/01/2017 
#include <SoftwareSerial.h> //Bluetooth iletişimi için kütüphane
#include <AFMotor.h> //L293d Arduino Motor sürücü için kütüphane
int incomingByte = 0;  // Bluetoothdan gelen veriler


//Bu kısımda motorları ve hızlarını tanıtıyoruz.Bu arada bir motor 0-255 arası hızda gidebiliyor.
AF_DCMotor motor1(1, 255); 
AF_DCMotor motor2(2, 255);
AF_DCMotor motor3(3, 255);
AF_DCMotor motor4(4, 255);

void setup() {
Serial.begin(9600); //Serial monitörü başlatıyoruz.
Serial.println("WAY!");// Serial monitöre başlangıçta WAY yazıyoruz buraya istediğinizi yazı isterseniz boş bırakın

void loop() {
  //Burada tekrardan hızları tek tek tanımlıyoruz.
motor1.setSpeed(255);  
motor2.setSpeed(255);  
motor3.setSpeed(255);
motor4.setSpeed(255);       
//Burada Serial 0dan büyük ise gelen veriyi okuyor
    if (Serial.available() > 0) {
    incomingByte = Serial.read();
    }
 
 // Sonra Switch case fonksiyonu ile caselerimizi tanımlıyoruz.
  
  switch(incomingByte)
  {
     case 'S':
         // motorların hepsi durucak
      { motor1.run(RELEASE);
       motor2.run(RELEASE); 
       motor3.run(RELEASE);
       motor4.run(RELEASE);
       Serial.println("DUR\n");
       incomingByte='*';}
      
     break;
     
     case 'F':
       // Motorlar ileri.
     {  motor1.run(FORWARD); 
       motor2.run(FORWARD); 
       motor3.run(FORWARD);
       motor4.run(FORWARD );
       Serial.println("İLERİ\n");
       incomingByte='*';}
     break;
    
      case 'B':
        // Motorlar geri
    {   motor1.run(BACKWARD);
       motor2.run(BACKWARD);
       motor3.run(BACKWARD);
       motor4.run(BACKWARD); 
       Serial.println("GERİ\n");
       incomingByte='*';}
     break;
     
     case 'R':
     // Motorlar sağa
     { motor1.run(FORWARD);
       motor2.run(RELEASE); 
       motor3.run(FORWARD);
       motor4.run(FORWARD);
       Serial.println("SAĞA\n");
       incomingByte='*';}
     break;

     
       case 'L':
        // Motorlar sola
      { motor1.run(RELEASE);
       motor2.run(FORWARD);   
       motor3.run(FORWARD);
       motor4.run(FORWARD);  
       Serial.println("SOLA\n");
       incomingByte='*';}
     break;
     
     
     
   
  }
}
