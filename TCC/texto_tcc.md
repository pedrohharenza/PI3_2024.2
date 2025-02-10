# Exatidão e Precisão nas Medições de Consumo de Energia
No contexto do desenvolvimento de uma estação de recarga com capacidade de medir o consumo de energia, é essencial compreender os conceitos de exatidão e precisão, que são fundamentais para garantir a confiabilidade das medições do consumo de energia. Embora esses termos sejam frequentemente usados de forma intercambiável, eles se referem a aspectos distintos da qualidade das medições.

## Exatidão
A exatidão de uma medição refere-se à proximidade entre o valor medido e o valor verdadeiro ou referência. Em outras palavras, uma medição é considerada exata quando o valor obtido pelo instrumento de medição está muito próximo ao valor real do consumo de energia, que pode ser determinado por um padrão de referência ou calculado com base em modelos precisos. No caso de uma estação de recarga, a exatidão é crítica, pois ela assegura que os dados fornecidos ao usuário, como o consumo de energia durante o processo de recarga, sejam representativos e confiáveis.

Por exemplo, se uma estação de recarga indicar que 10 kWh foram consumidos durante uma recarga, mas o valor real medido por um sistema de referência for 9,8 kWh, a exatidão do medidor da estação de recarga pode ser questionada, pois ele apresenta uma discrepância de 0,2 kWh em relação ao valor real.

## Precisão
Por outro lado, a precisão refere-se à capacidade de um instrumento de medição de fornecer resultados consistentes ao realizar medições repetidas sob as mesmas condições. Em termos práticos, um instrumento preciso sempre fornecerá os mesmos resultados quando medindo a mesma quantidade, mesmo que esses resultados não sejam exatos. A precisão é importante para garantir que as leituras do consumo de energia não variem significativamente entre medições sucessivas, o que poderia levar a interpretações errôneas dos dados.

No contexto de uma estação de recarga, se a medição de consumo de energia for repetida várias vezes e sempre resultar em valores semelhantes, mas não necessariamente no valor exato, o sistema será considerado preciso, mas não necessariamente exato. No entanto, um sistema altamente preciso pode ser ajustado ou calibrado para melhorar sua exatidão.

Relação entre Exatidão e Precisão
Idealmente, as medições devem ser tanto exatas quanto precisas. Um sistema que seja exato, mas não preciso, indicará corretamente o valor médio do consumo de energia, mas poderá apresentar flutuações em medições repetidas, dificultando a interpretação dos dados. Por outro lado, um sistema preciso, mas não exato, poderá fornecer medições consistentes, mas distorcidas em relação ao valor real, o que afetaria a confiabilidade dos dados.

No caso da estação de recarga de nível 1 AC, é essencial que os instrumentos de medição utilizados para monitorar o consumo de energia apresentem tanto exatidão quanto precisão para garantir que os usuários recebam informações corretas e consistentes sobre o consumo de energia durante o processo de recarga. Isso melhora a transparência para os usuários, e assegura que o usuário estará sendo cobrado pelo que realmente foi consumido.

# Funcionamento de uma estação de recarga

O funcionamento de uma estação de recarga para veículos elétricos (VEs) é regido por um conjunto de estados definidos pela norma ABNT NBR IEC 61851-1. Esses estados representam diferentes condições no processo de recarga. Cada estado indica uma etapa distinta na comunicação e no fornecimento de energia entre a estação de recarga e o veículo elétrico.

A norma descreve os estados com as letras A, B, C, D, E e F, com subdivisões que indicam variações ou condições específicas. A lógica de transição entre cada estádo depende do sinal de comunicação entre a estação de recarga e o carro. Esse sinal é chamado de Control Pilot. A seguir, detalha-se cada um desses estados e suas implicações para o funcionamento da estação de recarga.

Estado A: Sem Conexão
No Estado A, não há conexão entre o veículo elétrico e a estação de recarga. Nesse estado, o Control Pilot da estação de recarga está operando com 12V, indicando que o sistema está inativo e aguardando a conexão do cabo de recarga. Deve-se considerar que este é o estado inicial, onde ainda não houve qualquer interação entre a estação e o veículo.

Estado B: Conexão Estabelecida
O Estado B é alcançado quando o cabo de recarga é conectado entre o veículo e a estação de recarga. Esse estado é subdividido em duas condições principais:

B1: Neste subestado, o sinal Control Pilot está em 9V e não há comunicação ativa. Deve-se entender que isso indica que a estação está aguardando a sinalização do veículo para poder iniciar a carga.

B2: Quando o sinal Control Pilot ainda está em 9V, mas com a modulação por largura de pulso (PWM) ativa, deve-se considerar que a estação de recarga está pronta para fornecer energia, e o processo de carregamento pode começar assim que o veículo autorizar.

Estado C: Alimentação Disponível
O Estado C indica que a alimentação elétrica está disponível, ou seja, a estação de recarga pode fornecer energia ao veículo elétrico. O circuito piloto está operando a 6V, sinalizando que a recarga pode ser iniciada. Esse estado também é subdividido em duas variações:

C1: O circuito piloto está em 6V. Deve-se compreender que isso significa que as condições de segurança do carregamento estão sendo atendidas e o VE está pronto para receber energia sem nenhuma necessidade extra.

C2: O circuito piloto está em 6V com a modulação por largura de pulso (PWM) ativa, o que indica que a estação está ativa e pronta para iniciar a carga de forma dinâmica, regulando a entrega de energia conforme a necessidade do veículo.

