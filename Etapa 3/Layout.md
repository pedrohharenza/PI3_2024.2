# Seleção de Componentes

Os componentes selecionados para o desenvolvimento do projeto foram definidos levando em consideração, principalmente, a disponibilidade e os requisitos técnicos do projeto. Componentes **SMD** (Surface Mount Device) foram preferidos em relação aos componentes **PTH** (Pin Through Hole) para facilitar a fabricação e reduzir o número de furos na placa. A maioria dos resistores e capacitores foi selecionada no encapsulamento **0805**, que é amplamente disponível. Nesta etapa do projeto, foram especificados apenas os componentes mais críticos.

## Fonte de Alimentação

Para a alimentação de **+12V** e **-12V**, foram selecionadas duas fontes **AC/DC**: uma de **10W** para o **+12V** (**HLK-10M12**) e outra de **3W** para o **-12V** (**HLK-PM12**), já que o consumo de corrente para o **-12V** é baixo.

Para alimentar os demais circuitos, foram utilizados dois estágios de **step-down**. O primeiro utiliza um regulador linear **LM7805** (5V), que será utilizado para alimentar os **LEDs WS2812**. Esse regulador suporta até **1A**, mas será limitado a **833mA** pela fonte de **12V**. Cada LED WS2812, com o brilho máximo, consome **60mA**, o que permite alimentar até **13 LEDs** com brilho total. No entanto, devido à **resistência térmica** do LM7805 de **62,5°C/W**, e considerando a diferença de tensão de entrada (**12V**) e saída (**5V**) de **7V**, o uso de 13 LEDs sem dissipação de calor não é viável. Por esse motivo, será utilizado apenas **5 LEDs WS2812**. 

Para a alimentação de **3,3V**, será utilizado um regulador linear **AMS1117-3.3**. Conversores **DC/DC**, como o **buck**, que são mais eficientes que reguladores lineares, não foram considerados devido ao **chaveamento de alta frequência**, que pode gerar **ruídos excessivos**.

## Ampop

Para o circuito **Control Pilot**, foi selecionado o **TLV1805**, um comparador que aceita alimentação simétrica de **±12V**. Ele possui uma saída **push-pull**, com um **voltage swing máximo** de **300mV** e um **slew rate** de aproximadamente **40V/μs**. Para a aplicação, é necessária uma saída de **±12V** com uma variação máxima de **600mV** e tempo de subida de **-12V até 12V** de no máximo **13μs**.

Para o sinal de **1,65V**, foi utilizado um amplificador operacional (ampop) de uso geral, o **LMV321**, configurado como **buffer**. Essa configuração proporciona uma **baixa impedância de saída**, garantindo que o sinal não seja alterado pela carga conectada.

## Microcontrolador

O microcontrolador selecionado foi o **STM32F030K6T6**, que é de baixo custo, fácil de encontrar e atende aos requisitos técnicos do projeto.

## Conectores de Entrada e Saída

Os conectores de entrada e saída selecionados foram o modelo **691219610002** da **Wurth Elektronik**, que suportam **300VAC** a **57A** e atendem adequadamente aos requisitos do projeto.

## Relés

Os relés selecionados foram o **HF161F** da **Hongfa**, que suportam até **20A** em **250VAC** e possuem corrente de acionamento de **75mA**.



# Desenho do Layout
