## Lista de Possíveis componentes

Objetivo: Classe 1 Erro < 1%

| Componente             | PART NUMBER                                   |
|------------------------|-----------------------------------------------|
| **MCU**                | [STM32F373x](https://br.mouser.com/datasheet/2/389/stm32f373cc-1851083.pdf)|
| **MCU Parte isolada**  | [STM32F030K6T6](https://www.acheicomponentes.com.br/circuitos-integrados/circuito-integrado-stm32f030k6t6-lqfp-32-smd)|
| **Optoacoplador isolamento da UART**      | [6N137](https://br.mouser.com/datasheet/2/427/6n137-7681.pdf) [Documentação](https://electronics.stackexchange.com/questions/672452/serial-isolation-with-6n137-opto-coupler?rq=1)|
| **Sensor de corrente** | [Shunt]([https://www.eletrodex.net/passivos/resistores/especiais/resistor-de-medicao-shunt](https://br.mouser.com/ProductDetail/Vishay-Dale/WSLF2512L5000FEA?qs=aVyJF2WnouT0Jqstwf%2Fe3A%3D%3D)) de alta precisão ou transformador de corrente|
| **Sensor de Tensão**   | [Divisor resistivo de alta precisão](https://br.mouser.com/datasheet/2/385/sei_css_cssh-3077671.pdf) |
| **Comparador PWM**     | [TLV1805](https://www.ti.com/lit/ds/symlink/tlv1805-q1.pdf?ts=1729874561037&ref_url=https%253A%252F%252Fbr.mouser.com%252F); [LM2903](https://www.acheicomponentes.com.br/circuitos-integrados/smd/soic-8/circuito-integrado-lm2903dr-smd-soic-8-lm2903); [LMC7211AIM5](https://www.acheicomponentes.com.br/circuitos-integrados/smd/ci-amplificador-lmc7211aim5nopb-smd-sot-23-5) |
| **Fonte**              | [HLK-PM12](https://nettigo.eu/attachments/503) | 

<p align="center">
    <img src="Diagrama%20de%20blocos%20Monofásico%20simples.png" alt="Conector Tipo 2">
</p>

<p align="center">
    <img src="Diagrama%20de%20blocos%20Triásico%20completo.png" alt="Conector Tipo 2">
</p>


## Documentação sobre medida de corrente com shunt 
- https://br.mouser.com/applications/making-sense-current-sensing/
- https://www.escomponents.com/precision-current-sensing-guide4

## NXP Single-Phase Power Metering Reference Design
- https://www.nxp.com/design/design-center/development-boards-and-designs/single-phase-metering:SINGLE-PHASE-METER
  
## NXP Three-Phase Power Meter Reference Design
- https://www.nxp.com/design/design-center/development-boards-and-designs/three-phase-power-meter-reference-design:THREE-PHASE-POWER-METER

## Filter-Based Algorithm for Metering Applications
- https://www.nxp.com/docs/en/application-note/AN4265.pdf

## TI Single-Phase Electric Meter With Isolated Energy
- https://www.tij.co.jp/jp/lit/ug/tidu455a/tidu455a.pdf

## Isolação debug probe
- https://www.st.com/en/development-tools/st-link-v2.html

## Dicas do Renan
- Sigma delta é diferencial. Para medir tensão fase neutro o microcontrolador precisa estar com a ref no neutro
- NÃO CONECTAR O NOTEBOOK NO GRAVADOR QUANDO ESTIVER CONECTADO NA REDE, RISCO DE BOOM!
- Opto no pwm antes do ampop comparador do sinal CP para isolar o sinal
- Pesquisar sobre como fazer as contas sem fazer fft
- Se usar shunt considerar low side sensing para manter a mesma ref
- Pesquisar transformador que poderia resolver o problema da ref no neutro e manter as características de harmônicas
- pesquisar tranformador de corrente com erro baixo que poderia ser utilizado
- Perguntar pro Joabel sobre a fonte de alimentação do microcontrolador, se uma solução seria isolar com transformador, para ficar neutro como ref dos +12V e dps abaixar pra +3.3V com regulador linear. Teria que utilizar 3 fontes de 12V?
- Pra atingir o erro de 1% tem que calibrar para os componentes utilizados em software

## Salvar os dados
- Usar python para ler a porta serial e salvar os dados em um arquivo txt.

## Solução para o isolamento
- Utilizar o STM32F373 apenas para medida de energia e comunicar via UART isolado por opto para um STM32F030K6T6, que possui a máquina de estados do carregador


# Calibração de Software vs. Tensão de Referência Precisa para o ADC (NotebookLM + Datasheet STM32F373)
Na sua aplicação, onde você precisa de medidas precisas e acuradas do ADC, tanto a precisão da tensão de referência quanto a calibração do ADC por software são importantes.
## Tensão de Referência:
- A tensão de referência determina a escala de conversão do ADC. Uma tensão de referência mais precisa resulta em medições mais precisas.
- VREFINT: O STM32F373xx possui uma tensão de referência interna (VREFINT) com uma tensão típica de 1,23 V e uma dispersão de ±10 mV em relação à temperatura. Isso significa que a VREFINT pode variar dentro dessa faixa, afetando a precisão das medições do ADC.
- Referência Externa: Se a sua aplicação requer precisão maior do que a fornecida pela VREFINT, você pode usar uma referência externa de alta precisão. [VREF+ no datasheet]
- Impacto da Dispersão: Conforme discutido anteriormente, a dispersão da VREFINT refere-se à variação da sua tensão. Essa variação impacta diretamente a precisão das medições do ADC.
## Calibração de Software:
- A calibração do ADC por software pode compensar erros de offset e ganho, melhorando a precisão das medições.
- Calibração Interna: O STM32F373xx possui uma função de calibração interna que pode ser executada após a inicialização.
- Calibração Personalizada: Você também pode implementar sua própria rotina de calibração, medindo uma tensão conhecida e ajustando o software para corrigir os erros.
## Recomendações:
- Para a maioria das aplicações: A calibração do ADC por software, em conjunto com a VREFINT, pode ser suficiente para obter medidas precisas e acuradas.
- Para alta precisão: Se a sua aplicação exigir a maior precisão possível, utilize uma tensão de referência externa de alta precisão e faça a calibração do ADC por software.
## Considerações Adicionais:
- Impedância da Fonte do Sinal: A impedância da fonte do sinal conectado ao ADC deve ser baixa para garantir a precisão da conversão.
- Ruído: Minimize o ruído no circuito de medição, utilizando técnicas adequadas de layout e filtragem.
- Temperatura: A temperatura pode afetar a precisão do ADC e da tensão de referência. Utilize um sensor de temperatura para compensar as variações de temperatura ou opere o sistema em uma faixa de temperatura controlada.
- Datasheet: Consulte o datasheet completo do STM32F373xx para obter informações detalhadas sobre as características do ADC e da VREFINT.
## Em resumo:
A calibração do ADC por software pode melhorar a precisão das medições, mas uma tensão de referência precisa é fundamental para obter a melhor precisão possível. A escolha entre VREFINT e uma referência externa depende dos requisitos de precisão da sua aplicação.
