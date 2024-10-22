# Definição dos Parâmetros de Funcionamento da Estação de Recarga
Esta seção do projeto tem como objetivo descrever os parâmetros e o funcionamento de uma estação de recarga de veículos elétricos de forma detalhada, facilitando o entendimento do desenvolvimento do porjeto. A definição adequada desses parâmetros é essencial para garantir que o projeto atenda às especificações técnicas e funcionais necessárias para operar de maneira eficiente e segura.

## Clacificação de Estações de Recargas
As estações de recargas são clacificadas por Nível 1, Nível 2 e Nível 3. As estações de recargas AC convencionais mais comuns são as de Nível 1 e Nível 2 que se diferenciam pela sua potência de funcionamento onde estções de recarga Nível 1 operam com até 16A (geralmente 12A em residências) e potência de até 1,9 kW (120V x 16A) ou 3,5 kW (220V x 16A). Já estações de recargas Nível 2 podem chegar até 80A (carregadores comuns costumam ser de 16A ou 32A) com potência de até 19,2 kW (240V x 80A) ou mais, dependendo do modelo. Estações de recarga Nível 3 são temabém conhecidas por estações de carregamento rápido, é a unica estação de recarga que pode ser considerada um "Carregador de veículos elétricos" visoto que é a unica que converte a energia diretamente na estação. Diferente das estações de Nível 1 e Nível 2 a estação Nível 3 opera com corrente DC geralmente acima de 100A, podendo chegar a 500A ou mais com 400V a 800V (dependendo do sistema de carregamento) podendo variar de 50 kW a mais de 350 kW.


| Nível      | Corrente (A) | Tensão (V) | Potência (kW) | Tempo de Carregamento | Equipamento                         |
|------------|---------------|------------|----------------|-----------------------|-------------------------------------|
| Nível 1    | Até 16A      | 120V/220V  | 1.9kW (120V) / 3.5kW (220V) | 8 a 20 horas         | Tomada padrão                       |
| Nível 2    | Até 80A      | 240V       | Até 19.2kW    | 4 a 8 horas           | Ponto de carga dedicado             |
| Nível 3    | >100A        | 400V-800V  | 50 a 350kW    | <30 minutos           | Estações de carregamento público    |
