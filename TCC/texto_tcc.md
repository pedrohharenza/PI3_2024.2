## Comunicação por Largura de Pulso (PWM) no Funcionamento da Estação de Recarga
A comunicação por largura de pulso (PWM, do inglês Pulse Width Modulation) desempenha um papel importante na interação entre a estação de recarga e o veículo elétrico (VE). Sua principal função é transmitir, a informação de corrente máxima que o VE pode consumir durante o processo de carregamento. Essa comunicação é realizada por meio de um sinal de onda quadrada, em que a largura do pulso é modulada enquanto a frequência permanece constante. A largura do pulso é convertida em informações sobre a capacidade de corrente disponível para o carregamento do veículo. Essa relação entre a largura do pulso e a corrente pode ser expressa pela equação: X:

$$
I=60*D
$$

onde I representa a corrente máxima em ampères (A) e D é a razão cíclica do sinal PWM, expressa em porcentagem.

O sistema de alimentação da estação de recarga gera um sinal PWM com uma frequência de 1 kHz, e a amplitude do sinal varia entre ±12 V. Essa modulação permite que a estação de recarga e o VE se comuniquem, garantindo que o carregamento ocorra dentro dos limites seguros de corrente.

A razão cíclica do sinal PWM pode ser ajustada dinamicamente pelo sistema de recarga para se adaptar a diferentes condições operacionais, como gestão de carga ou limitações de potência da rede elétrica. Esse ajuste em tempo real permite que a estação de recarga informe ao veículo a corrente disponível em cada momento, otimizando o processo de carregamento e evitando sobrecargas.

O veículo elétrico responde ao sinal PWM aplicando uma carga resistiva ao sinal Control Pilot, que é o responsável pela comunicação com a estação de recarga. Essa carga resistiva gera uma queda de tensão que determina os estados da estação de recarga, conforme detalhado na Tabela 1. Cada estado corresponde a uma condição específica do processo de carregamento, como explicado anteriormente. 

| Estado | Descrição                                          | Control Pilot (V)       | Faixa de Tolerância (V) |
|--------|----------------------------------------------------|-------------------------|-------------------------|
| A      | Sem Conexão                                        | +12 V                   | 11,4 a 12,6 V           |
| B1     | Conexão Estabelecida (sem PWM)                     | +9 V                    | 8,37 a 9,59 V           |
| B2     | Conexão Estabelecida (com PWM)                     | +9 V (PWM ativo)        | 8,37 a 9,59 V           |
| C1     | Alimentação Disponível (sem PWM)                   | +6 V                    | 5,47 a 6,53 V           |
| C2     | Alimentação Disponível (com PWM)                   | +6 V (PWM ativo)        | 5,47 a 6,53 V           |
| D1     | Alimentação com Requisitos de Ventilação (sem PWM) | +3 V                    | 2,59 a 3,28 V           |
| D2     | Alimentação com Requisitos de Ventilação (com PWM) | +3 V (PWM ativo)        | 2,59 a 3,28 V           |
| E      | Sem Alimentação Disponível                         | 0 V                     | Não especificado        |
| F      | Falha no Sistema                                   | -12 V                   | Não especificado        |


O veículo elétrico também monitora a frequência do sinal PWM, que deve estar dentro da faixa de 1 kHz ± 5%. Caso o sinal esteja fora dessa faixa, o veículo não deve iniciar o processo de recarga, garantindo que a comunicação entre os dispositivos ocorra dentro dos parâmetros seguros e estabelecidos pela norma.

A estação de recarga monitora a parte inferior do sinal PWM, que deve atingir -12 V quando não estiver conectada ao veículo. Esse controle é essencial para verificar a presença de um diodo no circuito, que é responsável por garantir a integridade do sinal. Quando o diodo está presente, a parte inferior do sinal PWM deve apresentar 0 V, indicando que o circuito está funcionando corretamente e que a alimentação pode ser acionada com segurança.

O circuito que exemplificar a conexão do sinal Control Pilot da estação de recarga e um VE pode ser ilustrado pela figura x.

<p align="center">
    <img src="Imagens/Circuito%20Control%20Pilot.jpg">
</p>

## Proteções

