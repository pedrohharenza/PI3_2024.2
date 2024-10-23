# Definição dos Parâmetros de Funcionamento da Estação de Recarga
Esta seção do projeto tem como objetivo descrever os parâmetros e o funcionamento de uma estação de recarga de veículos elétricos de forma detalhada, facilitando o entendimento do desenvolvimento do porjeto. A definição adequada desses parâmetros é essencial para garantir que o projeto atenda às especificações técnicas e funcionais necessárias para operar de maneira correta e segura.

## Clacificação de Estações de Recargas
As estações de recarga são classificadas em Nível 1, Nível 2 e Nível 3. As estações AC convencionais mais comuns são as de Nível 1 e Nível 2, que se diferenciam pela potência de operação. As estações de recarga Nível 1 operam com até 16A (geralmente 12A em residências) e têm uma potência de até 1,9 kW (120V x 16A) ou 3,5 kW (220V x 16A). Por outro lado, as estações de recarga Nível 2 podem chegar a 80A, sendo que os carregadores comuns costumam ser de 16A ou 32A, e podem fornecer uma potência de até 19,2 kW (240V x 80A) ou mais, dependendo do modelo. As estações de recarga Nível 3, também conhecidas como estações de carregamento rápido, são as únicas que podem ser consideradas "carregadores de veículos elétricos", uma vez que convertem a energia diretamente na estação. Diferentemente das estações de Nível 1 e Nível 2, as estações de Nível 3 operam com corrente contínua (DC), geralmente acima de 100A, podendo chegar a 500A ou mais, com tensões que variam de 400V a 800V, dependendo do sistema de carregamento, e têm potências que podem variar de 50 kW a mais de 350 kW. 

| Nível      | Corrente (A) | Tensão (V) | Potência (kW) | Tempo de Carregamento | Equipamento                         |
|------------|---------------|------------|----------------|-----------------------|-------------------------------------|
| Nível 1    | Até 16A      | 120V/220V  | 1.9kW (120V) / 3.5kW (220V) | 8 a 20 horas         | Tomada padrão                       |
| Nível 2    | Até 80A      | 240V       | Até 19.2kW    | 4 a 8 horas           | Ponto de carga dedicado             |
| Nível 3    | >100A        | 400V-800V  | 50 a 350kW    | <30 minutos           | Estações de carregamento público    |

Os carregadores de Nível 1 e Nível 2 devem passar pelo On-board Charger, que está instalado dentro do veículo, antes de transferirem efetivamente a energia para a bateria do carro. O On-board Charger (carregador a bordo) é um componente essencial em veículos elétricos que gerencia o processo de carregamento da bateria. Quando um veículo é conectado a uma estação de carregamento de Nível 1 ou Nível 2, a corrente elétrica da rede elétrica passa primeiro pelo On-board Charger, que converte a corrente alternada (AC) em corrente contínua (DC), adequada para a bateria do veículo. Esse processo inclui a regulação da tensão e da corrente, garantindo que a bateria seja carregada de forma segura e eficiente. Assim, o On-board Charger atua como um intermediário entre a fonte de energia externa e a bateria do carro, permitindo a transferência de energia necessária para o carregamento. Esse processo torna muito mais simples o funcionamento de estações de recarga AC Nível 1 e Nivel 2.

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

| Sinal  CP          | Estado | Descrição                                                                                  |
|---------------------|--------|--------------------------------------------------------------------------------------------|
| +12V DC             | A       | A estação está pronta para iniciar o processo de carregamento (IDLE).   |
| PWM 1kHz +9V a -12V | B       | Estação de recarga está conectada preparando para o carregamento.       |
| PWM 1kHz +6V a -12V | C       | Veículo em estado de carregamento.                                      |
| PWM 1kHz +3 a -12   | D       | Veículo em estado de carregamento, ventilação necessária (normalmente não utilizada) |
| 0V ou -12V DC       | E ou F  | Erro                                                                    |

Do ponto de vista do Control Pilot, o veículo elétrico pode ser simplificado a um conjunto de resistências, onde o carro controla quais resistências estão ativadas. Essa configuração permite ajustar a tensão no sinal do Control Pilot (CP) e consequentemente alterar os estados da estação de recarga.


<p align="center">
    <img src="Imagens/EVSE%20esquemático.png" alt="Conector Tipo 2">
</p>

Em relação ao consumo de corrente, a estação de recarga informa ao veículo qual é a corrente máxima que pode ser fornecida, utilizando a razão cíclica do sinal do Control Pilot (CP). Essa comunicação permite que o veículo ajuste sua demanda de carga de acordo com as capacidades da estação.

