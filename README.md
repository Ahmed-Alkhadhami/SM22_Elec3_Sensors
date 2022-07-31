# Electric Task 3 : Designing a sensor circuits/systems






<img src="https://user-images.githubusercontent.com/107868473/182018243-be5ba879-03c1-4d6a-b58b-e7ba857eac14.png" width=35% height=35%>

Generally , there are two types of sensors:
* Analog Sensor
* Digital sensor  
We will give a simple example for each one in this repository Insha'a Allah.

<br/>

---

<br/>

## Analog Sensor
it's a sensor that produces a continuous analog output , that can be even fractional numbers.

### Component List :
* Arduino UNO
* LDR
* 2 PullDown Resistor (1 kΩ)
* Multimeter
* LED

<br/>

### Circuit Diagram
![image](https://user-images.githubusercontent.com/107868473/182019020-2ed9bb40-1ea5-485f-af04-b48dc2381ec4.png)

<br/>


### Idea Of The Code :
**General :**  
We will read the analog value/signal from the LDR sensor , then send it to the multimeter & LED , so we can sight the variation.

<br/>

**Explaining The Code :**  
1 - Pins 
* Defining a variable for the LDR input/read.
* Connecting the LDR to analog pin A5.
```bash
int sensorValue = 0;
byte LDR = A5;
```

2 - Initializing  
- Initializing status of each used pins whether it's IN or OUT.  
LDR is input , and variable digital pin 9 is output (for multimeter & LED).
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












## More Information
Push Button diagram  
![Push-button-Pinout](https://user-images.githubusercontent.com/107868473/180780878-b579ffa5-b229-417e-9d24-66cdb6199e6d.gif)

<br/>
<br/>

## Online Simulation link (testing) :
[**Wokwi**](https://wokwi.com/projects/338154709936243283)  
 

https://user-images.githubusercontent.com/107868473/181051676-99168938-6fec-453b-b254-3e8ae78ac946.mp4


  
<br/>
<br/>
<br/>
<br/>






---
This is the submission for week 3 tasks of the Electric path at Smart Method training of 2022.
