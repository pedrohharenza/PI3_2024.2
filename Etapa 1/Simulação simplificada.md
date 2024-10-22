# Simulação Simplificada da Estação de Recarga
Esta parte do projeto tem como objetivo descrever o funcionamento de uma simulação que representa os principais aspectos operacionais da estação de recarga. A simulação visa demonstrar como a estação se comunica com os veículos elétricos.

Como detalhado na seção [Definição dos parâmetros de funcionamento](Etapa%201/Definição%20dos%20parâmetros%20de%20funcionamento.md) a comunicação entre a estação de recarga e o veículo é realizada por meio do sinal Control Pilot. Este sinal é baseado em uma modulação por largura de pulso (PWM) de 1 kHz, na qual a amplitude máxima indica o estado da estação, enquanto a razão cíclica transmite a corrente máxima que a estação pode fornecer ao veículo.

## Simulação

O desenvolvimento do projeto será realizado com a utilização de um microcontrolador, que será encarregado de gerar o sinal PWM e processar os diferentes estados da estação de recarga. Com objetivo de simplificar a simulação será apenas considerado o sinla PWM que seria gerado pelo mircocontroladro. Também será considerado as resistências que controlam os estados de carregamento para simular o comportamento do carro elétrico do ponto de vista do sinal CP.
