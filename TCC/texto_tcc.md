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
As transições entre os estados A, B, C, D e E geralmente são causadas por ações do veículo elétrico ou do usuário, como conectar ou desconectar o cabo de recarga, iniciar ou interromper a carga, ou atender a uma solicitação de ventilação.

Por outro lado, as transições entre os subestados x1 e x2 (como B1 para B2, ou C1 para C2) são determinadas pelo sistema de alimentação para o VE, que gerencia a disponibilidade de energia e a comunicação com o veículo. Deve-se considerar que a transição para o Estado F ou para o Estado E pode ocorrer automaticamente em caso de falhas ou quando há uma condição de falta de energia, exigindo uma resposta imediata para garantir a segurança do sistema.


## Comunicação por Largura de Pulso (PWM) no Funcionamento da Estação de Recarga
A comunicação por largura de pulso (PWM) desempenha um papel fundamental na interação entre a estação de recarga e o veículo elétrico (VE). A principal função da modulação por largura de pulso é transmitir a corrente máxima que o VE pode consumir com segurança. Isso é realizado por meio de um sinal de onda quadrada, no qual a largura do pulso (tempo em que o sinal está em nível alto) é modulada, enquanto a frequência permanece constante. A variação da largura do pulso é convertida em informações sobre a capacidade de corrente disponível para o carregamento do veículo. A relação entre a largura de pulso e a corrente que pode ser consumida pode ser dada por:

$$
I=60*D
$$

Geração e Função do Sinal PWM
Geração do Sinal PWM: O sistema de alimentação da estação de recarga gera um sinal PWM com uma frequência fixa de 1 kHz, sendo a tensão do sinal variando entre ±12 V.

Função Principal: O principal objetivo do sinal PWM é informar ao veículo elétrico a corrente máxima que ele pode consumir com segurança durante o processo de recarga. Isso é feito ajustando a razão cíclica do sinal, ou seja, a proporção entre o tempo em que o sinal está em nível alto e o período total do sinal. Por exemplo, uma razão cíclica de 10% corresponde a 6A de corrente, enquanto uma razão cíclica de 85% corresponde a 51A de corrente (85% x 0.6 = 51).

Modificação da Razão Cíclica
O sistema de recarga pode modificar dinamicamente a razão cíclica do sinal PWM para se adaptar a condições de gestão de carga ou limitações de potência. Assim, a razão cíclica pode ser ajustada em tempo real, indicando ao veículo a corrente disponível naquele momento específico.
Resposta do Veículo Elétrico
O veículo elétrico responde ao sinal PWM aplicando uma carga resistiva à meia onda positiva do circuito-piloto de comando, que é responsável pela comunicação com a estação de recarga.

O VE também monitora a frequência do sinal PWM, que deve estar dentro da faixa de 1 ± 5% kHz. Caso o sinal esteja fora dessa faixa, o veículo não deve iniciar a recarga.

Estados e Comunicação PWM
Os estados B2, C2 e D2 fazem uso da comunicação PWM para informar ao VE a corrente máxima disponível:

Estado B2: Neste estado, a estação de recarga está pronta para fornecer energia, e o sinal PWM indica a corrente máxima disponível com base na razão cíclica.

Estado C2: Aqui, o sistema de alimentação também está pronto para fornecer energia, utilizando a modulação PWM para sinalizar a corrente máxima disponível.

Estado D2: Similar ao C2, mas no estado D2, a ventilação é necessária para garantir a segurança durante o carregamento. O sinal PWM ainda informa a corrente máxima, com a diferença de que a ventilação deve ser considerada.

Comunicação Digital vs. PWM
Embora a comunicação PWM seja utilizada nos Modos 2 e 3, o Modo 4 de recarga requer a comunicação digital adicional (LIN-CP). Em sistemas de recarga que implementam tanto PWM-CP quanto LIN-CP, o protocolo PWM é utilizado inicialmente. Se o veículo responder com sinais LIN válidos, a comunicação pode mudar para LIN-CP. Caso o veículo não responda com sinais LIN, a estação de recarga continuará utilizando a comunicação PWM.

Tabelas de Referência e Relação entre Razão Cíclica e Corrente Máxima
As tabelas A.7 e A.8 da norma fornecem uma referência para a razão cíclica do PWM e a corrente máxima permitida:

Uma razão cíclica de 0% indica que o sistema de alimentação para o VE não está disponível (estado F).

Uma razão cíclica de 100% significa que não há corrente disponível (estado x1).

Uma razão cíclica de 5% indica que a comunicação digital é necessária antes de ativar a alimentação.

Além disso, se a razão cíclica estiver entre 8% e 97%, com comunicação digital estabelecida, a corrente máxima não pode exceder o valor indicado nem pelo PWM nem pela comunicação digital.

Sinal de -12V e Segurança
O sistema de alimentação também monitora a parte inferior do sinal PWM, que deve atingir -12V. Esse controle serve para verificar a presença de diodo antes de permitir o fechamento do dispositivo de manobra de alimentação, garantindo que o sistema de recarga funcione de forma segura.




