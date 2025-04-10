---
layout: page
title: Week 9 - Networking
description: 
img: assets/img/Project9/networking-event.jpg
importance: 9
category: work
giscus_comments: false
---

This week Jordan and I worked on the part of my final project which requires sending a lot of data from hardware to Unity through the wifi.


Originally, I was just using sending data on a timer to Unity, but for this week I switched to using web sockets which were a little trickier to set up. Unfornunately, there was no built-in Unity packages for recieving websockets, so it took trying a few plug ins from github before it actually started to work. There was a little more work to do making sure that if there wasn't currently a tag being held in front of the scanner it should return 00. 

The next thing to do on the agenda was create some sort of system for detecting different objects/parts. From the design review, it seemed like RFID would work the best.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project9/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

After getting the RFID to work, I knew I had to come back to thing I was most dreading, getting the acceleration on the MPU6050 to work properly. I tried so many things. I tried to make a 3D project, but it was impossible to keep still. I went back to the 2D project, and eventually fixed the drifting, but the biggest problem was whenever you made a quick motion the accelerometer then gave you the opposite direction directly aftwerwards and the character would snap back. The closest I got was when the input was above a threshold it would try to ignore the next couple inputs. This kind of worked, but felt terrible to play. Even without the snapping back problem, the direction felt too random to be fun. In the end, I came up with a new solution, which was to use the forward axis of rotation to push the character forward and backward. After a little tweaking, this method feels by far the best to control and it requires no dealing with the acceleration. 

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project9/2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

There was a problem where it was easy to get the character offset just by moving it around. To fix this, I added a button to the breadboard which when pressed stops the movement and rotation,allowing you to reset where you want the character.

The next struggle was combining all the code. One strange part was when the MPU6050 and RFID scanners were using the same pin, and it was fixed by just taking out a wire from the RFID scanner and it still worked. 

Here is the final result (At certain points it's not moving because I'm holding down the button).

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project9/PS70P9.gif" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Sorry the amount of text, it was a very coding heavy week. 

Arduino Code:

{% highlight javascript %}
#include <WiFi.h>
#include <WebSocketsServer.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <Wire.h>
#include <MFRC522v2.h>
#include <MFRC522DriverSPI.h>
#include <MFRC522DriverPinSimple.h>
#include <MFRC522Debug.h>

// ==== WiFi Settings ====
const char* ssid = "MAKERSPACE";
const char* password = "12345678";

// ==== WebSocket Server ====
WebSocketsServer webSocket = WebSocketsServer(81);

// ==== MPU6050 Setup ====
Adafruit_MPU6050 mpu;

// ==== RFID Setup ====
MFRC522DriverPinSimple ss_pin(5); // RFID CS pin on GPIO 5
MFRC522DriverSPI driver{ss_pin};
MFRC522 mfrc522{driver};

// ==== Button Setup ====
const int buttonPin = 4;

// ==== Timers ====
unsigned long lastDataSendTime = 0;
const int sendInterval = 20;

String lastUID2chars = "00"; // stores RFID short code
unsigned long lastCardTime = 0;
const unsigned long cardTimeout = 1000; // 1 second

// ==== WebSocket Event Handler ====
void webSocketEvent(uint8_t num, WStype_t type, uint8_t * payload, size_t length) {
  switch (type) {
    case WStype_DISCONNECTED:
      Serial.printf("WebSocket client #%d disconnected\n", num);
      break;
    case WStype_CONNECTED: {
        IPAddress ip = webSocket.remoteIP(num);
        Serial.printf("WebSocket client #%d connected from %d.%d.%d.%d\n", num, ip[0], ip[1], ip[2], ip[3]);
      }
      break;
    case WStype_TEXT:
      Serial.printf("Received text from client #%d: %s\n", num, payload);
      break;
    default:
      break;
  }
}

void setup() {
  Serial.begin(115200);
  pinMode(buttonPin, INPUT_PULLUP);

  // ==== WiFi Connection ====
  Serial.println("Connecting to WiFi...");
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nConnected to WiFi");
  Serial.print("ESP32 IP Address: ");
  Serial.println(WiFi.localIP());

  // ==== WebSocket Start ====
  webSocket.begin();
  webSocket.onEvent(webSocketEvent);
  Serial.println("WebSocket server started on port 81");

  // ==== MPU6050 Init ====
  Serial.println("Initializing MPU6050...");
  if (!mpu.begin()) {
    Serial.println("Failed to find MPU6050 chip");
    while (1) { delay(10); }
  }
  Serial.println("MPU6050 Found!");
  mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
  mpu.setGyroRange(MPU6050_RANGE_1000_DEG);
  mpu.setFilterBandwidth(MPU6050_BAND_5_HZ);
  Serial.println("MPU6050 configured");

  // ==== RFID Init ====
  Serial.println("Initializing RFID...");
  mfrc522.PCD_Init();
  MFRC522Debug::PCD_DumpVersionToSerial(mfrc522, Serial);
  Serial.println("RFID Ready.");
}

bool cardIsPresent = false;

