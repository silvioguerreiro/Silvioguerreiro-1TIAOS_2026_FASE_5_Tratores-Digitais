 <a href="https://www.fiap.com.br/"><img width="2385" height="642" alt="logo-fiap" src="https://github.com/user-attachments/assets/62285a6c-34fe-4206-8a85-7ad584c6908b" border="0" width=40% height=40%></a>  

<br>

# Cap 1 - FarmTech na Era da Cloud Computing

## 👨‍💻 Grupo – 35  
**Curso:** 1TIAOS – Fase 5  

## 👨‍🎓 Integrantes  
* [**Silvio Prestes Guerreiro Junior**](https://www.linkedin.com/in/silvio-guerreiro-junior/)
* **Matrícula:** RM567958

## 👩‍🏫 Professores  
**Tutor(a):** [Sabrina Otoni](https://www.linkedin.com/company/inova-fusca)  
**Coordenador(a):** [André Godoi Chiovato](https://www.linkedin.com/company/inova-fusca)  

---
## 1. Descrição

Este repositório resolve a atividade da **Fase 5** em dois eixos:

- **Entrega 1 — Machine Learning**
  - análise exploratória da base `crop_yield.csv`;
  - clusterização para identificar tendências de produtividade;
  - detecção de outliers;
  - treinamento e comparação de modelos de regressão para prever o **rendimento da safra**.

- **Entrega 2 — Computação em Nuvem**
  - estimativa de custo mensal na AWS para hospedar uma API e o modelo de ML;
  - comparação entre **São Paulo (sa-east-1)** e **N. Virginia (us-east-1)**;
  - justificativa técnica da região escolhida.

## 2. Entrega 1 — Machine Learning

## 2.1 Visão geral da base

- Total de registros: **156**
- Total de colunas: **6**
- Total de culturas: **4**
- Não há valores ausentes
- Distribuição por cultura:
  - **Cocoa, beans**: 39 registros
  - **Oil palm fruit**: 39 registros
  - **Rice, paddy**: 39 registros
  - **Rubber, natural**: 39 registros
    
## 2.2 Link de acesso ao Jupyter

  - https://colab.research.google.com/drive/15rxJ8rxyo9SJ4xUpyRSVBqGOM1Bhj01Q?usp=drive_link


## 3. Entrega 2 — Computação em Nuvem (AWS)

## 3.1 Premissas

Foi considerada uma máquina Linux simples para hospedar:

- uma API para receber dados dos sensores;
- o modelo de Machine Learning da Entrega 1.

Configuração solicitada:

- **2 CPUs**
- **1 GiB de memória**
- **até 5 Gigabit de rede**
- **50 GB de armazenamento HD**

## 3.2 Escolha da instância

A opção mais barata que atende a esse perfil é a **t4g.micro**.

## 3.3 Estimativa de custo mensal

Para atender ao requisito de armazenamento **HD**, foi considerado **EBS standard (magnetic)** com 50 GB.

| Região | Instância | EC2 mensal (USD) | EBS 50 GB (USD) | Total mensal (USD) |
|---|---|---:|---:|---:|
| us-east-1 (N. Virginia) | t4g.micro | 6,13 | 2,50 | **8,63** |
| sa-east-1 (São Paulo) | t4g.micro | 9,78 | 6,00 | **15,78** |

![Comparação de custo mensal AWS](images/aws_cost_comparison.png)

## 3.4 Qual é a solução mais barata?

A solução mais barata é:

# **us-east-1 (N. Virginia)**

Total estimado: **USD 8,63/mês**

## 3.5 Qual região escolher se houver restrição legal para armazenamento no exterior?

Se houver:

- necessidade de acesso rápido aos sensores;
- exigência de armazenamento local;
- restrição para armazenamento fora do Brasil;

a melhor escolha é:

# **sa-east-1 (São Paulo)**

### Justificativa

- menor latência para sensores e aplicações no Brasil;
- melhor aderência à residência de dados;
- menor complexidade de governança quando existe restrição a armazenamento internacional.

## 3.6 Resposta final da Entrega 2

- **Mais barato:** us-east-1 (N. Virginia)
- **Melhor opção com restrição legal e menor latência:** sa-east-1 (São Paulo)

## 4. Vídeos

Substitua pelos links finais antes da entrega:

- **Vídeo 1 — Entrega 1:** COLE_AQUI_O_LINK_DO_YOUTUBE_NAO_LISTADO
- **Vídeo 2 — Entrega 2:** COLE_AQUI_O_LINK_DO_YOUTUBE_NAO_LISTADO

## 5.Resultado final do projeto

- identificou padrões de produtividade por clusterização;
- detectou cenários discrepantes;
- construiu e comparou múltiplos modelos de regressão;
- selecionou um modelo final com bom desempenho;
- comparou custo em nuvem entre duas regiões AWS;
- justificou a escolha da região mais adequada em contexto técnico e legal.
