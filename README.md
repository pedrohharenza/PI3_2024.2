# Estação de Recarga de Veículos Elétricos PI3 2024.2

Este projeto tem como objetivo desenvolver e implementar uma estação de recarga portátil para veículos elétricos monofásica de 12A 220VAC Nível 1, com uma potência de 2,64 kW. O projeto abrange desde a seleção dos componentes, projeto dos circuitos com simulações, até a implementação prática em uma placa de circuito impresso (PCB). Para validar a funcionalidade e garantir a segurança da estação de recarga, será também desenvolvido um **Testador de Estação de Recarga**.

## Características do Projeto
- **Corrente Máxima**: 12A em 220VAC (2,64 kW).
- **Case**: Produzido com impressora 3D.
- **Interface de Usuário**: LEDs RGB para indicar estados (Idle, Pronto, Carregando, Erro).
- **Microcontrolador**: STM32 para controle e monitoramento.
- **Proteções**: Circuito de proteção de pico de tensão e filtro EMI

## Testador de Estação de Recarga
Para garantir a confiabilidade e o desempenho do carregador, será desenvolvido um **Testador de Estação de Recarga**. Este dispositivo simulará condições reais de carregamento e verificará o correto funcionamento da estação antes de ser utilizado em um veículo.

## Etapas do Projeto
1. [**Etapa 1**](Etapa%201/): [Definição dos parâmetros de funcionamento](Etapa%201/Definição%20dos%20parâmetros%20de%20funcionamento.md) e apresentar uma [simulação simplificada](Etapa%201/Simulação%20simplificada.md) para validação dos circuitos que serão utilizados.
3. **Etapa 2**: Desenvolvimento do esquemático de cada circuito que abrange os funcionamentos do carregador.
4. **Etapa 3**: Defeinição dos componentes que serão utilizados e desenvolvimento do layout da PCB.
5. **Etapa 4**: Implementação dos circuitos em PCB, implementação do código, e implementação do case em impressão 3D.

## Referências

- https://www.ti.com/lit/ug/tiduf04/tiduf04.pdf?ts=1729670182718&ref_url=https%253A%252F%252Fwww.ti.com%252Fsolution%252Fac-charging-pile-station%253Fvariantid%253D14389%2526subsystemid%253D31340
- https://www.researchgate.net/figure/Typical-control-pilot-circuit-according-to-IEC61851-1_fig1_338287849
- IEC 61851-1  Sistema de recarga condutiva para veículos elétricos Parte 1: Requisitos gerais
