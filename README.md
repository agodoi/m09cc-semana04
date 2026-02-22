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


<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig1.png" width="500">


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

## (5) Comunicação UART TX/RX e como Por No Gráfico

* UART = Universal Asynchronous Receiver/Transmitter
* É um método de comunicação serial que:
  - envia dados bit a bit;
  - usa apenas um fio para transmitir (TX) e outro para receber (RX);
  - não usa clock compartilhado;
  - sincroniza cada byte usando start e stop bits.

👉 É chamada assíncrona porque não existe um fio de clock.

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig4.png" width="500">
Obs: o trem de pulsos do gráfico não bate com a sequência binária. GPT está desobediente. 

## (6) Roteiro Prático Simulado

**(6.1)** Abra o [https://www.tinkercad.com/dashboard]

**(6.2)** Monte este circuito

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig3.png" width="500">

**(6.3)** Use esse código no Arduino TX

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

**(6.4)** Use esse código no Arduino RX

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
**(6.5)** Configure o osciloscópio para 500us no tempo/div;

**(6.6)** Dê play no simulador do Tinkercad;

**(6.7)** Dê o máximo de zoom na tela do oscilas até preencher quase toda a sua tela do PC e tire um print para congelar a imagem. Observando este print, responda:

**(6.8)** Olhando para o desenho, encontre os bits do caracter que está sendo transmitido no software;

**(6.9)** Agora, identifique onde está o **bit start** e o **bit stop** e marque-os com a ajuda de um POST-IT sobre a sua tela. Desjeito assim:

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig6.jpeg" width="500">

**(6.10)** Percebe o **bit stop** está à direita do dado no gráfico? E que o **bit start** está à esquerda? Por que isso?

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig5.jpeg" width="500">

**(6.11)** Tome cuidado para não sair do Kahoot. Tire uma foto da sua tela mostrando o post-it marcando 2 QUADROS sinalizando START - DADO - STOP de cada quadro. Envie esta foto para o professor via slack para deixar registrado.

## (7) Comunicação UART TX/RX no Osciloscópio

**(7.1)** Forme um grupo de 5 pessoas;

**(7.2)** Pegue com o professor um kit:

- 01 Arduino Uno;
- 01 Oscilosópio;
- 01 ponta de prova.
- 01 cabo USB para gravar o Arduino;
- jumpers para ler dados.

**(7.3)** Grave o seguinte código no Arduino Uno:

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

**(7.4)** Conecte a ponta de prova do osciloscópio no pino TX do Uno usando um jumper macho-macho;

**(7.5)** Ligue o oscilas e pressione o botão RUN/STOP que fica no canto direito superior olhando para o aparelho;

**(7.6)** Tente congelar o sinal no display mexendo lentamente no botão TRIGGER, que também fica à direita olhando para o aparelho;

**(7.7)** Você também pode ajusar melhor o sinal para o centro da tela mexendo no botão < POSITION>, e também, pode esticar o sinal girando no botão SEC/DIV para a direita. Volte no item **(7.6)** para recongelar o sinal;


