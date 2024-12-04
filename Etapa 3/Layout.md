# Seleção de Componentes

Os componentes selecionados para o desenvolvimento do projeto foram definidos levando em consideração, principalmente, a disponibilidade e os requisitos técnicos do projeto. Componentes **SMD** (Surface Mount Device) foram preferidos em relação aos componentes **PTH** (Pin Through Hole) para facilitar a fabricação e reduzir o número de furos na placa. A maioria dos resistores e capacitores foi selecionada no encapsulamento **0805**, que é amplamente disponível. Nesta etapa do projeto, foram especificados apenas os componentes mais críticos.

## Fonte de Alimentação

Para a alimentação de **+12V** e **-12V**, foram selecionadas duas fontes **AC/DC**: uma de **10W** para o **+12V** [HLK-10M12](https://evelta.com/content/datasheets/098-HLK-10MX.pdf) e outra de **3W** para o **-12V** [HLK-PM12](https://nettigo.eu/attachments/503), já que o consumo de corrente para o **-12V** é baixo.

Para alimentar os demais circuitos, foram utilizados dois estágios de **step-down**. O primeiro utiliza um regulador linear [LM7805](https://www.alldatasheet.com/datasheet-pdf/view/82833/fairchild/lm7805.html) (5V), que será utilizado para alimentar os LEDs [WS2812](https://cdn-shop.adafruit.com/datasheets/WS2812.pdf). Esse regulador suporta até **1A**, mas será limitado a **833mA** pela fonte de **12V**. Cada LED WS2812, com o brilho máximo, consome **60mA**, o que permite alimentar até **13 LEDs** com brilho total. No entanto, devido à **resistência térmica** do LM7805 de **62,5°C/W**, e considerando a diferença de tensão de entrada (**12V**) e saída (**5V**) de **7V**, o uso de 13 LEDs sem dissipação de calor não é viável. Por esse motivo, será utilizado apenas **5 LEDs WS2812**. 

Para a alimentação de **3,3V**, será utilizado um regulador linear [AMS1117-3.3](http://www.advanced-monolithic.com/pdf/ds1117.pdf). Conversores **DC/DC**, como o **buck**, que são mais eficientes que reguladores lineares, não foram considerados devido ao **chaveamento de alta frequência**, que pode gerar **ruídos excessivos**.

## Ampop

Para o circuito **Control Pilot**, foi selecionado o [TLV1805](https://www.ti.com/lit/ds/symlink/tlv1805-q1.pdf?ts=1729874561037&ref_url=https%253A%252F%252Fbr.mouser.com%252F), um comparador que aceita alimentação simétrica de **±12V**. Ele possui uma saída **push-pull**, com um **voltage swing máximo** de **300mV** e um **slew rate** de aproximadamente **40V/μs**. Para a aplicação, é necessária uma saída de **±12V** com uma variação máxima de **600mV** e tempo de subida de **-12V até 12V** de no máximo **13μs**.

Para o sinal de **1,65V**, foi utilizado um amplificador operacional (ampop) de uso geral, o [LMV321](https://www.onsemi.com/pdf/datasheet/lmv321-d.pdf)

## Microcontrolador

O microcontrolador selecionado foi o [STM32F030K6T6](https://br.mouser.com/datasheet/2/389/stm32f030f4-1851168.pdf), que é de baixo custo, fácil de encontrar e atende aos requisitos técnicos do projeto.

## Conectores de Entrada e Saída

Os conectores de entrada e saída selecionados foram o modelo [691219610002](https://br.mouser.com/ProductDetail/Wurth-Elektronik/691219610002?qs=sPbYRqrBIVneFMqRi9IErQ%3D%3D) da **Wurth Elektronik**, que suportam **300VAC** a **57A** e atendem adequadamente aos requisitos do projeto.

## Relés

Os relés selecionados foram o [HF161F](https://source.hongfa.com//pdf/web/viewer.html?file=/Uploads/Product/PDF/HF161F_en.pdf?timestamp=1733333696) da Hongfa, com capacidade para suportar até 20A em 250VAC e corrente de acionamento de 75mA, atendendo assim a todos os requisitos necessários para a aplicação.



# Desenho do Layout

O desenho do layout foi pensado de forma a tornar o processo de fabricação o mais fácil possível e ao mesmo tempo garantir o funcionamento da estação de recarga. Para isso foi considerado uma placa dupla face com a maior parte das trilhas de 0.3mm ou maior, com o menor espaçamento de 0.3mm. Para facilitar a montagem foi dado prioridade para componentes SMD e utilizado PTH apenas quando realmente necessário. O layout apresenta uma parte destinada a medidas de corrente e tensão que não será aprofundado, pois não é necessário para que estação de recarga funcione corretamente.

O layout foi separado na parte onde circula potências mais altas e a parte de baixa potência. Para parte onde circula a tensão de entrada 220VAC foi considerado um espaçamento entre tilhas de 3mm ou maior, seguindo a tabela da norma IPC-2221, para tensões 311V a 500V de pico, para trilhas externas em altitudes menores que 3050m é preciso espaçamento de pelo menos 2.5mm



