![image](https://github.com/user-attachments/assets/5dd95791-a625-4650-b805-e6e7bcac9ebb)# Simulação Simplificada da Estação de Recarga
Esta parte do projeto tem como objetivo descrever o funcionamento de uma simulação que representa os principais aspectos operacionais da estação de recarga. A simulação visa demonstrar como a estação se comunica com os veículos elétricos.

Como detalhado na seção [Definição dos parâmetros de funcionamento](Definição%20dos%20parâmetros%20de%20funcionamento.md) a comunicação entre a estação de recarga e o veículo é realizada por meio do sinal Control Pilot. Este sinal é baseado em uma modulação por largura de pulso (PWM) de 1 kHz, na qual a amplitude máxima indica o estado da estação, enquanto a razão cíclica transmite a corrente máxima que a estação pode fornecer ao veículo.

## Simulação

O desenvolvimento do projeto será realizado com a utilização de um microcontrolador, que será encarregado de gerar o sinal PWM e processar os diferentes estados da estação de recarga. Com objetivo de simplificar a simulação será apenas considerado o sinla PWM gerado pelo mircocontroladro. Também será considerado as resistências que controlam os estados de carregamento para simular o comportamento do carro elétrico do ponto de vista do sinal CP.

Como visto na [Definição dos parâmetros de funcionamento](Definição%20dos%20parâmetros%20de%20funcionamento.md) o sinal Control Pilot (CP) opera em 12V DC ou como um PWM variando entre +12V e -12V, com sua amplitude ajustada conforme as resistências controladas pelo veículo elétrico. Para gerar esse sinal, é necessário um amplificador operacional com alimentação simétrica de +12V e -12V. O sinal PWM gerado pelo microcontrolador varia entre +3.3V e 0V. O amplificador operacional compara esse PWM com um nível de referência de +1.65V, resultando no sinal desejado na saída. Assim, quando o sinal PWM é 3.3V, a saída do comparador fornece +12V, e quando o sinal PWM é 0V, a saída do comparador se ajusta para -12V.

<p align="center">
    <img src="Imagens/simulação%20pwm.png">
</p>

O microcontrolador deve ser capaz de medir a amplitude do sinal PWM do CP para determinal qual é o estado da estação de recarga. Para isso é necessário reduzir o sinal para que esteja dentro do limite que o microcontrolador aceite, de 0V a 3.3V. para isso é utilizado a alimentação de +3.3V e alguns resistores para elevar o sinal e diminuir sua amplitude. Para que a medição do sinal CP não seja alterado, é utilizado um amplificador operacional como buffer de isolamento da medida. Com isso, o microcontrolador consegue determinar os estados da estação de recarga com base na amplitude do sinal PWM.

<p align="center">
    <img src="Imagens/leitura%20do%20sinal%20cp.png">
</p>
