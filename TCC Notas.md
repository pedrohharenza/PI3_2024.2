## Lista de Possíveis componentes

Objetivo: Erro < 1% Classe A

| Componente             | PART NUMBER                                   |
|------------------------|-----------------------------------------------|
| **MCU**                | [STM32F373x](https://br.mouser.com/datasheet/2/389/stm32f373cc-1851083.pdf)|
| **MCU Parte isolada**  | [STM32F030K6T6](https://www.acheicomponentes.com.br/circuitos-integrados/circuito-integrado-stm32f030k6t6-lqfp-32-smd)
| **Sensor de corrente** | Shunt de alta precisão ou transformador de corrente|
| **Sensor de Tensão**   | [Divisor resistivo de alta precisão](https://br.mouser.com/datasheet/2/385/sei_css_cssh-3077671.pdf) |
| **Comparador PWM**     | [TLV1805](https://www.ti.com/lit/ds/symlink/tlv1805-q1.pdf?ts=1729874561037&ref_url=https%253A%252F%252Fbr.mouser.com%252F) |
| **Fonte**              | [HLK-PM12](https://nettigo.eu/attachments/503) | 


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
