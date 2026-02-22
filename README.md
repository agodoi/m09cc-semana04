
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

# Kahoot - Pergunta 1 

# Kahoot - Pergunta 2 

## (4) Comunicação UART TX/RX e como Por No Gráfico

* UART = Universal Asynchronous Receiver/Transmitter
* É um método de comunicação serial que:
  - envia dados bit a bit;
  - usa apenas um fio para transmitir (TX) e outro para receber (RX);
  - não usa clock compartilhado;
  - sincroniza cada byte usando start e stop bits.

👉 É chamada assíncrona porque não existe um fio de clock.

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig4.png" width="500">
Obs: o trem de pulsos do gráfico não bate com a sequência binária. GPT está desobediente.

## Outras configurações possíveis do UART

O UART permite diferentes formatos de frame, variando quantidade de bits de dados, uso de paridade e número de bits de parada.

| Configuração | Bits de dados | Paridade | Bits de stop | Total de bits no frame* | Quando é usada / Observação |
|-------------|--------------|----------|--------------|--------------------------|------------------------------|
| **8N1** | 8 | Nenhuma | 1 | 10 | Padrão mais comum em Arduino, ESP32 e PCs |
| **7E1** | 7 | Par (Even) | 1 | 10 | Sistemas antigos, telemetria e comunicação com modems |
| **7O1** | 7 | Ímpar (Odd) | 1 | 10 | Equipamentos industriais legados |
| **8E1** | 8 | Par (Even) | 1 | 11 | Quando precisa de detecção simples de erro |
| **8O1** | 8 | Ímpar (Odd) | 1 | 11 | Alternativa à paridade par para verificação |
| **8N2** | 8 | Nenhuma | 2 | 11 | Usado quando receptor precisa de mais tempo para processar |
| **7E2** | 7 | Par (Even) | 2 | 11 | Protocolos industriais específicos |

\*Total de bits considera: **1 start + dados + paridade (se houver) + stop**

### Exemplo de leitura

- **8N1** → 1 start + 8 dados + 1 stop = 10 bits  
- **8E1** → 1 start + 8 dados + 1 paridade + 1 stop = 11 bits  
- **8N2** → 1 start + 8 dados + 2 stop = 11 bits  

### Observação importante

Maior número de bits no frame significa:

- mais confiabilidade (detecção de erro / sincronização)
- porém menor eficiência (mais bits para enviar o mesmo dado)


O **bit de paridade** é um bit extra enviado junto com os dados para **detectar erros simples de transmissão**. Ele não corrige o dado. Como funciona?

* Ele verifica se a quantidade de bits `1` no byte é:
  - **Paridade par (Even):** o total de `1`s deve ser **par**
  - **Paridade ímpar (Odd):** o total de `1`s deve ser **ímpar**
* Se o receptor contar e o resultado não bater, sabe que **houve erro no envio**. Exemplo:

Dados:

```
01000001   (letra 'A')
```

Número de `1`s = 2 (par)

* Paridade **par** → bit = `0` (continua par)
* Paridade **ímpar** → bit = `1` (fica ímpar)
<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig7.png" width="500">


# Kahoot - Pergunta 3

# Kahoot - Pergunta 4

## (5) Roteiro Prático Simulado

**(5.1)** Abra o [https://www.tinkercad.com/dashboard]

**(5.2)** Monte este circuito

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig3.png" width="500">

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
**(5.5)** Configure o osciloscópio para 500us no tempo/div;

**(5.6)** Dê play no simulador do Tinkercad;

**(5.7)** Dê o máximo de zoom na tela do oscilas até preencher quase toda a sua tela do PC e tire um print para congelar a imagem. Observando este print, responda:

**(5.8)** Olhando para o desenho, encontre os bits do caracter que está sendo transmitido no software;

**(5.9)** Agora, identifique onde está o **bit start** e o **bit stop** e marque-os com a ajuda de um POST-IT sobre a sua tela. Desjeito assim:

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig6.jpeg" width="500">

**(5.10)** Percebe o **bit stop** está à direita do dado no gráfico? E que o **bit start** está à esquerda? Por que isso? Para manter a sua autonomia, caso não saiba a resposta, pode jogar no GPTo que ele te responde ou pode perguntar para o prof. Note também que o LSB (Least Significant Bit) é o primeiro a ser transmitido

**(5.11)** Tome cuidado para não sair do Kahoot. Tire uma foto da sua tela mostrando o post-it marcando 2 QUADROS sinalizando START - DADO - STOP de cada quadro. Envie esta foto para o professor via slack para deixar registrado.

# Kahoot - Pergunta 5

# Kahoot - Pergunta 6

# Kahoot - Pergunta 7

# Kahoot - Pergunta 8

## (6) Comunicação UART TX/RX no Osciloscópio

**(6.1)** Forme um grupo de 5 pessoas;

**(6.2)** Pegue com o professor um kit:

- 01 Arduino Uno;
- 01 Oscilosópio;
- 01 ponta de prova.
- 01 cabo USB para gravar o Arduino;
- jumpers para ler dados.

**(6.3)** Grave o seguinte código no Arduino Uno:

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

**(6.4)** Conecte a ponta de prova do osciloscópio no pino TX do Uno usando um jumper macho-macho;

**(6.5)** Ligue o oscilas e pressione o botão RUN/STOP que fica no canto direito superior olhando para o aparelho;

**(6.6)** Tente congelar o sinal no display mexendo lentamente no botão TRIGGER, que também fica à direita olhando para o aparelho;

**(6.7)** Você também pode ajusar melhor o sinal para o centro da tela mexendo no botão < POSITION>, e também, pode esticar o sinal girando no botão SEC/DIV para a direita. Volte no item **(7.6)** para recongelar o sinal;

**(6.8)** O sinal está igual a este abaixo?

<img src="https://github.com/agodoi/m09cc-semana04/blob/main/assets/fig5.jpeg" width="500">

**(6.8)** Se a taxa baud rate é de 9.600bps, qual é o tempo de duração de cada bit?

**(6.8)** **DESAFIO:** Uma sequência de 10 bits: BIT START + 1 BYTE + BIT STOP tem qual duração? Consegue comprovar isso na tela do oscila? Vale um chocolate se mandar no slack uma foto do seu oscilas no slack e uma explicação objetiva e clara. Pode usar post it ou recursos do osciloscópio para comprovar o tempo em segundos (ou milisegundos) desse "quadro de 10 bits".

# Kahoot - Pergunta 9

# Kahoot - Pergunta 10

# FIM
