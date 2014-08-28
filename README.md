BLE Chat

This Android App works with a HM-10 BLE module.  It can be used for communication between an Android device and a microcontroller.

It has been tested on a Galaxy SIII and a HM-10 module hooked up to an Arduino UNO..  

See the HM-10 datasheet for the correct pinout.  The tested module had:

PIN 1 =>  ARDUINO 0 (RX), 
PIN 2 => ARDUINO 1 (TX), 
PIN 12 => 3.3V, PIN 13 => GND 
PIN 23 => LED +.  

There was also a 0.1uF capacitor between VCC and ground and a 470 OHM resistor between PIN 23 and the LED. 

There seems to be a 21 character (20 characters plus a newline) limit on serial data, at least on the firmware tested.  The app limits data input to 20 characters. 

There is a text field and a SEND button to send data and a list that displays data coming in via serial,  similar to the Google standard Bluetooth Chat sample app.

This code is a slightly modified version of the BT4LEDTest app written by danasf available here:  https://github.com/danasf/hm10-android-arduino 

That code was based on the Google BLE example called BluetoothLeGatt available here:  https://developer.android.com/samples/BluetoothLeGatt/index.html

Below is an Arduino sketch that will echo characters from the serial port that can be used to test BLE Chat.



/*
    BLE_echo
    
    Test a serial connection to a HM-10
    BLE module by reading incoming data
    and writing it back out the serial
    port.
    
*/

const int BUFF_LEN = 21;      // serial buffer length

char sBuff[BUFF_LEN];         // serial buffer

void setup()
{
  Serial.begin(9600);      // open serial port
  
  Serial.setTimeout(20);  // timeout defaults to 1000 ms

}

void loop()
{

  // while bytes available ;
  if( Serial.available() )
  {
    // read into buffer
    int bytesRead = Serial.readBytes(sBuff, BUFF_LEN);
    
    // echo read bytes to serial port
    for(int i=0; i < bytesRead; i++) Serial.write(sBuff[i]);

    
  } // if


}