A norma estabelece diversas exigências relacionadas às proteções, com destaque para a preocupação com as fugas de corrente em corrente alternada (CA) e corrente contínua (CC). Em relação à proteção contra correntes diferenciais, é fundamental que os pontos de conexão sejam protegidos por Dispositivos de Proteção à Corrente Diferencial Residual (DDR) com uma corrente residual de funcionamento não superior a 30 mA. Os DDRs devem ser do tipo A ou superior e atender às normas IEC 61008-1, IEC 61009-1, ABNT NBR IEC 60947-2 e ABNT NBR IEC 62423.

Adicionalmente, em instalações que utilizam DDRs do tipo AC, o sistema de alimentação para veículos elétricos (VE) deve incluir um meio de proteção contra corrente de falta com desempenho igual ou superior ao de um DDR tipo A. Também deve ser implementado um dispositivo que desconecte a alimentação caso a corrente de falta em corrente contínua (CC) ultrapasse 6 mA. A norma ainda exige que, em caso de falhas, todos os condutores ativos sejam desconectados e que sejam adotadas medidas de proteção adequadas para correntes de falta em corrente contínua.

## Conectores

As estações de recarga de veículos elétricos (EVs) utilizam diferentes tipos de conectores para garantir a conexão entre o veículo e o ponto de carga. O tipo de conector escolhido depende das especificações do veículo, da região e do padrão adotado pelas operadoras de rede de recarga. O mais utilizado no Brasil e na Europa é o conector Tipo 2, que se destaca pela sua versatilidade e ampla compatibilidade com diversos modelos de veículos elétricos. Esse conector possui uma configuração de 7 pinos, sendo três para a transmissão de corrente elétrica, dois para a comunicação entre o veículo e a estação, e dois para a aterragem do sistema como ilustra a Figura X.

Um dos pinos de comunicação é responsável pelo sinal Control Pilot discutido anteriormente, o Outro pino é responsável pelo sinal Proximity Pilot (PP). Esse sinal permite à estação de recarga identificar quando o cabo está corretamente conectado ao veículo. Ele também fornece informações sobre a corrente que o cabo é capaz de suportar, além de ajudar a controlar a corrente elétrica fornecida ao veículo de acordo com a capacidade do cabo e a temperatura, evitando sobrecarga ou aquecimento excessivo. Essa informação é dada por uma resistência, normalmente encontrada dentro do plug, entre o pino PP e PE, o valor dessa resistência indica qual a capcidade máxima aceita pelo plug. A relação entre os diferentes valores de resistências e a máxima corrente que pode circular no cabo está representada na Tabela X.

| Resistência do PP (Ω) | Corrente Máxima Suportada Pelo Cabo (A) |
|-----------------------|---------------------|
| 1500 Ω              |   10 A     |
| 680 Ω               |   20 A     |
| 220 Ω               |   32 A     |
| 100 Ω               |   63 A     |

Além do Tipo 2, existem outros conectores, como o Tipo 1, amplamente usado em veículos elétricos fabricados na América do Norte e em algumas regiões da Ásia. O Tipo 1 é baseado em uma configuração de 5 pinos e transmite uma corrente de até 32A em corrente alternada (AC). Outro padrão importante é o conector Combo 2, que combina o Tipo 2 com dois pinos adicionais para suportar a recarga em corrente contínua (DC), permitindo a recarga rápida, ideal para estações de recarga de alta potência.

O design e a construção desses conectores seguem rigorosos padrões de segurança, pois são responsáveis por transportar grandes quantidades de energia elétrica. Eles devem ser robustos, resistentes a intempéries e capazes de garantir uma conexão segura e estável durante o processo de recarga. Além disso, cada conector é projetado para se comunicar com o veículo, fornecendo informações sobre o status da carga e garantindo a proteção contra sobrecargas ou falhas elétricas. Em muitas estações de recarga, o conector é acoplado à tomada por um mecanismo de trava, o que impede a desconexão acidental durante o processo de carga.

https://www.ytelect.com/blog/what-are-even-and-odd-order-harmonics_b240#:~:text=Even%20and%20odd%20order%20harmonics%20are%20key%20factors%20in%20power,problems%20in%20the%20electrical%20system.

