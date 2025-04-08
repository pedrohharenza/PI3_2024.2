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




# Desenvolvimento do Firmware


O desenvolvimento do firmware foi estruturado de forma modular, seguindo a lógica apresentada no diagrama de blocos, o que facilitou a organização e a manutenção do código. A programação foi realizada em linguagem C, utilizando o ambiente de desenvolvimento integrado STM32CubeIDE, que oferece ferramentas para configuração e depuração dos microcontroladores da família STM32. Assim como no desenvolvimento do hardware, a programação foi dividida em duas partes principais, sendo a primeira dedicada para o funcionamento da estação de recarga e a segunda dedicada na aquisição de medidas e cálculo do consumo de energia, ambas as partes foram programadas sem o uso de sistema operacional de tempo real.

## Desenvolvimento do Firmware Dedicado a Estação de Recarga

A primeira etapa do desenvolvimento do firmware foi focada no funcionamento da estação de recarga, seguindo o protocolo de comunicação discutido anteriormente. Para isso, foi implementada uma máquina de estados para gerenciar os diferentes estados do processo de carregamento. Com o objetivo de simplificar a implementação, os estados D e E foram suprimidos sem comprometer o funcionamento da estação. O estado D foi incorporado ao estado C, pois ambos compartilham o mesmo comportamento, diferenciando-se apenas por informar a necessidade de ventilação durante o carregamento. Da mesma forma, o estado E foi tratado como F, uma vez que ambos resultam na interrupção do carregamento. A lógica de transição entre os estados pode ser visualizada na Figura 24.


Figura 24 - Diagrama de estados

Fonte:  Elaboração própria (2025).

O sistema inicia com o comportamento do estado A. para que ocorra alteração no estado de carregamento é preciso que a tensão elétrica no sinal Control Pilot se altere, isso ocorrerá quando o VE solicitar alteração no estados de carregamento ou ocorrer uma intervenção do usuário, como a remoção da conexão entre estação de recarga e o VE. Para identificar a alteração de estado também foi necessário a configuração adequada do ADC para interpretar o sinal de comunicação com o VE e consequentemente definir o estado de funcionamento da estação de recarga.
Para o controle do sinal de comunicação, foi necessário configurar o periférico para gerar o sinal PWM com razão cíclica de aproximadamente 26,7%, garantindo que a estação de recarga transmita a informação de corrente elétrica máxima que o VE pode consumir de 16 A, como estabelecido pelos requisitos do projeto.
Para o controle do sinal de comunicação, foi necessário configurar um periférico para gerar um sinal PWM, permitindo que a estação de recarga realize o controle adequado do sinal Control Pilot de acordo com cada estado de carregamento e a informação de corrente máxima que pode ser consumida.

O acionamento dos relés foi realizado por um pino de propósito geral (GPIO) do STM32F0, responsável por controlar tanto o relé de comutação da fase quanto o relé de comutação do neutro.
A interface com o usuário foi implementada utilizando LEDs RGB WS2812, que fornecem feedback visual sobre o estado de carregamento. O controle das cores é realizado por meio de pulsos PWM, permitindo a transmissão das informações necessárias. A comunicação é feita pelo envio de 24 bits para cada led, sendo dividido em 8 bits para cor verde, 8 bits para a cor vermelha e 8 bits para o azul. Os bits são transmitidos a cada 1,25 microssegundos, o que corresponde a uma frequência de 800 KHz. Para enviar o bit 1, o sinal de comunicação deve permanecer em nível alto por aproximadamente dois terços do período representado por T1H, e em nível baixo pelo restante do período, representado por T1L. Já para enviar o bit 0, o sinal deve permanecer em nível alto por cerca de um terço do período, representado por T0H, e em nível baixo por dois terços do período, representado por T0L. Após o envio dos dados é preciso manter o sinal em baixo por 50 microsegundos, representado por Treset, para indicar a finalização da comunicação. Para realizar essa comunicação, utilizou-se o acesso direto à memória (DMA) para transferir as diferentes larguras de pulso para o temporizador, que, gera um sinal PWM com os dados definidos. A Figura 25 ilustra a forma de onda do sinal de comunicação para o envio da informação de cores para os leds WS2812.
Figura 25 - Diagrama de estados