void loop() {
  webSocket.loop();

  // Check if a card is currently held over the reader
  cardIsPresent = mfrc522.PICC_IsNewCardPresent() && mfrc522.PICC_ReadCardSerial();

  // If a card is present, store the UID
  if (cardIsPresent) {
    String uidString = "";
    for (byte i = 0; i < mfrc522.uid.size; i++) {
      if (mfrc522.uid.uidByte[i] < 0x10) uidString += "0";
      uidString += String(mfrc522.uid.uidByte[i], HEX);
    }

    lastUID2chars = uidString.substring(0, 2);
    lastUID2chars.toUpperCase();
    lastCardTime = millis();

    Serial.println("Scanned RFID UID: " + uidString);
    Serial.println("Stored Tag: " + lastUID2chars);

    mfrc522.PICC_HaltA();
    mfrc522.PCD_StopCrypto1();
  }

  // Use timeout to clear tag **only if card hasn't been present for a while**
  if (millis() - lastCardTime > cardTimeout) {
    lastUID2chars = "00";
  }

  // Send data every 20ms
  unsigned long currentTime = millis();
  if (currentTime - lastDataSendTime >= sendInterval) {
    lastDataSendTime = currentTime;

    // Get MPU6050 sensor readings
    sensors_event_t a, g, temp;
    mpu.getEvent(&a, &g, &temp);

    // Read button
    int buttonState = digitalRead(buttonPin);
    float buttonValue = (buttonState == LOW) ? 1.0 : 0.0;

    // Build and send message
    String dataString = String("ACC,") +
      String(a.acceleration.x, 2) + "," +
      String(a.acceleration.y, 2) + "," +
      lastUID2chars + "," +
      String(buttonValue, 2) + ",GYRO," +
      String(g.gyro.x, 2) + "," +
      String(g.gyro.y, 2) + "," +
      String(g.gyro.z, 2) + ",";

    webSocket.broadcastTXT(dataString);
    Serial.println("Sent: " + dataString);
  }
}



Unity Code:

{% highlight javascript %}
using UnityEditor.ShaderGraph.Internal;
using UnityEngine;
using WebSocketSharp;

public class PlayerPhysicalControls : MonoBehaviour
{
    public string esp32IP = "192.168.0.118";
    public int port = 81;

    public float moveSpeed = 5f;
    public float rotationSpeed = 100f;
    public float gyroSensitivity = 5f;
    public bool invertGyro = true;

    public float gyroForwardThreshold = 0.2f; // Adjust this based on your ESP32 data
    public float gyroBackwardThreshold = -0.2f;

    private WebSocket ws;

    private float angle = 0f;
    private Vector3 currentGyro = Vector3.zero;

    private Rigidbody2D rb;
    public float holdingButton;

    public string tagPin;

    private SpriteRenderer renderer;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
        renderer = GetComponent<SpriteRenderer>();
        ConnectToESP32();
    }

    void ConnectToESP32()
    {
        string wsUrl = "ws://" + esp32IP + ":" + port + "/";
        ws = new WebSocket(wsUrl);

        ws.OnOpen += (sender, e) =>
        {
            Debug.Log("Connected to ESP32 WebSocket!");
        };

        ws.OnMessage += (sender, e) =>
        {
            ProcessMessage(e.Data);
        };

        ws.OnError += (sender, e) =>
        {
            Debug.LogError("WebSocket error: " + e.Message);
        };

        ws.OnClose += (sender, e) =>
        {
            Debug.Log("WebSocket closed: " + e.Reason);
        };

        ws.ConnectAsync();
    }

    void Update()
    {
        // Apply gyro-based rotation
       
        
        float rotationChange = currentGyro.z * gyroSensitivity * (invertGyro ? -1 : 1);
        
        if (holdingButton >= .5f)
        {
            rotationChange = 0;
        }
        
        angle += rotationChange;
        
        transform.rotation = Quaternion.Euler(0f, 0f, angle);
        
        print(tagPin);

        if (tagPin == "7C")
        {
            renderer.material.color = Color.blue;
        } else if (tagPin == "1C")
        {
            renderer.material.color = Color.red;
        }
        else
        {
            //print("White");
            renderer.material.color = Color.white;
        }
        
        //print("Button: " +holdingButton+ "X: " + currentGyro.x + " Y: " + currentGyro.y + " Z: " + currentGyro.z);
    }

    void FixedUpdate()
    {
        if (holdingButton >= .5f)
        {
            rb.linearVelocity = Vector2.zero;
            return;
        }
        
        Vector2 moveDirection = Vector2.zero;

        // Forward or backward movement depending on z-axis rotation
        if (currentGyro.x > gyroForwardThreshold)
        {
            moveDirection = transform.right; // Forward
        }
        else if (currentGyro.x < gyroBackwardThreshold)
        {
            moveDirection = -transform.right; // Backward
        }

        if (rb != null)
            rb.linearVelocity = moveDirection * moveSpeed;
        else
            transform.position += (Vector3)moveDirection * moveSpeed * Time.fixedDeltaTime;
    }

    void ProcessMessage(string message)
    {
        string[] tokens = message.Split(',');

        if (tokens.Length >= 9 && tokens[0] == "ACC" && tokens[5] == "GYRO")
        {
            string rfidShort = tokens[3]; // RFID (e.g., "7C")
        
            if (
                float.TryParse(tokens[4], out float bt) && // button
                float.TryParse(tokens[6], out float gx) &&
                float.TryParse(tokens[7], out float gy) &&
                float.TryParse(tokens[8], out float gz))
            {
                tagPin = rfidShort;
                holdingButton = bt;
                currentGyro = new Vector3(gx, gy, gz);
            }
            else
            {
                Debug.LogWarning("Failed to parse sensor data: " + message);
            }
        }
        else
        {
            Debug.LogWarning("Received data in unexpected format: " + message);
        }
    }

    void OnDestroy()
    {
        if (ws != null)
            ws.Close();
    }
}

{% endhighlight %}