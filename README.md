# Tarot da Morte: Predição de Desfecho em Casos de SRAG (2013–2025)

**Projeto acadêmico de ciência de dados aplicado à saúde pública**, desenvolvido como trabalho final da disciplina *Introdução à Ciência de Dados* do Instituto Federal de Brasília (IFB).

## Visão Geral

Este projeto visa **prever o desfecho clínico (alta ou óbito)** em casos de Síndrome Respiratória Aguda Grave (SRAG) utilizando dados públicos do SIVEP-Gripe (2013–2025). A abordagem combina **análise exploratória avançada** com **modelagem de machine learning** para identificar padrões de risco e construir um modelo preditivo com finalidade de vigilância epidemiológica.

## Objetivos

* Consolidar e harmonizar 13 anos de dados públicos de SRAG (2013–2025)
* Realizar análise exploratória (EDA) para identificar fatores de risco
* Desenvolver um modelo de classificação binária para predição de desfecho
* Avaliar a importância relativa das variáveis clínicas e demográficas
* Documentar todo o processo para reprodutibilidade e extensão futura

## Dados

* **Fonte:** SIVEP-Gripe (Ministério da Saúde, Brasil)
* **Período:** 2013 a 2025
* **Registros brutos:** ~5 milhões
* **Registros para análise:** 4.173.338 (após filtragem)
* **Variáveis selecionadas:** 15 (idade, sexo, UTI, comorbidades, desfecho)

### Links para bases públicas

* [SRAG 2013–2018](https://opendatasus.saude.gov.br/dataset/srag-2013-2018)
* [SRAG 2021–2024](https://opendatasus.saude.gov.br/dataset/srag-2021-a-2024)
* [Banco de dados já tratado (SQLite)](https://drive.google.com/file/d/1okXrX9d5NSgrb4BnvT_K9GivemfASZyK/view?usp=drive_link)

## Estrutura de Pastas

```
Tarot_da_Morte/
├── artigo/           # Artigo científico formatado
├── imagens/eda/      # Gráficos e figuras da análise exploratória
├── notebook/         # Notebooks principais (.ipynb)
├── video/            # Slides e vídeo de apresentação
└── README.md         # Este arquivo
```

## Metodologia

### 1. Harmonização de Dados (V5)

* Unificação de 13 arquivos CSV em banco SQLite
* Padronização de nomenclaturas (ex: `METABOLICA` → `DIABETES`)
* Tratamento de inconsistências de estrutura e encoding

### 2. Pré-processamento

* Criação da variável alvo binária `TARGET` (0=Alta, 1=Óbito)
* Binarização de variáveis categóricas (UTI, comorbidades)
* Tratamento de idade (correção de valores >120 anos, formato 40XX)
* Codificação de sexo (M=1, F=0)

### 3. Análise Exploratória (EDA)

* Distribuição do desfecho (24,62% óbitos)
* Análise de idade por desfecho (média: 43,5 anos vs 66,5 anos)
* Impacto de UTI (43,75% mortalidade vs 13,84%)
* Taxa de óbito por comorbidades e contagem cumulativa

### 4. Modelagem Preditiva

* **Algoritmo:** Regressão Logística com `class_weight='balanced'`
* **Features:** 10 variáveis (idade, sexo, UTI, suporte ventilatório, 6 comorbidades)
* **Divisão:** 80% treino, 20% teste (estratificado)
* **Avaliação:** AUC-ROC, matriz de confusão, precisão, recall

## Resultados Principais

### Estatísticas Descritivas

* **Total de casos:** 4.173.338
* **Taxa de óbito:** 24,62%
* **Idade média (óbito):** 66,5 anos
* **Internação em UTI:** 29,47% dos casos

### Desempenho do Modelo

| Métrica              | Valor      |
| -------------------- | ---------- |
| **AUC-ROC**          | **0,8262** |
| **Acurácia**         | 73,45%     |
| **Recall (Óbito)**   | 75%        |
| **Precisão (Óbito)** | 47%        |

### Features Mais Importantes

1. **SUPORT_VEN_BIN** (suporte ventilatório)
2. **UTI_BIN** (internação em UTI)
3. **ASMA_BIN** (impacto negativo)
4. **RENAL_BIN** (doença renal)
5. **CS_SEXO_BIN** (masculino)

## Como Reproduzir

1. **Acesse o notebook principal:**

   * [Google Colab - TarotdaMorte.ipynb](https://colab.research.google.com/drive/128ozXS6nYkqqrJ7I8XinUG_ShsLMQcOB?authuser=0#scrollTo=NX5lrtdsMcvD)
2. **Execute as células sequencialmente:**

   * Monte o Google Drive
   * Extraia o banco SQLite
   * Realize o pré-processamento
   * Execute a análise exploratória
   * Treine e avalie o modelo

## Documentação

* **Artigo Científico:** Artigo formatado no padrão Springer LNCS
* **Relatório Técnico:** Detalhamento da harmonização V5 e metodologia
* **Vídeo Explicativo:** https://drive.google.com/drive/folders/1L7qTMUcZgZs-_YSV_cD3DBcQ8ZemNmhi?usp=sharing 

## Autores

* **Mayara Vieira Martins Santos** - [ORCID](https://orcid.org/0009-0001-7946-7855)
* **Ryan Sousa de Moraes** - [ORCID](https://orcid.org/0009-0002-6856-8906)

**Orientação:** Prof. Fábio Henrique (IFB)
**Disciplina:** Introdução à Ciência de Dados
**Período:** 2025/2

## Agradecimentos

* Instituto Federal de Brasília (IFB) pelo apoio institucional
* Ministério da Saúde pela disponibilização dos dados do SIVEP-Gripe
* Professores e colegas pelo suporte durante o desenvolvimento

---

**Palavras-chave:** srag, machine-learning, saude-publica, python, predicao, datascience, epidemiologia, ifb


