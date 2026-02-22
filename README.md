# Aplicação da Camada

## (1) Objetivos

* Atividade prática para aplicação dos conceitos da camada física de redes de computadores;
* Entendimento do bit-a-bit de uma transmissão TX/RX;
* Entendimento da tabela ASCII;
* Análise por no gráfico do sinal usando osciloscópio;
* Responder ao desafio do Kahoot durante a aula;


## (2) Sinal no Cabeamento numa Transmissão/Recepção

Quando enviamos uma mensagem pela rede, o que realmente viaja no fio?

- não são letras;
- não são pacotes ainda;
- são bits elétricos;
- conjunto de bits formam bytes, conjunto de bytes formam dados.
- Por exemplo, vamos enviar a letra ```a```


<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig1.png" width="400">


## (3) Tabela ASCII

* American Standard Code for Information Interchange

* É um padrão que associa cada caractere a um número.

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig2.jpg" width="1200">

* O computador não envia letras, envia números.

* Esses números são representados em binário e transmitidos como sinais elétricos.

**Portanto:**

1) Tabela ASCII associa cada caractere a um número
2) Esse número vira binário
3) O binário vira sinal elétrico
4) O sinal viaja pelo fio

## (4) Kahoot (pergunta teste) Conversão de base numérica

## (5) Roteiro Prático Simulado

**(5.1)** Abra o [https://www.tinkercad.com/dashboard]

**(5.2)** Monte este circuito

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig3.png" width="800">

**(5.3)** Use esse código no Arduino TX

```
// C++ code
//

void setup()
{
  Serial.begin(9600);
}

void loop()
{
  Serial.write("a");
}
```

**(5.4)** Use esse código no Arduino RX

```
// C++ code
//

void setup() {
  Serial.begin(9600);
}

void loop() {
  if (Serial.available() > 0) {
    char c = Serial.read();   // lê 1 byte
  }
}
```

