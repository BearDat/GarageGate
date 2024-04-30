#include <Servo.h>

/*   Pinout   */
#define btnDown 2               
#define btnUp 3                 

#define latchPin 9              
#define dataPin 8               
#define clockPin 10             
#define lightPin9 12            
#define lightPinLessThan9 11    
#define servoPin 5              
/*   Variables   */
int curNum = 0;                 
Servo servoMotor;               

/*   Constants   */
// numbers lol
byte segments[10] {B1000000,    // Number 0 needs all of the LEDs to be turned ON except LED "G"
                   B1111001,    // Number 1
                   B0100100,    // Number 2
                   B0110000,    //     .
                   B0011001,    //     .
                   B0010010,    //     .
                   B0000010,    //     .
                   B1111000,    //     .
                   B0000000,    //     .
                   B010000 };   // Number 8

/*   Setup Function - Doesnt repeat   */
void setup() {

    /*   Pin Modes I/O   */
    pinMode(btnDown, INPUT);                
    pinMode(btnUp, INPUT);                 

    pinMode(latchPin, OUTPUT);             
    pinMode(dataPin, OUTPUT);               
    pinMode(clockPin, OUTPUT);              

    pinMode(lightPin9, OUTPUT);             
    pinMode(lightPinLessThan9, OUTPUT);     

    servoMotor.attach(servoPin);            
    displayNumber(curNum);                  
}

/*   Loop Function - Repeats itself until arduino Reset   */
void loop() {
    /*   Check for Pressed Button Down   */
    if (digitalRead(btnDown)) {                             
        if (curNum > 0) { 
            curNum--;                         
            displayNumber(curNum);
            servoMotor.write(90);          
            delay(1000);                     
            servoMotor.write(-90);          
        }                        
        while (digitalRead(btnDown));                       
    }

    /*   Check for Pressed Button Up   */
    if (digitalRead(btnUp)) {                              
        if (curNum < 9) { 
            curNum++;                        
            displayNumber(curNum);
            servoMotor.write(90);          
            delay(1000);                     
            servoMotor.write(-90);          
        }                        
        while (digitalRead(btnUp));
    }

    // Turn on light for number 9
    if (curNum == 9) {
        digitalWrite(lightPin9, HIGH);
    } else {
        digitalWrite(lightPin9, LOW);
    }

    // Turn on light for numbers less than 9
    if (curNum < 9) {
        digitalWrite(lightPinLessThan9, HIGH);
    } else {
        digitalWrite(lightPinLessThan9, LOW);
    }
}

/*   Custom Functions   */
void displayNumber(int number) {                                
    digitalWrite(latchPin, LOW);                               
    shiftOut(dataPin, clockPin, MSBFIRST, segments[number]);    
    digitalWrite(latchPin, HIGH);                               
    delay(200);                                                 
}
