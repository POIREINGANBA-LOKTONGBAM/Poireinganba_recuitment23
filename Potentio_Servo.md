# !::Potntio_Servo::!
**Materials Requried:**
1. Potentiometer
2. Servo Motor
3. Arduino uno

**Connections:**
1. Connect one leg of the potentiometer to the 5V power source on the Arduino.
2. Connect the other to GND.
3. Connect the wiper of the potentiometer to one of the analog input pins on the Arduino(A0)
4. Connect the signal wire of the servo to pin 9, power to 5v and ground to GND.

**Code:**
1. Include the Servo Library
2. We create an instance 'Myservo' To controll the servo motor.
3. We need two variabels , one that stores the analog pin and other that stores the value read from the potentio meter.
4. Another variable 'servoAngle' that stores the angle (in degrees) to which the servo motor should be positioned.
5. In the setup function: myservo.attach(9): tells Arduino that pin 9 is for servo motor.
6. In the loop function: potValue = analogRead(potPin);: This line reads the analog voltage from the potentiometer connected to pin A0. The analogRead function converts this voltage into a value between 0 and 1023 and stores it in potValue.
'servoAngle' = map(potValue, 0, 1023, 0, 180);: The map function is used to map the potValue (ranging from 0 to 1023) to a servo angle between 0 and 180 degrees. This means that when you turn the potentiometer knob, it will change the servo angle accordingly.
myservo.write(servoAngle);: This line sets the servo angle to the value calculated in the previous step using myservo.write. This command actually controls the position of the servo motor.

Link: https://www.tinkercad.com/things/encEozEZoLj
