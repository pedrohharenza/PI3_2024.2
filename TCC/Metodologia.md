# Metodologia

Este trabalho tem como objetivo desenvolver uma estação de recarga para veículos elétricos capaz de medir o consumo de energia com precisão e exatidão. Para isso, a metodologia adotada foi dividida em etapas que incluem a pesquisa bibliográfica sobre os princípios de funcionamento de medidores de energia, o aprofundamento nos temas relacionados ao funcionamento de estações de recarga, o desenvolvimento de hardware e software, a realização de testes práticos e a análise dos resultados. A pesquisa bibliográfica abrangeu o estudo de técnicas de medição de tensão, corrente e potência em circuitos CA além do impacto de harmônicas na precisão das medições. A abordagem utilizada é experimental, com foco na construção de um protótipo funcional e na validação de suas medições. A escolha da abordagem experimental justifica-se pela necessidade de validar na prática os conceitos teóricos estudados e desenvolver uma solução que atenda às exigências de precisão e exatidão. Com a execução desta metodologia, espera-se obter um protótipo funcional capaz de medir o consumo de energia com margens de erro inferiores a X%, além de validar sua precisão em comparação com resultados obtidos utilizando o analisador de potêancia PA1000 da Tektronix.

Desenvolvimento do Hardware

O desenvolvimento do hardware foi subdividido nas seguintes etapas:

a) Desenvolvimento do esquemático: A partir das soluções teóricas estudadas, foi elaborado o esquemático, que define a interligação dos componentes do sistema, incluindo os sensores de corrente e tensão, bem como o circuito de alimentação e proteção.

b) Seleção de componentes: Realizou-se a escolha dos componentes eletrônicos mais adequados para a aplicação, levando em consideração aspectos como a precisão das medições, a resistência a interferências, a compatibilidade com as demais partes do sistema e a disponibilidade.

c) Projeto da placa de circuito impresso (PCI): Com base no esquemático, foi projetada a placa de circuito impresso, considerando aspectos como otimização do espaço, minimização de ruídos e a viabilidade de montagem.

d) Montagem do protótipo: Após a fabricação da placa de circuito impresso, foi realizada a montagem do protótipo, com a soldagem dos componentes e a realização de testes iniciais de funcionamento.

Desenvolvimento do Firmware

O desenvolvimento do firmware foi subdividido nas seguintes etapas:

a) Definição dos requisitos e funcionalidades: Nesta etapa, foram levantados os requisitos e funcionalidades essenciais para o bom funcionamento do sistema, como a precisão das medições, o controle da estação de recarga e a comunicação entre os microcontroladores responsáveis pelo medidor de energia e pela estação de recarga.

b) Desenvolvimento do código para o microcontrolador da estação de recarga: Foi programado o microcontrolador responsável pelo controle da recarga, garantindo o monitoramento do processo, a interação com o usuário e a comunicação com o microcontrolador do medidor de energia.

c) Desenvolvimento do código para o microcontrolador do medidor de energia: Programou-se o microcontrolador dedicado à medição de energia, que realiza a leitura de corrente, tensão e o cálculo da potência consumida, além de enviar essas informações para o microcontrolador da estação de recarga. Considerou-se também a implementação de algoritmos para compensação de harmônicas e calibração dos sensores, visando garantir a precisão das medições.

d) Testes de integração e ajuste fino: Após o desenvolvimento inicial dos códigos, foram realizados testes de integração entre os microcontroladores da estação de recarga e do medidor de energia. O objetivo foi garantir que os dados de medição fossem corretamente coletados e enviados, e que o controle da recarga funcionasse de forma eficiente. Durante essa fase, ajustes foram feitos para otimizar a comunicação entre os sistemas e corrigir possíveis falhas de desempenho ou precisão.
