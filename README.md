# Electric Task 3 : Designing A Sensor Circuits/Systems




<img src="https://user-images.githubusercontent.com/107868473/182018243-be5ba879-03c1-4d6a-b58b-e7ba857eac14.png" width=35% height=35%>

Generally , there are two types of sensors:
* Analog Sensor
* Digital Sensor  
We will give a simple example for each one in this repository Insha'a Allah.

<br/>

---

<br/>

# Analog Sensor
it's a sensor that produces a continuous analog output , that can be even fractional numbers. The sensor we will use for our example is an LDR (light-dependent resistor) , which is a component that decreases resistance with respect to receiving luminosity (light) on the component's sensitive surface.

## Component List :
* Arduino UNO
* LDR
* 2 Pull Down Resistors (1 kΩ)
* Multimeter
* LED

<br/>

## Circuit Diagram
![image](https://user-images.githubusercontent.com/107868473/182019020-2ed9bb40-1ea5-485f-af04-b48dc2381ec4.png)

<br/>


## Idea Of The Code :
### General :
We will read the analog value/signal from the LDR sensor , then send it to the multimeter & LED , so we can sight the variation.

<br/>

### Explaining The Code :
1 - Pins 
* Defining a variable for the LDR input/read.
* Connecting the LDR to analog pin A5.
```bash
int sensorValue = 0;
byte LDR = A5;
```

2 - Initializing  
- Initializing status of each used pins whether it's IN or OUT.  
LDR is input , and PWM digital pin 9 is output (for multimeter & LED).
- Starting the serial monitor to see the input value changes on the screen.
```bash
void setup ( )
{
  pinMode(LDR,INPUT);
  pinMode(9,OUTPUT);
  Serial.begin (9600);
}
```

3- Main Code / Loop
- Assigning the read value from the LDR to the variable **sensorValue** .
- Printing the exact value of **sensorValue** in the serial monitor.
- Sending the value of **sensorValue** to the multimeter & LED after mapping (changing or maping that range of LDR values (0-1023) to a different range (readable range by the other components ))

```bash
void loop ()
{
  sensorValue = analogRead(LDR)  ;
  Serial.println(sensorValue);
  analogWrite(9 , map (sensorValue , 0,1023 ,0,255));
}
```


<br/>
<br/>


## Online Simulation link (testing) :
[**TinkerCad**](https://www.tinkercad.com/things/lw5mnreFti4-fabulous-bombul-gaaris/editel?tenant=circuits)  
 
<br/>

https://user-images.githubusercontent.com/107868473/182021716-a5ddb9bd-c6fa-434c-90b0-86de84e1cb7d.mp4




  
<br/>
<br/>

# Digital Sensor
it's an electronic or electrochemical sensor, where data is digitally converted and transmitted. We will be using an IR (IR stands for Infra red) for this part.

## Component List :
* Arduino UNO
* IR Sensor
* IR Remote
* 3 Pull Down Resistors (1 kΩ)
* 3 LEDs


<br/>

## Circuit Diagram
![image](https://user-images.githubusercontent.com/107868473/182041009-30b171a0-26fa-4556-95a4-a9b8c5869f85.png)

<br/>


## Idea Of The Code :
### General :
Pressing the remote buttons will send a signal to the IR sensor , which will be translated through the code to any action we want.  
I programmed 6 buttons to present a simple example :
* button 1 : will turn blue led ON for 0.5 sec.
* button 2 : will turn green led ON for 0.5 sec.
* button 3 : will turn orange led ON for 0.5 sec.
* button 4 : will turn all LEDs ON (from left to right) , each  for 0.5 sec.
* button 5 : will turn all LEDs ON, green first then the other two , each  for 0.5 sec.
* button 6 : will turn all LEDs ON (from right to left) , then it will all go OFF together.

<br/>

### Explaining The Code :
1 - Pins 
* Connecting the LEDs to pins 8 , 9 and 10.
* Connecting the IR sensor to pin 3.
```bash
int BlueLed = 10;
int GreenLed = 9;
int OrangeLed  = 8;

int RECV_PIN = 3;
```

2 - Initializing  
**Librarary lines :**  
* define the input pin that connected to the IR sensor.
* assigning a "true" value to the variable __results__ (if any signal is received , a "true" value will come up)
```bash
IRrecv irrecv(RECV_PIN);
decode_results results;
```

**set up**  
- Initializing status of each used pins for all LEDs (all OUT for sure).
- Starting the serial monitor to see the input value changes on the screen.
will need this absolutely to know the value of each button , to determine the cases in the code.  
also , printing the string in the serial monitor to indicate when it's started.
- 
```bash
void setup()
{
  //Set Led Pins
  pinMode(BlueLed, OUTPUT);
  pinMode(GreenLed, OUTPUT);
  pinMode(OrangeLed   , OUTPUT);
  
  
  //Enable serial usage and IR signal in
  Serial.begin(9600);
  Serial.println("Enabling IRin");
  irrecv.enableIRIn(); 
  Serial.println("Enabled IRin");
}
```

3- Main Code / Loop
in simple & breif words :
* Using an **if** which will  will  check if there is signal coming from the remote , if yes then assign its value to variable **value**.
* compare the value of **value** with the written cases , if any match , then run it. (all cases mentioned previously)

```bash
void loop()
{
  if (irrecv.decode(&results)) {//irrecv.decode(&results) returns true if anything is recieved, and stores info in varible results
    unsigned int value = results.value; //Get the value of "results" as an unsigned int, so we can use switch case
    Serial.println(value);
    switch (value) {
      case 2295: 
      digitalWrite(BlueLed , HIGH);
      delay(500);
      digitalWrite(BlueLed , LOW);
      break;   

      case 34935:
      digitalWrite(GreenLed  , HIGH);
      delay(500);
      digitalWrite(GreenLed  , LOW);
      break;
      
      case 18615:
      digitalWrite(OrangeLed , HIGH);
      delay(500);
      digitalWrite(OrangeLed   , LOW);
      break;
      
      // 3 more cases , no need to present them ... it's too long to be showed & nothing new
      
    
    }
    irrecv.resume(); // Receive the next value
  }
}
```

<br/>


## Online Simulation link (testing) :
[**TinkerCad**](https://www.tinkercad.com/things/c7rpsbLO3Vr-terrific-inari/editel?tenant=circuits)  
 
<br/>



https://user-images.githubusercontent.com/107868473/182042127-82a04ede-0ee0-4f2c-a66e-8feff51baaf6.mp4





---
This is the submission for week 4 tasks of the Electric path at Smart Method training of 2022.
