# Estação de Recarga de Veículos Elétricos PI3 2024.2

Este projeto tem como objetivo desenvolver e implementar uma estação de recarga portátil para veículos elétricos monofásica de 16A 220VAC Nível 1. O projeto abrange desde a seleção dos componentes, projeto dos circuitos com simulações, até a implementação prática em uma placa de circuito impresso (PCB).

## Características do Projeto
- **Corrente Máxima**: 16A em 220VAC.
- **Gabinete**: Produzido em impressão 3D.
- **Interface de Usuário**: LEDs RGB para indicar estados (Idle, Pronto, Carregando, Erro).
- **Microcontrolador**: STM32 para controle e monitoramento de consumo de energia.
- **Proteções**: Circuito de proteção gerais.

## Etapas do Projeto
- [**Etapa 1**](Etapa%201/): [Definição dos parâmetros de funcionamento](Etapa%201/Definição%20dos%20parâmetros%20de%20funcionamento.md) e apresentar uma [simulação simplificada](Etapa%201/Simulação%20simplificada.md) para validação dos circuitos que serão utilizados.
- [**Etapa 2**](Etapa%202/): Desenvolvimento do [esquemático](Etapa%202/Esquemático.md) de cada circuito que abrange os funcionamentos do carregador.
- [**Etapa 3**](Etapa%203/): Defeinição dos componentes que serão utilizados e desenho do [layout da PCB](Etapa%203/Layout.md).
- [**Etapa 4**](Etapa%204/): Implementação dos circuitos em PCB, implementação do código, e implementação do case em impressão 3D.

## Referências

- [Texas Instruments - EVSE Reference Design](https://www.ti.com/lit/ug/tiduf04/tiduf04.pdf?ts=1729670182718&ref_url=https%253A%252F%252Fwww.ti.com%252Fsolution%252Fac-charging-pile-station%253Fvariantid%253D14389%2526subsystemid%253D31340)
- [Pionix - EVSE Reference Design](https://www.researchgate.net/figure/Typical-control-pilot-circuit-according-to-IEC61851-1_fig1_338287849)
- IEC 61851-1  Sistema de recarga condutiva para veículos elétricos Parte 1: Requisitos gerais
