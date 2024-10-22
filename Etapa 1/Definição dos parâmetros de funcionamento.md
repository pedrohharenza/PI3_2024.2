# Definição dos Parâmetros de Funcionamento da Estação de Recarga
Esta seção do projeto tem como objetivo descrever os parâmetros e o funcionamento de uma estação de recarga de veículos elétricos de forma detalhada, facilitando o entendimento do desenvolvimento do porjeto. A definição adequada desses parâmetros é essencial para garantir que o projeto atenda às especificações técnicas e funcionais necessárias para operar de maneira eficiente e segura.

## Clacificação de Estações de Recargas
As estações de recarga são classificadas em Nível 1, Nível 2 e Nível 3. As estações AC convencionais mais comuns são as de Nível 1 e Nível 2, que se diferenciam pela potência de operação. As estações de recarga Nível 1 operam com até 16A (geralmente 12A em residências) e têm uma potência de até 1,9 kW (120V x 16A) ou 3,5 kW (220V x 16A). Por outro lado, as estações de recarga Nível 2 podem chegar a 80A, sendo que os carregadores comuns costumam ser de 16A ou 32A, e podem fornecer uma potência de até 19,2 kW (240V x 80A) ou mais, dependendo do modelo. As estações de recarga Nível 3, também conhecidas como estações de carregamento rápido, são as únicas que podem ser consideradas "carregadores de veículos elétricos", uma vez que convertem a energia diretamente na estação. Diferentemente das estações de Nível 1 e Nível 2, as estações de Nível 3 operam com corrente contínua (DC), geralmente acima de 100A, podendo chegar a 500A ou mais, com tensões que variam de 400V a 800V, dependendo do sistema de carregamento, e têm potências que podem variar de 50 kW a mais de 350 kW. 

| Nível      | Corrente (A) | Tensão (V) | Potência (kW) | Tempo de Carregamento | Equipamento                         |
|------------|---------------|------------|----------------|-----------------------|-------------------------------------|
| Nível 1    | Até 16A      | 120V/220V  | 1.9kW (120V) / 3.5kW (220V) | 8 a 20 horas         | Tomada padrão                       |
| Nível 2    | Até 80A      | 240V       | Até 19.2kW    | 4 a 8 horas           | Ponto de carga dedicado             |
| Nível 3    | >100A        | 400V-800V  | 50 a 350kW    | <30 minutos           | Estações de carregamento público    |

Os carregadores de Nível 1 e Nível 2 devem passar pelo On-board Charger, que está instalado dentro do veículo, antes de transferirem efetivamente a energia para a bateria do carro. O On-board Charger (carregador a bordo) é um componente essencial em veículos elétricos que gerencia o processo de carregamento da bateria. Quando um veículo é conectado a uma estação de carregamento de Nível 1 ou Nível 2, a corrente elétrica da rede elétrica passa primeiro pelo On-board Charger, que converte a corrente alternada (AC) em corrente contínua (DC), adequada para a bateria do veículo. Esse processo inclui a regulação da tensão e da corrente, garantindo que a bateria seja carregada de forma segura e eficiente. Assim, o On-board Charger atua como um intermediário entre a fonte de energia externa e a bateria do carro, permitindo a transferência de energia necessária para o carregamento.

## Conector
Existem diversos tipos de padrões de conectores para estações de veículos elétricos; no entanto, o conector mais utilizado no Brasil e na Europa é conhecido como Tipo 2, que será o utilizado para o desenvolvimento do projeto. Este conector é amplamente adotado devido à sua versatilidade e compatibilidade com a maioria dos veículos elétricos disponíveis no mercado.

<p align="center">
    <img src="Imagens/Conector%20tipo%202.png" alt="Conector Tipo 2">
</p>

| Pino | Nome             | Função                                                   |
|------|------------------|----------------------------------------------------------|
| 1    | L1   | Fase 1 da alimentação AC (220V)                          |
| 2    | L2   | Fase 2 da alimentação AC (220V) apenas para trifásico    |
| 3    | L3   | Fase 3 da alimentação AC (220V) apenas para trifásico    |
| 4    | N    | Neutro da alimentação AC                                 |
| 5    | PE   | Protective Earth - Terra                                 |
| 6    | CP   | Control Pilot - Utilizado para comunicação entre o veículo e a estação de carregamento |
| 7    | PP   | Proximity Pilot - Detector de presnça e identificação do limite de corrente do cabo conectado ao carro         |


## Protocolo de Comunicação - Control Pilot
A comunicação entre a estação de recarga e o veículo é realizada por meio do Control Pilot (CP). O sinal do CP determina os estados da estação de recarga, podendo ser um sinal estático ou um sinal PWM de 1 kHz. A razão cíclica desse sinal PWM comunica ao veículo a corrente máxima que a estação de recarga pode fornecer.

| Estado  CP          | Descrição                                                                                  |
|---------------------|--------------------------------------------------------------------------------------------|
| +12V DC                 | A estação está pronta para iniciar o processo de carregamento (IDLE).                     |
| +9V DC                  | Estação de recarga está conectada preparando para o carregamento.                         |
| PWM 1kHz +9V a -12V     | A estação de recarga está pronta e aguardando a conexão do veículo para iniciar o processo de carregamento."   |
| PWM 1kHz +6V a -12V     | Veículo em estado de carregamento.                                                        |
| 0V ou -12V DC           | Erro                                                                                      |