Fonte:  WORLDSEMI (2025).
Para a comunicação entre os dois microcontroladores, foi configurada a interface serial UART. Para garantir a integridade dos dados transmitidos, foi implementado um protocolo baseado em confirmação, onde cada mensagem recebida é validada antes de prosseguir com a execução do sistema. O STM32F373 envia uma confirmação positiva (ACK) ou negativa (NACK) após cada instrução recebida do STM32F0. A execução da instrução ocorre somente quando o STM32F0 recebe a confirmação adequada, assegurando a confiabilidade da comunicação. Caso contrário, cinco tentativas são feitas e se mesmo assim não existir a confirmação positiva o sistema interrompe o funcionamento determinando estado F.

## Desenvolvimento do Firmware Dedicado a Medida de Energia

Para o desenvolvimento do firmware dedicado à medida de energia no STM32F373, primeiramente foi configurado o ADC sigma-delta para aquisição das medidas de corrente e tensão elétrica em modo diferencial, utilizando DMA para enviar os dados para um buffer circular. O buffer circular é uma estrutura de dados utilizada para armazenar temporariamente informações em um ciclo contínuo, onde, ao atingir o final do espaço alocado, ele volta ao início, sobrescrevendo os dados mais antigos. As medições de corrente e tensão elétrica são realizadas simultaneamente, garantindo a sincronia entre as duas variáveis. Em medidores de energia, é fundamental amostrar a tensão e a corrente elétrica ao mesmo tempo, pois isso assegura que a medição da potência instantânea seja exata. A potência instantânea é dada pelo produto da tensão elétrica e da corrente elétrica. Se as duas grandezas forem amostradas em momentos diferentes, pode haver um descompasso entre elas, resultando em cálculos incorretos da potência. A amostragem simultânea garante que a relação entre a tensão e a corrente seja capturada corretamente, permitindo um cálculo mais exato da potência consumida. 

A frequência de amostragem do ADC sigma-delta foi ajustada para garantir que as harmônicas até a décima quinta ordem fossem consideradas. Para isso, foi definida uma frequência mínima de amostragem de X kHz, assegurando que as componentes harmônicas relevantes fossem incluídas na análise e contribuindo para que a medida energia consumida atenda ao nível de erros estabelecido.

Em seguida, assim como no firmware da estação de recarga, foi configurado a interface serial UART, seguindo o mesmo protocólo baseado em confirmação. As instruções que pode ser enviadas para o STM32F373 são:

a) Iniciar medida
b) Finalizar medida

Quando a instrução para iniciar a medição de energia é recebida e o ACK é retornado, o STM32F373 começa o processamento das amostras de tensão e corrente com o objetivo de calcular o valor da energia consumida. O cálculo é realizado em grupos de amostras adquiridas ao longo de um período de 833 µs para otimizar o desempenho de processamento. Para minimizar a influência de ruídos nas medições, é aplicado um filtro de média móvel sobre as amostras, garantindo a qualidade dos dados. Após o processamento, o valor da energia consumida é calculado. Quando o sistema recebe a instrução para finalizar a medição, esse processo é interrompido e o valor da energia consumida durante a recarga é enviado via comunicação UART. Para possibilitar o monitoramento contínuo do consumo de energia durante a recarga, foi configurado para que o valor de consumo seja transmitido via UART a cada 1 segundo, em vez de apenas ser enviado o valor final.




## Desenvolvimento do Firmware Dedicado à Medida de Energia

O desenvolvimento do firmware dedicado à medida de energia no STM32F373 foi realizado com foco em atender ao requisito de precisão, garantindo um erro inferior a 1%. O microcontrolador foi configurado para utilizar o ADC sigma-delta, um conversor analógico-digital de 16 bits, que permite a aquisição de medidas de corrente e tensão elétrica em modo diferencial. O uso de ADC sigma-delta em medidores de energia é comum devido à sua alta resolução, capacidade de rejeição a ruídos e precisão em medições de sinais de baixa amplitude, como os provenientes de sensores de corrente e tensão elétrica utilizados, garantindo cálculos confiáveis de potência e energia.

O ADC sigma-delta foi configurado para operar em conjunto com acesso diereto a memória (DMA), que permite o envio contínuo das amostras de corrente e tensão para um buffer circular. Esse buffer é uma estrutura de dados que armazena temporariamente as informações em um ciclo contínuo, sobrescrevendo os dados mais antigos ao atingir o final do espaço alocado. Essa abordagem garante que as medições sejam realizadas de forma contínua e sem perda de dados, mesmo em cenários de alta taxa de amostragem.

### Aquisição de Dados com ADC Sigma-Delta e DMA

