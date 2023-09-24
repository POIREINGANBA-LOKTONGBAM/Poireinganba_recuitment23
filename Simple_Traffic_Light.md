# :::Simple Traffic Light:::
In this challenge I used Tinkercad to create a simple 3 led traffic light where the light changes every time we push a button.
**required materials:**  
1. Arduino Uno.
2. LEDs (Red, Yellow, and Green).
3. Push button.
4. Resistors (220-330 ohms).
5. Breadboard.  
**Connections:**
1. Connect Annodes to port 2,3,4 respectively.
2. Connect the cathodes to individual resistors and then to GND of breadboard.
3. Connect one end of the push button to port 7 and the other to GND.
**Code:**
1. First we define the pin numbers with the corresponding connections of the LEDs and the button.
2. Then we give 2 variables: lightState(defines whic LED is on) and: buttonPressed(with boolean to tell if button is pressed or not)
3. We use setup() function to configure the pins we defined earlier. We set buttonPin as an input with a pull-up resistor to eliminate the need for an external resistor. We set redPin, yellowPin, and greenPin as outputs to control the LEDs. Finally, we call updateTrafficLight() to initialize the traffic light to the starting state (Red).
4. Next we make loop that checks the state of the push button. if the button is pressed the value goes low(0) else high(0)
5. In the if statement : lightState variable is incremented to cycle thruogh the led states. We call updateTrafficLight() to update the LEDs based on the new state. We set buttonPressed to true to prevent further state changes until the button is released and pressed again.
6. else statement checks If button is not pressed at all the button state stays high to prevent further changes.
7. The updateTrafficLight() function is responsible for updating the state of the LEDs based on the current lightState variable. It turns on and off the LEDs accordingly.

Link: https://www.tinkercad.com/things/6iIDEDD42Dw
