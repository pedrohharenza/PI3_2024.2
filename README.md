# Estação de Recarga de Veículos Elétricos PI3 2024.2

Este projeto tem como objetivo desenvolver e implementar um carregador portátil para veículos elétricos de 16A e 220VAC, com uma potência de 3,52 kW. O projeto abrange todas as etapas, desde a seleção dos componentes, o projeto dos circuitos com simulações, até a implementação prática em uma placa de circuito impresso (PCB). Para validar a funcionalidade e garantir a segurança da estação de recarga, será também desenvolvido um **Testador de Estação de Recarga**.

## Características do Projeto
- **Corrente Máxima**: 16A em 220VAC (3,52 kW).
- **Case**: Produzido com impressora 3D.
- **Interface de Usuário**: LEDs RGB para indicar estados (Idle, Pronto, Carregando, Erro).
- **Microcontrolador**: STM32 para controle e monitoramento.
- **Proteções**: Circuito de protesão de pico de tensão e filtro EMI

## Testador de Estação de Recarga
Para garantir a confiabilidade e o desempenho do carregador, será desenvolvido um **Testador de Estação de Recarga**. Este dispositivo simulará condições reais de carregamento e verificará o correto funcionamento da estação, analisando parâmetros como corrente, tensão e comportamento sob carga.

## Etapas do Projeto
1. **Etapa 1**: Definição dos parâmetros de funcionamento da estação de recarga e apresentar uma simulação simplificada para validação dos circuitos que serão utilizados.
2. **Etapa 2**: Desenvolvimento do esquemático de cada circuito que abrange os funcionamentos do carregador.
3. **Etapa 3**: Defeinição dos componentes que serão utilizados e desenvolvimento do layout da PCB.
4. **Etapa 4**: Implementação dos circuitos em PCB, implementação do código, e implementação do case em impressão 3D.
