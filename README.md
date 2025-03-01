# Control-using-MAC-
ESP-NOW Button-LED Toggle System
This project demonstrates how to use the ESP-NOW protocol to send and receive data between two ESP32 devices. One device controls an LED based on a button press, while the other device toggles the LED state when it receives a signal.

Features
ESP-NOW Communication: Two ESP32 devices communicate using ESP-NOW.
Button Input: A button press on one ESP32 device sends a signal to toggle the LED on the other ESP32 device.
LED Control: The LED on the second ESP32 device turns on or off based on the received signal.
Components
2 x ESP32 Development Boards: One for sending the button press signal, the other for receiving the signal and controlling the LED.
1 x Push Button: Connected to the first ESP32 to trigger the toggle action.
1 x LED: Connected to the second ESP32 to show the toggle effect.
Jumper Wires and Breadboard for connections.
Pin Configuration
Button: Pin 4 (Input, configured with INPUT_PULLUP mode)
LED: Pin 5 (Output)
Installation
Hardware Setup
First ESP32 (Sender):

Connect the button to Pin 4.
Connect the ESP32 to your computer for programming.
Second ESP32 (Receiver):

Connect an LED to Pin 5.
Connect the ESP32 to your computer for programming.
Software Setup
Arduino IDE: Make sure you have the ESP32 board support installed in the Arduino IDE. If not, follow these instructions to install ESP32.
Upload Code: Open the provided code in the Arduino IDE, select the appropriate ESP32 board, and upload the code to both devices.
Communication Setup
Receiver MAC Address: In the code, the receiverMAC array contains the MAC address of the second ESP32 (receiver). You need to replace it with the MAC address of the actual ESP32 you are using as the receiver. You can obtain the MAC address of an ESP32 using the following code:
cpp
Copy
void setup() {
  Serial.begin(115200);
  Serial.println(WiFi.macAddress());
}
Run this code on the receiver ESP32 to obtain its MAC address and replace it in the receiverMAC[] array of the sender ESP32.

Code Explanation
ESP-NOW Communication: The sender ESP32 sends a signal with the message "toggle" to the receiver ESP32 when the button is pressed.
LED Toggle: The receiver ESP32 listens for the signal and toggles the LED state when it receives the "toggle" message.
Button Debouncing: The button press is debounced using a time check (debounceDelay), so multiple presses are not registered in quick succession.
Functions:
OnDataSent: Callback function to handle the status of the data transmission.
OnDataRecv: Callback function to handle incoming data and toggle the LED on the receiver device.
Button Press: The sender device checks for button presses and sends a "toggle" message when pressed.
Usage
Upload the Code: Upload the provided code to both ESP32 boards using the Arduino IDE.
Set Up Devices: Power both ESP32 devices. One should have the button connected, and the other should have the LED connected.
Test Communication: Press the button on the sender device. It should send a signal to the receiver device, toggling the LED on or off.
Troubleshooting
If the devices do not communicate, ensure both devices are within range of each other and that their MAC addresses are correctly set in the sender device.
If the LED does not toggle, check the wiring of the LED and ensure it is correctly connected to the correct pin.
Ensure that esp_now_init() is successfully initialized and that both devices are added as peers using esp_now_add_peer().
Future Improvements
Multiple Buttons and LEDs: You can add more buttons and LEDs to control multiple devices or implement more complex interactions.
Encryption: Implement ESP-NOW encryption for secure communication between devices.
Button Hold Detection: Add functionality to handle long button presses for different actions.
