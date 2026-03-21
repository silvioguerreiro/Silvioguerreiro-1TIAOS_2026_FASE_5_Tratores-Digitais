 <a href="https://www.fiap.com.br/">
  <img width="2385" height="642" alt="logo-fiap" src="https://github.com/user-attachments/assets/62285a6c-34fe-4206-8a85-7ad584c6908b" border="0" width="40%" height="40%">
</a>

<br>

# Cap 1 - FarmTech na Era da Cloud Computing

## 👨‍💻 Grupo 35
**Curso:** 1TIAOS – Fase 5

## 👨‍🎓 Integrantes
- [**Silvio Prestes Guerreiro Junior**](https://www.linkedin.com/in/silvio-guerreiro-junior/)
- **RM:** 567958

## 👩‍🏫 Professores
- **Tutor(a):** [Sabrina Otoni](https://www.linkedin.com/company/inova-fusca)
- **Coordenador(a):** [André Godoi Chiovato](https://www.linkedin.com/company/inova-fusca)

---

## Sumário
- [1. Descrição do projeto](#1-descrição-do-projeto)
- [2. Entrega 1 — Machine Learning](#2-entrega-1--machine-learning)
- [3. Entrega 2 — Computação em Nuvem (AWS)](#3-entrega-2--computação-em-nuvem-aws)
  - [3.1 Objetivo](#31-objetivo)
  - [3.2 Perguntas do enunciado](#32-perguntas-do-enunciado)
  - [3.3 Premissas adotadas](#33-premissas-adotadas)
  - [3.4 Escolha dos recursos na AWS](#34-escolha-dos-recursos-na-aws)
  - [3.5 Correção metodológica da estimativa](#35-correção-metodológica-da-estimativa)
  - [3.6 Comparativo detalhado de custos](#36-comparativo-detalhado-de-custos)
  - [3.7 Gráficos comparativos](#37-gráficos-comparativos)
  - [3.8 Pergunta 1 — qual a solução mais barata?](#38-pergunta-1--qual-a-solução-mais-barata)
  - [3.9 Pergunta 2 — qual opção escolher com baixa latência e restrição legal?](#39-pergunta-2--qual-opção-escolher-com-baixa-latência-e-restrição-legal)
  - [3.10 Arquitetura proposta](#310-arquitetura-proposta)
- [4. Conclusão](#4-conclusão)
- [5. Referências](#5-referências)

---

# 1. Descrição do projeto

Este repositório apresenta a resolução da atividade da **Fase 5**, organizada em dois eixos complementares:

### **Entrega 1 — Machine Learning**
- análise exploratória da base `crop_yield.csv`;
- clusterização para identificação de padrões de produtividade;
- detecção de outliers;
- treinamento e comparação de modelos de regressão;
- predição do rendimento da safra.

### **Entrega 2 — Computação em Nuvem**
- estimativa de custo mensal em AWS para hospedar uma API e o modelo de ML;
- comparação entre as regiões **São Paulo (`sa-east-1`)** e **N. Virgínia (`us-east-1`)**;
- justificativa técnica, econômica e jurídica para a escolha da região e dos recursos na nuvem.

---

# 2. Entrega 1 — Machine Learning

## 2.1 Visão geral da base

| Métrica | Valor |
|---|---:|
| Total de registros | 156 |
| Total de colunas | 6 |
| Total de culturas | 4 |
| Valores ausentes | 0 |

### Distribuição por cultura
- **Cocoa, beans:** 39 registros
- **Oil palm fruit:** 39 registros
- **Rice, paddy:** 39 registros
- **Rubber, natural:** 39 registros

## 2.2 Acesso ao notebook
- [Abrir no Google Colab](https://colab.research.google.com/drive/15rxJ8rxyo9SJ4xUpyRSVBqGOM1Bhj01Q?usp=drive_link)
- Link Video: https://youtu.be/mhZatSwNN78
---

# 3. Entrega 2 — Computação em Nuvem (AWS)

## 3.1 Objetivo

Nesta etapa foi realizada uma estimativa de custos na AWS para hospedar uma **máquina Linux simples** capaz de:

- receber os dados dos sensores da Entrega 1 por meio de uma API;
- armazenar o sistema operacional, a aplicação e o modelo de ML;
- executar o processamento necessário para inferência e rotinas básicas de Machine Learning.

A comparação foi feita entre duas regiões da AWS:

- 🇧🇷 **São Paulo (`sa-east-1`)**
- 🇺🇸 **N. Virgínia (`us-east-1`)**

---

## 3.2 Perguntas do enunciado

### **Pergunta 1**
> Usando a calculadora da AWS, qual é a solução mais barata em **On-Demand (100%)** para uma máquina Linux com:
>
> - **2 CPUs**
> - **1 GiB de memória**
> - **até 5 Gigabit de rede**
> - **50 GB de armazenamento**

### **Pergunta 2**
> Considerando a necessidade de acessar rapidamente os dados dos sensores e a existência de **restrições legais para armazenamento no exterior**, qual opção deveria ser escolhida? Justifique.

---

## 3.3 Premissas adotadas

Para que a estimativa ficasse coerente com o enunciado, foram adotadas as seguintes premissas:

1. **Cobrança On-Demand (100%)**, sem Savings Plans e sem instância reservada.  
2. **1 instância Linux** executando continuamente (**730 horas/mês**).  
3. **1 volume EBS de 50 GB** para o sistema operacional, aplicação e artefatos do modelo.  
4. **Sem cobrança de transferência de dados**, porque o enunciado não informou volume de tráfego e o arquivo exportado na calculadora foi gerado com **0 TB** de entrada e saída.  
5. **Sem monitoramento avançado, load balancer, NAT, snapshots ou banco de dados gerenciado**, pois a atividade pediu apenas uma máquina Linux simples.

### Fórmulas utilizadas

```text
Custo mensal do EC2 = preço por hora × 730
Custo mensal do EBS = preço por GB-mês × 50
Custo mensal total = EC2 + EBS
Custo anual = custo mensal total × 12
```

---

## 3.4 Escolha dos recursos na AWS

### **Instância escolhida: Amazon EC2 t4g.micro**

A instância **`t4g.micro`** foi escolhida porque é a opção de menor custo que atende diretamente aos requisitos de hardware solicitados:

- **2 vCPU**
- **1 GiB de memória**
- **rede de até 5 Gbps**

Além disso, ela pertence à família **T4g**, baseada em **AWS Graviton2 (ARM64)**, voltada para cargas gerais de baixo custo, como APIs simples, serviços web e processamento leve a moderado. Como contrapartida, é importante validar a compatibilidade da aplicação e das bibliotecas com a arquitetura ARM64.

### **Armazenamento: Amazon EBS**

A instância `t4g.micro` utiliza armazenamento **EBS-only**, portanto o volume em bloco é necessário para persistir:

- sistema operacional Linux;
- código da API;
- bibliotecas e artefatos do modelo de Machine Learning;
- arquivos temporários ou buffers de ingestão dos sensores.

### **Observação técnica sobre o item “HD” do enunciado**

Embora o enunciado cite “50 GB de armazenamento (HD)”, a estimativa final adotou **EBS gp3** como volume principal por um motivo técnico importante: os volumes **`st1`** e **`sc1`** (HDD) **não podem ser usados como volume de boot**, e a própria AWS recomenda SSD de uso geral para cargas com leitura e escrita pequenas e aleatórias. Em uma VM Linux simples que hospedará uma API e ML, `gp3` é a escolha mais consistente para o volume raiz.

> **Resumo da decisão técnica**
> - **EC2**: escolhido porque o enunciado pede uma máquina Linux simples.
> - **t4g.micro**: escolhido porque atende exatamente 2 vCPU, 1 GiB e até 5 Gbps.
> - **EBS**: escolhido porque a instância é EBS-only e precisa de persistência.
> - **gp3**: adotado por ser o volume de uso geral mais adequado ao boot e à aplicação.

---

## 3.5 Correção metodológica da estimativa

O arquivo `My Estimate (1).csv`, exportado anteriormente da AWS Pricing Calculator, **não responde integralmente ao enunciado**, porque os preços nele registrados usam modalidades com desconto de longo prazo:

- **São Paulo:** `3yr No Upfront`
- **N. Virgínia:** `Compute Savings Plans 3yr No Upfront`

Por essa razão, os valores do CSV foram usados apenas como **evidência da simulação inicial**, mas a resposta final desta entrega foi **recalculada em On-Demand (100%)**.

### Comparação entre a simulação exportada e a estimativa final

| Base de cálculo | São Paulo | N. Virgínia | Observação |
|---|---:|---:|---|
| CSV exportado da calculadora | US$ 10,89/mês | US$ 5,57/mês | não está em On-Demand |
| Estimativa final desta entrega | US$ 17,38/mês | US$ 10,13/mês | recalculada em On-Demand 100% |

---

## 3.6 Comparativo detalhado de custos

### **3.6.1 Custo da instância EC2 (Linux, On-Demand)**

| Região | Preço por hora | Custo mensal (730 h) | Custo anual |
|---|---:|---:|---:|
| 🇺🇸 us-east-1 (N. Virgínia) | US$ 0,0084 | US$ 6,13 | US$ 73,58 |
| 🇧🇷 sa-east-1 (São Paulo) | US$ 0,0134 | US$ 9,78 | US$ 117,38 |

### **3.6.2 Custo do armazenamento EBS (50 GB)**

| Região | Preço por GB-mês | Tipo considerado | Custo mensal | Custo anual |
|---|---:|---|---:|---:|
| 🇺🇸 us-east-1 | US$ 0,08 | EBS gp3 | US$ 4,00 | US$ 48,00 |
| 🇧🇷 sa-east-1 | US$ 0,152 | EBS gp3 | US$ 7,60 | US$ 91,20 |

### **3.6.3 Custo total**

| Região | EC2 mensal | EBS mensal | Total mensal | Total anual |
|---|---:|---:|---:|---:|
| 🇺🇸 us-east-1 | US$ 6,13 | US$ 4,00 | **US$ 10,13** | **US$ 121,58** |
| 🇧🇷 sa-east-1 | US$ 9,78 | US$ 7,60 | **US$ 17,38** | **US$ 208,58** |

### **Leitura financeira do comparativo**
- A opção em **N. Virgínia** economiza **US$ 7,25 por mês** e **US$ 87,00 por ano** em relação a São Paulo.
- Em termos relativos, **São Paulo custa cerca de 71,6% a mais** do que N. Virgínia.
- Pela ótica inversa, **us-east-1 custa cerca de 41,7% menos** do que sa-east-1.

---

## 3.7 Gráficos comparativos

### **Gráfico 1 — custo mensal por região**
<img width="1579" height="940" alt="custo_mensal_aws" src="https://github.com/user-attachments/assets/5b4811e8-d685-4ea9-8531-1ae5535ab798" />

O gráfico mensal deixa evidente que a diferença de preço não está apenas na computação. O custo da região de São Paulo é maior **tanto na instância EC2 quanto no volume EBS**, o que amplia a diferença no total final.

### **Gráfico 2 — custo anual por região**
<img width="1582" height="731" alt="custo_anual_aws" src="https://github.com/user-attachments/assets/d60de760-e536-463b-acd8-0674216f5ed4" />

A visualização anual mostra melhor o impacto da decisão arquitetural: embora a diferença mensal pareça moderada, no horizonte de 12 meses o custo adicional de São Paulo ultrapassa **US$ 87,00**.

### **Gráfico 3 — matriz de decisão**
<img width="1480" height="699" alt="matriz_decisao_aws" src="https://github.com/user-attachments/assets/d9941cc0-25fa-4825-91f0-cf41860c3e17" />

A matriz sintetiza o raciocínio da entrega:
- **us-east-1** é superior no critério **custo**;
- **sa-east-1** é superior em **latência para sensores no Brasil** e em **adequação jurídica**, quando existe restrição para armazenamento internacional.

---

## 3.8 Pergunta 1 — qual a solução mais barata?

### **Resposta objetiva**
> A solução **mais barata** é hospedar a máquina Linux na região **`us-east-1` (N. Virgínia)**.

### **Justificativa**
Essa escolha é a mais econômica porque:
- o preço **On-Demand** da instância `t4g.micro` é menor em `us-east-1`;
- o custo do volume **EBS gp3** também é menor em `us-east-1`;
- a soma dos dois componentes produz o menor custo total do comparativo.

### **Síntese da resposta da Pergunta 1**
- **Região mais barata:** `us-east-1`
- **Custo mensal estimado:** **US$ 10,13**
- **Custo anual estimado:** **US$ 121,58**

---

## 3.9 Pergunta 2 — qual opção escolher com baixa latência e restrição legal?

### **Resposta objetiva**
> Se houver necessidade de **acessar rapidamente os dados dos sensores** e houver **restrições legais para armazenar dados no exterior**, a melhor escolha é a região **`sa-east-1` (São Paulo)**.

### **Justificativa técnica**
Quando os sensores estão no Brasil, usar a região de São Paulo tende a reduzir a distância física entre origem e processamento. Isso favorece:
- menor latência;
- maior agilidade de ingestão dos dados;
- melhor tempo de resposta da API;
- menor sensibilidade a atrasos em chamadas de rede.

### **Justificativa jurídica**
Sob a ótica da **LGPD**, a escolha de `sa-east-1` é mais prudente quando o projeto tem restrição para armazenamento fora do país:

- o **art. 33** trata da **transferência internacional de dados** e condiciona esse envio a hipóteses específicas;
- o **art. 46** determina a adoção de medidas técnicas e administrativas aptas a proteger os dados;
- os princípios da **segurança** e da **prevenção** reforçam a necessidade de desenhar a arquitetura de forma a reduzir riscos jurídicos e operacionais.

### **Síntese da resposta da Pergunta 2**
- **Região escolhida quando há restrição legal e necessidade de baixa latência:** `sa-east-1`
- **Motivo principal:** melhor aderência operacional e jurídica ao cenário do enunciado

---

## 3.10 Arquitetura proposta

<img width="1600" height="900" alt="arquitetura_farmtech_aws" src="https://github.com/user-attachments/assets/e8604187-60f6-459b-b8af-3141f35aa3f4" />


### Leitura da arquitetura
1. **Sensores em campo** enviam dados para a aplicação.
2. A **API** é executada em uma instância **EC2 t4g.micro**.
3. O mesmo host também executa a camada de **Machine Learning**.
4. O armazenamento persistente é feito em **EBS (50 GB)**.
5. A mesma arquitetura pode ser implantada em ambas as regiões; o que muda é o custo e a adequação do cenário.

---

## 3.11 Link Video
https://youtu.be/-54wGEJ8z28

--

# 4. Conclusão

A análise demonstra que a decisão em nuvem não deve considerar apenas o menor preço, mas também o contexto operacional e regulatório da solução.

## **Conclusão da Pergunta 1**
A região **`us-east-1` (N. Virgínia)** é a **opção mais barata** para a máquina Linux especificada, com custo estimado de **US$ 10,13/mês**.

## **Conclusão da Pergunta 2**
Se o projeto exigir **baixa latência para os sensores** e houver **restrição ao armazenamento no exterior**, a escolha mais adequada passa a ser **`sa-east-1` (São Paulo)**, ainda que o custo seja maior.

## **Decisão final resumida**

| Critério | Melhor opção |
|---|---|
| **Menor custo** | `us-east-1` |
| **Menor latência para sensores no Brasil** | `sa-east-1` |
| **Maior aderência jurídica ao cenário proposto** | `sa-east-1` |

> Em síntese: **us-east-1 vence em custo**, mas **sa-east-1 vence quando o projeto precisa manter os dados no Brasil e responder mais rapidamente à origem dos sensores**.

---

# 5. Referências

1. AWS — **General purpose EC2 instance types (T4g)**  
   https://aws.amazon.com/ec2/instance-types/general-purpose/

2. AWS — **EC2 On-Demand Pricing**  
   https://aws.amazon.com/ec2/pricing/on-demand/

3. AWS — **Amazon EBS pricing**  
   https://aws.amazon.com/pt/ebs/pricing/

4. AWS — **Amazon EBS volume types**  
   https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html

5. EC2DB — **t4g.micro regional pricing** (dados oriundos da AWS Pricing API)  
   https://www.ec2db.com/instances/t4g.micro

6. AWS Pricing — **us-east-1 regional EBS prices**  
   https://aws-pricing.com/us-east-1.html

7. AWS Pricing — **sa-east-1 regional EBS prices**  
   https://aws-pricing.com/sa-east-1.html

8. Planalto — **Lei nº 13.709/2018 (LGPD)**  
   https://www.planalto.gov.br/ccivil_03/_Ato2015-2018/2018/Lei/L13709.htm

9. Governo Federal — **Princípios da LGPD**  
   https://www.gov.br/saude/pt-br/acesso-a-informacao/lgpd/principios

---

