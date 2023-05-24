<div> 
  <h2>Introdução ao PWM </h2>
  <p><strong>PWM é a técnica usada para gerar sinais analógicos de um dispositivo digital como um Microcontrolador e ela é tão eficiente que hoje em dia quase todos os Microcontroladores modernos possuem hardware dedicado para a geração de sinais PWM.</strong></p>
</div>
<br>

<div>
  <h2>Componentes necessários </h2>
  <p><strong>Arduino nano , L293D , bateria 5V, um resistor 10k, um botão e um motor </trong></P>
</div>
<br>

<h2>Esquemático</h2>

![PWM](https://github.com/tamis2K/PWM/assets/90485488/8aa3a69b-2e3e-465c-8017-408244e5729c)


<br>

<h1>Código fonte</h1>

```javascript

#include <Arduino.h>


#define BUTTON_PIN 2
#define PWM 9


int estado_botao = 0;
int pwm = 0;
int ultimo_estado_botao = 0;
unsigned long tempo_acionado = 0;
unsigned long tempo_delay = 50;

void setup() {
  pinMode(PWM, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {

  int leitura = digitalRead(BUTTON_PIN);

  if (leitura != ultimo_estado_botao) {
    ultimo_estado_botao = leitura;
    if (leitura == HIGH) {  
      tempo_acionado = millis();
    }
  }

  if (leitura == HIGH && ((millis() - tempo_acionado) > tempo_delay && pwm < 255)) {
    pwm += 64;
    }else if (leitura == HIGH && ((millis() - tempo_acionado) > tempo_delay)){
    pwm = 0;
    }

  analogWrite(PWM, pwm);
  delay(50);
}
```

<h2>Funcionamento do projeto</h2>
<p><strong>Usando o Vs code e sua extensão PlatformIO criamos um novo projeto e usamos o código em cima para cada vês que o botão for pressionado a velocidade do motor aumente até o máximo  e depois retorne  para velocidade inicial.</strong></p>
