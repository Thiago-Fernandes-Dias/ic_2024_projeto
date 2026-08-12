# Avaliação de Abordagens de Ajuste de Hiperparâmetros em Dinâmica da Digitação

> **Projeto de Iniciação Científica (UFABC - Edital 01/2024)**  
> **Área:** Ciências Exatas e da Terra | Ciência da Computação (Metodologia e Técnicas da Computação)  
> **Documento Principal:** [main.pdf](main.pdf)

## Visão Geral

Este repositório contém a proposta e o desenvolvimento do projeto de iniciação científica focado na **avaliação e comparação de abordagens para ajuste de hiperparâmetros (HPO — *Hyperparameter Optimization*) em algoritmos de classificação baseados em dinâmica da digitação**.

A **dinâmica da digitação** é uma modalidade biométrica comportamental que reconhece indivíduos com base no seu ritmo e padrão de digitação (como tempo de pressão de teclas, intervalo entre digitações e taxas de erro).

## Resumo do Projeto

Sistemas de autenticação baseados em senhas estáticas possuem limitações sérias de segurança, sendo vulneráveis a ataques de força bruta ou vazamento de credenciais. A biometria comportamental surge como uma solução transparente, pois não exige hardware especializado (como leitores de impressões digitais ou câmeras), podendo ser integrada diretamente em formulários de login e aplicações web.

Contudo, a eficiência dos modelos de aprendizado de máquina aplicados a esse problema depende substancialmente do ajuste adequado de seus **hiperparâmetros** (ex.: parâmetro de penalidade $C$ em SVMs, taxa de aprendizado em redes neurais ou o **limiar de corte / *threshold*** do sistema biométrico).

### Principais Questões e Motivação

1. **Ajuste Global vs. Individualizado:** A maioria dos trabalhos aplica hiperparâmetros ou limiares de corte globais (iguais para todos os usuários). O projeto investiga se realizar o ajuste de forma **individualizada por usuário** melhora o desempenho biométrico em comparação à abordagem **global**.
2. **Limitações do Ajuste por EER na Literatura:** Diversos estudos reportam apenas o *Equal Error Rate* (EER) otimizando o limiar de corte sobre dados de teste. Em aplicações práticas, contudo, os rótulos de teste não estão disponíveis em tempo de execução, tornando indispensável o emprego de técnicas formais e rigorosas de ajuste de hiperparâmetros durante a fase de treinamento/validação.

## Objetivos

### Objetivo Geral

Comparar diferentes abordagens para ajuste de hiperparâmetros (globais e individualizadas) de algoritmos de classificação aplicados à dinâmica da digitação em **texto fixo**.

### Objetivos Específicos

* **Selecionar algoritmos** de classificação consolidados na literatura de dinâmica da digitação.
* **Definir abordagens de ajuste** de hiperparâmetros (ex.: ajuste global vs. ajuste individualizado por usuário).
* **Realizar experimentos** comparativos sistematizados.
* **Avaliar e analisar** o desempenho preditivo e biométrico obtido sob cada abordagem.

## 🔬 Metodologia

### Conjuntos de Dados (*Datasets*)

Para garantir a reprodutibilidade dos estudos, o projeto faz uso de dados publicamente disponíveis:

* **CMU Keystroke Benchmark** ([Killourhy & Maxion, 2009](https://www.cs.cmu.edu/~keystroke/)): Coleta de 51 indivíduos digitando a senha `.tie5Roanl` em 8 sessões (400 amostras por indivíduo).
* **KeyRecs** ([Dias et al., 2023](https://zenodo.org/records/7886743)): Coleta em texto fixo e livre composta por 99 indivíduos (2 sessões de 100 amostras).
* *Outras bases potenciais:* GREYC e o dataset de Risto & Graven (2024).

> **Divisão Treino/Teste:** Amostras de sessões mais antigas são utilizadas para o treinamento, enquanto amostras mais recentes são reservadas para o teste.

### Métricas de Desempenho

A avaliação biométrica segue as métricas padronizadas da literatura:

* **FMR (*False Match Rate*):** Taxa de impostores aceitos indevidamente.
* **FNMR (*False Non-Match Rate*):** Taxa de usuários genuínos rejeitados indevidamente.
* **HTER (*Half Total Error Rate*):** Média entre FMR e FNMR:
  $$\text{HTER} = \frac{\text{FNMR} + \text{FMR}}{2}$$
* **BAcc (*Balanced Accuracy* / Acurácia Balanceada):**
  $$\text{BAcc} = 1 - \text{HTER}$$