A relação entre a corrente máxima (I) fornecida pela estação de recarga e a razão cíclica (D) do sinal do Control Pilot (CP) pode ser expressa pela seguinte equação:

$$
I = 60 \times D
$$

É importante destacar que essa comunicação entre a estação de recarga e o veículo define um limite de corrente que o veículo não deve ultrapassar. Caso uma carga conectada solicite mais corrente do que o permitido, a estação de recarga pode fornecer uma corrente superior, mas isso pode resultar em riscos, como superaquecimento e outras falhas.

## Protocolo de comunicação - Proximity Pilot
O Proximity Pilot (PP) funciona como um sistema de detecção da conexão do cabo da estação de recarga ao veículo e também determina o limite de corrente que esse cabo suporta. A comunicação entre o PP e o veículo é realizada através de uma resistência que se estabelece entre o PP e o Protective Earth (PE), podendo variar de acordo com a corrente máxima que o cabo é capaz de conduzir. Normalmente, essa resistência está integrada diretamente no cabo de alimentação.

| Resistência do PP (Ω) | Corrente Máxima Suportada Pelo Cabo (A) |
|-----------------------|---------------------|
| 1500 Ohm              |   10 A     |
| 680 Ohm               |   20 A     |
| 220 Ohm               |   32 A     |
| 100 Ohm               |   63 A     |

Como o foco do projeto é desenvlvimento de uma estação de recarga portátil Nível 1, será utilizado um cabo como a resistência de 680 Ohm entre PP e PE.

## Sistemas de Proteções

### IDR Tipo B
O IDR tipo B é um dispositivo de proteção essencial em estações de recarga de veículos elétricos, projetado para detectar correntes de fuga em circuitos que operam tanto com corrente alternada quanto contínua. Ele monitora a diferença entre a corrente que entra e a que sai do circuito, desarmando automaticamente quando identifica uma discrepância significativa. Isso é crucial em ambientes de recarga, onde falhas de isolamento ou contato com água podem ocorrer. Ao interromper o fornecimento de eletricidade em caso de fuga, o IDR tipo B protege os usuários contra choques elétricos e previne danos aos equipamentos, garantindo um ambiente de recarga seguro e confiável. De acordo com as norma de segurança  elétrica NBR 16825, a instalação de IDR tipo B é obrigatória em estações de recarga de veículos elétricos. Essa proteção pode ser instalada diretamente na estação de recarga ou no quadro de distribuição de energia.

### Sensores de Corrente
Sensores de corrente em estações de recarga atuam como um sistema de proteção ao monitorar continuamente a corrente elétrica que flui para o veículo. Eles podem detectar anomalias, como correntes de fuga ou sobrecargas, e acionar medidas de proteção em tempo real. Quando um sensor identifica uma corrente que diverge do esperado, como uma sobrecarga, ele pode desativar automaticamente a estação de recarga, prevenindo danos ao veículo ou à infraestrutura.
 - Sensor de efeito Hall
 - Sensor de corrente transformador
 - Resistor Shunt

### Sensores de Tensão
Sensores de tensão podem ser utilizados como sistema de proteção em estações de recarga de veículos elétricos ao monitorar continuamente a tensão elétrica fornecida ao sistema. Eles detectam desvios dos níveis de tensão esperados, como sobrecargas ou quedas abruptas. Quando uma anomalia é identificada, o sensor pode acionar automaticamente um desligamento da estação de recarga, prevenindo danos ao veículo e à infraestrutura. Essa proteção é crucial, pois tensões inadequadas podem resultar em falhas elétricas, danos à bateria do veículo ou até riscos de incêndio.
 - Divisor resistivo (Tolerância dos resistores)
 - Transformadores (ZHTPT107)
 - Transdutores de tensão

### Proteção Contra Surto de Tensão
Em estações de recarga, a proteção de surto de tensão geralmente é realizada por dispositivos de proteção contra surtos (DPS). Esses dispositivos são projetados para proteger os equipamentos contra picos de tensão transitórios, como os causados por raios ou manobras na rede elétrica.
Quando um surto é detectado, o DPS desvia a energia excessiva para a terra ou a absorve, evitando que essa tensão alta chegue aos componentes sensíveis da estação de recarga e do veículo elétrico. Isso ajuda a prevenir danos que poderiam comprometer a operação dos sistemas. A instalação de DPS é essencial para garantir a segurança e a longevidade das estações de recarga, especialmente em áreas propensas a surtos elétricos