# Harmônicas Pares e Ímpares em Sistemas Elétricos
Em sistemas elétricos, as harmônicas são componentes de frequência que são múltiplos inteiros da frequência fundamental. Elas surgem devido a distorções não lineares em equipamentos e cargas, tais como retificadores, inversores e fontes chaveadas. As harmônicas são classificadas em pares (2ª, 4ª, 6ª, etc.) e ímpares (3ª, 5ª, 7ª, etc.), e sua presença pode causar diversos problemas, como distorção de tensão, sobrecarga em condutores e interferência em sistemas de comunicação. No entanto, as harmônicas ímpares são geralmente mais relevantes e estudadas do que as harmônicas pares, devido às características de simetria dos sinais em sistemas elétricos.

De acordo com Lathi (2007), em "Sinais e Sistemas Lineares", a análise de Fourier permite decompor um sinal periódico em uma soma de senoides com frequências múltiplas da fundamental. Para sinais com simetria de meia onda, ou seja, quando o sinal satisfaz a condição $f(t)=-f(t+ T/2)$ , onde  $T$ é o período, apenas as harmônicas ímpares estão presentes na série de Fourier. Essa simetria é comum em sistemas elétricos bem projetados, nos quais as cargas não lineares distorcem a forma de onda da corrente ou tensão, mas mantêm a simetria entre os semiciclos positivo e negativo. Como resultado, as harmônicas ímpares dominam o espectro de distorção.

Por outro lado, as harmônicas pares aparecem quando há assimetria na forma de onda, ou seja, quando os semiciclos positivo e negativo não são espelhados. Essa condição é menos comum em sistemas elétricos equilibrados, pois a maioria das distorções não lineares preserva a simetria de meia onda. No entanto, é comum que a segunda harmônica se torne significativa em casos onde há distorções assimétricas entre os semiciclos positivo e negativo. Por exemplo, em sistemas com retificadores de meia onda ou em transformadores operando próximo à saturação magnética, a forma de onda pode perder sua simetria, gerando harmônicas pares. Conforme destacado por Lathi, a presença de harmônicas pares pode indicar problemas como desbalanceamento de cargas, falhas em equipamentos ou a presença de componentes de corrente contínua (DC) no sinal. Em sistemas trifásicos, por exemplo, as harmônicas pares tendem a se cancelar quando as cargas estão equilibradas, o que reforça sua menor relevância em comparação com as harmônicas ímpares.

Além disso, as harmônicas ímpares têm um impacto mais significativo em sistemas de potência. A 3ª harmônica e seus múltiplos (9ª, 15ª, etc.), conhecidas como harmônicas triplas, são particularmente problemáticas em sistemas trifásicos, pois se somam no condutor neutro, podendo causar sobrecarga e superaquecimento. Já as harmônicas de ordem superior (5ª, 7ª, etc.) podem levar a problemas de ressonância em circuitos com capacitores de correção de fator de potência, além de aumentar as perdas por efeito Joule e histerese magnética.

Em resumo, as harmônicas ímpares são mais estudadas e consideradas em sistemas elétricos devido à sua predominância em sinais com simetria de meia onda, que é característica de distorções não lineares típicas. Já as harmônicas pares, embora menos frequentes, podem servir como indicadores de problemas como desbalanceamento ou falhas em equipamentos. A segunda harmônica, em particular, ganha relevância em casos de assimetria entre os semiciclos positivo e negativo, como em retificadores de meia onda ou transformadores operando em condições de saturação. A análise desses fenômenos é essencial para o projeto e operação de sistemas elétricos eficientes e confiáveis, e pode ser aprofundada com base em referências como "Sinais e Sistemas Lineares" de B.P. Lathi, que fornece uma base teórica sólida para o estudo de sinais e suas propriedades no domínio da frequência.

NBR17019 DE 04/2022 - Instalações elétricas de baixa tensão - Requisitos para instalações em locais especiais - Alimentação de veículos elétricos

https://www.chip37.com/PDF/STM32F373VCH6%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C.pdf




# Desenvolvimento do Hardware

