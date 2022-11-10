#include <LiquidCrystal_I2C.h>

// Primeiro é feita a definição dos pinos (o que está em cada pino)

const byte pinTrig = 8; // pino usado para disparar os pulsos do sensor
const byte pinEcho = 9; // pino usado para ler a saida do sensor
const byte pinBut = 2;  // pino usado para o push button

int PinoTemp = 0; //pino do sensor de temperatura

// define variáveis globais

byte state = 1;          // estado do menu
byte decimal = 0;        // número de casas decimais
String unity = "cm";     // descrição das unidades
double *result;          // uso do ponteiro para um double (obrigatório)


void setup()
{
  // pin mode - definie entradas e saídas digitais
  pinMode(pinBut, INPUT_PULLUP);   // pullup interno do Arduino

  // inicializa o sensor HC-SR04
  HCSR04.begin(pinTrig,pinEcho);
  
  // Inicializa a porta serial para leitura de dados
  Serial.begin(9600);

  // inicializa o lcd
  lcd.begin(16,2);          
}

void loop(){
  {
  readPushButton(); // verifica se o pushbutton foi acionado
  sowDisplay();     // exibe a distância no display lcd
  delay(150); // delay de 150ms
}
  switch (pressedButton) { // tem que crar a variavel pressed button pra
   // podedr saber qual dos botoes foi pressionado
    
    case 1:
//esse trecho teria que trocar mas não sei como
void readPushButton() { // verifica se o botão foi acionado
  if (!digitalRead(pinBut)) { // verifica se o botão foi acionado = LOW
    state >= 3 ? state = 0 : state = state;  
    state++;  
    while (!digitalRead(pinBut)) {} // aguarda soltar o botão
    lcd.clear();
    delay(150); // delay para reduzir o efeito bouncing
  }
  break;
  
  case 2:
  
   int reading = analogRead(PinoDoSensor);	       //Fazendo a leitura do pino A0, conectado ao sensor
 float tensao = reading * 5.0;			               //Convertendo a leitura em tensão.
 tensao /= 1024.0;							                   //Convertendo a tensão em dados (1024 faixas de dados)
 float TempC = (tensao - 0.5) * 100 ;		           //Converção de 10mV por ºC , com desvio de 
 Serial.println("Temperaturas Medidas");	         //Título
 Serial.print(TempC); Serial.println(" C");	       //Mostra no Monitor Serial a temperatura em ºC + unidade
 Serial.println("");						                   //Adiciona uma linha vazia para facilitar a leitura
  break;
  
}

//tá meio estranho esse trecho,mas não sei trocar tbm

void sowDisplay() { // exibe resultados no display LCD
  // faz leitura de acordo com o valor da variável state
  switch (state) {
    case 1:
    result = HCSR04.measureDistanceCm();     
    decimal = 0;
    unity = " cm";
    break;
}
