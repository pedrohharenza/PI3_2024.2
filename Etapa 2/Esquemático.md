# Esquemático

O esquemático do projeto será dividio nos seguintes circuitos

- Control Pilot
- Microcontroldor
- Proteções
- Acionamento dos relés
- LEDs
- Alimentação

# Control Pilot

Como já foi discutido antes na [Definição dos parâmetros de funcionamento](Definição%20dos%20parâmetros%20de%20funcionamento.md) o circuito do Control Pilot tem como objetivo gerar o sinal de comunicação com o veículo, podendo ser PWM ±12V 1kHz ou +12V sem PWM. Para isso foi desenhado um circuito semelhante ao apresentado na simulação, utilizando comprardor. Para que seja possível obter as saídas de +12V e -12V foi considerado o comparador [TLV1805](https://www.ti.com/lit/ds/symlink/tlv1805-q1.pdf?ts=1729874561037&ref_url=https%253A%252F%252Fbr.mouser.com%252F) que possui saída Rail-to-Rail, isso significa que as tensões de saída podem ser muito próximas da tensão de alimentação, já que a alimentção do comparador é ±12V


O comparador faz a comparação do PWM gerado pelo STM32 de +3V3 a 0V com 3V3/2 tendo na sáida o sinal PWM de ±12V que comunica com o carro.

# Microcontrolador

O circuto do microcontrolador é simples. Precisa apenas das alimentações, capacitores de desacoplamento para reduzir ruido, cristal oscilador e as conexões com os demais circuitos

# Proteções

O circuito de proteção apresenta um fusível e um varistor para conter surtos de tensão ou curto-circuito. Se um surto de alta tensão ocorrer (por exemplo, um pico causado por um raio), o varistor age para limitar a tensão excessiva, evitando que ela chegue aos componentes sensíveis. Se houver um aumento excessivo de corrente, o fusível será acionado, interrompendo o fluxo de corrente e protegendo o circuito de danos.

# Acionamento dos relés

Os relés selecionados para a construção da estação de recarga são acionados por uma tensão de 12V. Para isso, é necessário um driver de acionamento que recebe o sinal de controle do microcontrolador e, a partir da fonte de alimentação de 12V, aciona os relés.

# LEDSs

A interface homem máquina selecionada para estação de recarga será LEDs RGB do tipo WS2812 sendo possível determinar cores diferentes para indicar cada estado.