A aquisição das medidas de corrente e tensão elétrica é feita de forma simultânea, um requisito fundamental para o cálculo da potência instantânea. A potência instantânea é obtida pelo produto da tensão e da corrente elétrica no mesmo instante de tempo. Se as duas grandezas fossem amostradas em momentos diferentes, poderia ocorrer um descompasso entre elas, resultando em erros significativos no cálculo da potência. A amostragem simultânea garante que a relação entre tensão e corrente seja capturada corretamente, assegurando a exatidão dos cálculos de energia.

### Frequência de Amostragem e Harmônicas

A frequência de amostragem do ADC sigma-delta foi cuidadosamente ajustada para garantir que as harmônicas até a décima quinta ordem fossem consideradas. Para capturar essas distorções, foi definida uma frequência mínima de amostragem de X kHz, que permite a inclusão das componentes harmônicas relevantes na análise. Essa configuração contribui para que a medida da energia consumida atenda ao nível de erro estabelecido.

### Interface Serial UART e Protocolo de Comunicação

Assim como no firmware da estação de recarga, também foi configurada a interface serial UART para comunicação com o STM32F0 utilizando o protocolo baseado em confirmação (ACK/NACK), onde cada comando enviado ao microcontrolador é validado antes da execução. As principais instruções que podem ser recebidas são:

- Iniciar Medida: Quando recebida, o STM32F373 inicia o processamento das amostras de tensão e corrente elétrica para calcular a energia consumida.

- Finalizar Medida: Interrompe o processo de medição e envia o valor final da energia consumida via UART.

### Processamento das Amostras e Cálculo de Energia

Após o recebimento da instrução para iniciar a medição, o STM32F373 começa a processar as amostras de tensão e corrente em grupos de amostras adquiridas ao longo de 833 µs. Esse intervalo foi escolhido para otimizar o desempenho de processamento, garantindo que o sistema opere de forma eficiente sem sobrecarregar o microcontrolador, sem comprometer a confiabilidade dos dados calculados.

Para minimizar a influência de ruídos nas medições, foi implementado um filtro de média móvel sobre as amostras. Esse filtro suaviza as variações abruptas nos dados, garantindo a qualidade e a confiabilidade das medições. O cálculo da energia consumida é realizado com base nas amostras filtradas, assegurando que os valores finais sejam precisos e consistentes. O mesmo filtro é aplicado às amostras de tensão e corrente elétrica, garantindo que o atraso introduzido seja idêntico para ambas as grandezas e, consequentemente, preservando o sincronismo das medições.

### Monitoramento Contínuo do Consumo de Energia

Além de calcular o valor final da energia consumida, o sistema foi configurado para permitir o monitoramento contínuo durante a recarga. A cada 1 segundo, o valor atual do consumo de energia é transmitido via UART, proporcionando um acompanhamento em tempo real do processo de recarga.




O circuito equivalente que pode exemplificar o comportamento do sinal de
comunicação quando conectado a um VE pode ser representado pela Figura 8:


### Estação de Recarga Com Medidor de Energia da Empresa Pionix

Além da análise de medidores de energia, também foi estudado o projeto aberto de uma estação de recarga trifásica de veículos elétricos desenvolvida pela Pionix, que inclui a capacidade de medir o consumo de energia de forma confiável. A Figura 13 ilustra o modelo 3D da estação de recarga analisada.

A solução apresentada pela Pionix, diferente dos medidores de energia analisados anteriormente, utiliza o ADE7978ACPZ-RL, um circuito integrado da fabricante Analog Devices, dedicado à medição de energia. Este componente foi projetado para medir com precisão parâmetros de tensão elétrica, corrente elétrica, potência ativa e reativa, fator de potência e frequência. As aquisições das medidas são feitas pelo ADC externo ADE7932ARIZ que possui isolamento galvânico na sua aquisição. A comunicação entre a estação de recarga e o ADE7978ACPZ-RL é realizada por meio de uma interface SPI.

A principal vantagem de usar um circuito integrado dedicado à medição de energia é a simplicidade na implementação. Com isso, não é necessário o desenvolvimento do firmware para a aquisição de amostras e processamento do sinal. Além disso, essa solução oferece isolamento galvânico, proporcionando maior segurança ao manuseio do equipamento e proteção contra variações de alta tensão na rede elétrica. Em contrapartida o ADE7978ACPZ-RL apresenta um custo elevado, podendo tornar o seu uso inviável. A Figura 14 ilustra um diagrama de blocos de como a solução é implementada na estação de recarga.