Estado D: Alimentação Disponível com Requisitos de Ventilação
O Estado D é similar ao Estado C, mas com a diferença de que o veículo exige ventilação adicional no processo de recarga devido ao calor gerado durante o carregamento. O circuito piloto estará operando a 3V, indicando que o sistema está em uma condição de recarga que exige controle térmico adequado. Esse estado também possui variações:

D1: O circuito piloto está em 3V e a ventilação é necessária para evitar o superaquecimento durante a recarga.

D2: O circuito piloto está em 3V com a modulação por largura de pulso (PWM) ativa, assim como no estado C2, a alimentação está pronta, com a modulação para controlar o fornecimento de energia.

Estado E: Sem Alimentação Disponível
O Estado E indica que não há alimentação disponível para o veículo. Nesse estado, sinal Control Pilot está a 0V, sinalizando uma falha no fornecimento de energia ou uma condição de emergência. Deve-se observar que esse estado é ativado quando o sistema de alimentação para o VE não pode fornecer energia e pode indicar uma situação de falta de energia, onde o dispositivo de acionamento do sistema precisa abrir para garantir a segurança.

Estado F: Falha no Sistema
O Estado F representa uma falha no sistema de alimentação da estação de recarga. O circuito piloto estará operando a -12V, sinalizando que há um problema crítico no sistema que requer manutenção. Quando o sistema entra nesse estado, deve-se destravar a tomada do veículo em até 30 segundos, garantindo a segurança do usuário e evitando danos maiores ao sistema de recarga. O Estado F é um estado de erro que exige a intervenção de manutenção para resolver o problema.

Transições Entre os Estados
As transições entre os estados A, B, C, D e E depender da amplitude positiva do sinal Control Pilot

## Comunicação por Largura de Pulso (PWM) no Funcionamento da Estação de Recarga
A comunicação por largura de pulso (PWM, do inglês Pulse Width Modulation) desempenha um papel importante na interação entre a estação de recarga e o veículo elétrico (VE). Sua principal função é transmitir, a informação de corrente máxima que o VE pode consumir durante o processo de carregamento. Essa comunicação é realizada por meio de um sinal de onda quadrada, em que a largura do pulso é modulada enquanto a frequência permanece constante. A largura do pulso é convertida em informações sobre a capacidade de corrente disponível para o carregamento do veículo. Essa relação entre a largura do pulso e a corrente pode ser expressa pela equação: X:

$$
I=60*D
$$

onde I representa a corrente máxima em ampères (A) e D é a razão cíclica do sinal PWM, expressa em porcentagem.

O sistema de alimentação da estação de recarga gera um sinal PWM com uma frequência de 1 kHz, e a amplitude do sinal varia entre ±12 V. Essa modulação permite que a estação de recarga e o VE se comuniquem, garantindo que o carregamento ocorra dentro dos limites seguros de corrente.

A razão cíclica do sinal PWM pode ser ajustada dinamicamente pelo sistema de recarga para se adaptar a diferentes condições operacionais, como gestão de carga ou limitações de potência da rede elétrica. Esse ajuste em tempo real permite que a estação de recarga informe ao veículo a corrente disponível em cada momento, otimizando o processo de carregamento e evitando sobrecargas.

O veículo elétrico responde ao sinal PWM aplicando uma carga resistiva ao sinal Control Pilot, que é o responsável pela comunicação com a estação de recarga. Essa carga resistiva gera uma queda de tensão que determina os estados da estação de recarga, conforme detalhado na Tabela 1. Cada estado corresponde a uma condição específica do processo de carregamento, como a conexão do veículo, a disponibilidade de alimentação e a necessidade de ventilação, entre outros. 

| Estado | Descrição                                      | Tensão no Control Pilot |
|--------|------------------------------------------------|-------------------------|
| A      | Sem Conexão                                     | +12 V                   |
| B1     | Conexão Estabelecida (sem PWM)                 | +9 V                    |
| B2     | Conexão Estabelecida (com PWM)                 | +9 V (PWM ativo)        |
| C1     | Alimentação Disponível (sem PWM)               | +6 V                    |
| C2     | Alimentação Disponível (com PWM)               | +6 V (PWM ativo)        |
| D1     | Alimentação com Requisitos de Ventilação (sem PWM) | +3 V                    |
| D2     | Alimentação com Requisitos de Ventilação (com PWM) | +3 V (PWM ativo)        |
| E      | Sem Alimentação Disponível                      | 0 V                     |
| F      | Falha no Sistema                                | -12 V                   |

O veículo elétrico também monitora a frequência do sinal PWM, que deve estar dentro da faixa de 1 kHz ± 5%. Caso o sinal esteja fora dessa faixa, o veículo não deve iniciar o processo de recarga, garantindo que a comunicação entre os dispositivos ocorra dentro dos parâmetros seguros e estabelecidos pela norma.

A estação de recarga monitora a parte inferior do sinal PWM, que deve atingir -12 V quando não estiver conectada ao veículo. Esse controle é essencial para verificar a presença de um diodo no circuito, que é responsável por garantir a integridade do sinal. Quando o diodo está presente, a parte inferior do sinal PWM deve apresentar 0 V, indicando que o circuito está funcionando corretamente e que a alimentação pode ser acionada com segurança.


