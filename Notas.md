## Lista de Possíveis componentes

Objetivo: Erro < 1% comparado ao PA-1000

| Componente             | PART NUMBER                                   |
|------------------------|-----------------------------------------------|
| **MCU**                | [STM32F37](https://br.mouser.com/datasheet/2/389/stm32f373cc-1851083.pdf)|
| **Sensor de corrente** | Shunt de alta precisão ou transformador de corrente|
| **Sensor de Tensão**   | [Divisor resistivo de alta precisão](https://br.mouser.com/datasheet/2/385/sei_css_cssh-3077671.pdf) |
| **Comparador PWM**     | [TLV1805](https://www.ti.com/lit/ds/symlink/tlv1805-q1.pdf?ts=1729874561037&ref_url=https%253A%252F%252Fbr.mouser.com%252F) |
| **Fonte**              | [HLK-PM12](https://nettigo.eu/attachments/503) | 


## Documentação sobre medida de corrente com shunt 
- https://br.mouser.com/applications/making-sense-current-sensing/
- https://www.escomponents.com/precision-current-sensing-guide4

## Three-Phase Power Meter Reference Design
- https://www.nxp.com/design/design-center/development-boards-and-designs/three-phase-power-meter-reference-design:THREE-PHASE-POWER-METER

## Single-Phase Electric Meter With Isolated Energy
- https://www.tij.co.jp/jp/lit/ug/tidu455a/tidu455a.pdf

## Dica do Renan
- Sigma delta é diferencial. Para medir tensão fase neutro meu microcontrolador precisa estar com a ref no neutro
- Opto na saída pwm antes do ampop para isolar o sinal
- Pesquisar sobre como fazer as contas no software sem fazer fft
- 