O desenvolvimento do hardware para a estação de recarga de veículos elétricos nível 1 de 16A foi dividido em duas partes principais: a primeira voltada para o funcionamento da estação de recarga, seguindo o protocolo de comunicação abordado em capítulos anteriores, e a segunda dedicada à aquisição de medidas de tensão elétrica e corrente elétrica para o cálculo do consumo de energia. Ambas as partes foram projetadas para atender aos requisitos de precisão, com erro de medição inferior a 1%.

A primeira parte do sistema é responsável pelo controle da estação de recarga, que é realizado por meio da implementação de uma máquina de estados no microcontrolador STM32F0. Este microcontrolador foi escolhido por ser uma solução simples, de baixo custo e com ampla disponibilidade no mercado, além de atender plenamente às necessidades da aplicação. A comunicação entre os microcontroladores STM32F0 e STM32F373 foi projetada para utilizar UART (Universal Asynchronous Receiver-Transmitter), garantindo uma troca de dados eficiente e confiável.

A segunda parte do sistema é dedicada à aquisição de medidas de tensão elétrica e corrente elétrica, essenciais para o cálculo preciso do consumo de energia. Para essa finalidade, foi utilizado o microcontrolador STM32F373, que possui características avançadas voltadas para instrumentação, como um módulo de ponto flutuante e um conversor analógico-digital (ADC) do tipo Sigma-Delta. Esses recursos permitem medições de alta precisão, atendendo ao requisito de erro total inferior a 1%. O sensor de corrente elétrica utilizado foi um resistor shunt, que oferece alta precisão e baixo custo, enquanto a tensão elétrica da rede foi medida por meio de um divisor resistivo. Diferente da primeira parte, este circuito não é isolado da rede elétrica, o que exigiu cuidados adicionais no projeto para garantir a confiabilidade do sistema.

A alimentação do sistema foi projetada para garantir estabilidade e eficiência. Para atender ao funcionamento da estação de recarga, foram utilizados dois módulos de fonte chaveada de 12V, conectados de forma a produzir um sinal de +12V e outro de -12V. Para a parte isolada do circuito, foi empregado um módulo de fonte chaveada não isolada de 5V, seguido por um estágio de redução de tensão para 5V utilizando um conversor buck e outro estágio de redução para 3.3V utilizando um regulador linear. A alimentação do STM32F0 é feita pela tensão de 3.3V. Na parte não isolada, também existe um estágio de redução de tensão para 3.3V para alimentar o STM32F373. Além disso, reguladores de tensão foram incorporados para garantir que os componentes operem dentro de suas faixas nominais, mesmo em condições de variação da rede elétrica.

Para proteção do sistema, foram utilizados um fusível e um varistor, que garantem a segurança contra sobrecorrentes e surtos de tensão elétrica. Esses componentes foram estrategicamente posicionados para proteger tanto a parte isolada quanto a não isolada do circuito, garantindo a integridade do sistema como um todo.

A seleção dos componentes para ambas as partes do sistema foi realizada com base em critérios técnicos e econômicos, priorizando a precisão, a confiabilidade e a conformidade com normas técnicas. Sensores com erro inferior a 0,5% foram escolhidos para garantir que o erro total da medição fique abaixo de 1%. O STM32F373, com seu ADC Sigma-Delta e módulo de ponto flutuante, foi essencial para alcançar a precisão necessária nas medições de energia.

Após a montagem dos circuitos, foram realizados testes para validar o funcionamento do sistema. A calibração dos sensores foi essencial para ajustar os parâmetros de medição e garantir a precisão das leituras. O erro do sistema foi verificado por meio da comparação com um padrão de referência, como um multímetro de precisão. Testes de carga simulada também foram conduzidos para avaliar a robustez do sistema em diferentes cenários de recarga.

Além dos aspectos técnicos, foram consideradas questões como proteção contra falhas, eficiência energética e conformidade com normas técnicas. Mecanismos de desligamento automático em caso de sobrecarga ou curto-circuito foram implementados para aumentar a segurança do sistema. A minimização de perdas nos circuitos foi priorizada para melhorar a eficiência global da estação de recarga. Por fim, o projeto foi desenvolvido em conformidade com normas técnicas, como a ABNT NBR IEC 61851, que estabelece requisitos para sistemas de recarga de veículos elétricos.
