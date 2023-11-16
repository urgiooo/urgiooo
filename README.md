const int trigPin = 9;
const int echoPin = 10;
const int buzzer = 11;
const int ledPin = 13;
const int ledPin2 = 6;
const int ledPin3 = 7;
long duration;
int distance;
int safetyDistance;


void setup() 
{
pinMode(trigPin, OUTPUT); 
pinMode(echoPin, INPUT); 
pinMode(buzzer, OUTPUT);
pinMode(ledPin, OUTPUT);
pinMode(ledPin2, OUTPUT);
pinMode(ledPin3, OUTPUT);
Serial.begin(9600);
}


void loop() 
{

digitalWrite(trigPin, LOW);
delayMicroseconds(2);
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);
distance= duration*0.034/2;
safetyDistance = distance;

if (safetyDistance <= 30){
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin2, HIGH);
}
else{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin2, LOW);
}

if (safetyDistance <= 15){
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin3, HIGH);
  digitalWrite(ledPin2, LOW);
}
else{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin3, LOW);
}

if (safetyDistance <= 5){
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin, HIGH);
  digitalWrite(ledPin2, LOW);
  digitalWrite(ledPin3, LOW);
}
else{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin, LOW);
}
Serial.print("Distance: ");
Serial.println(distance);
}
