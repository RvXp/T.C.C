# Impacto das Funções de Ativação na Generalização de Redes Neurais para Detecção de Ataques DDoS

Este repositório contém o código-fonte desenvolvido para o Trabalho de Conclusão de Curso (TCC) do Bacharelado em Sistemas de Informação da Universidade Federal de Uberlândia (UFU).

O objetivo do projeto é investigar o impacto de diferentes funções de ativação na capacidade de generalização de Redes Neurais Artificiais aplicadas à detecção de ataques de Negação de Serviço Distribuída (DDoS).

---

## 📖 Resumo

Modelos baseados em aprendizado de máquina frequentemente apresentam resultados elevados quando treinados e avaliados sobre o mesmo conjunto de dados. Entretanto, esses resultados nem sempre se mantêm quando os modelos são aplicados a tráfego proveniente de ambientes distintos.

Neste estudo, três configurações de Redes Neurais Artificiais foram comparadas, mantendo-se constantes:

- Arquitetura;
- Otimizador;
- Função de perda;
- Taxa de aprendizado;
- Estratégia de treinamento;
- Conjunto de atributos.

A única variável alterada foi a função de ativação da camada oculta:

- Sigmoid
- ReLU
- Tanh

Os modelos foram treinados utilizando o dataset **CICDDoS2019** e posteriormente avaliados, sem novo treinamento, no dataset **UNSW-NB15**, permitindo analisar sua capacidade de generalização diante da mudança de domínio.

---

## 🎯 Questões de Pesquisa

### RQ1

Em que medida a função de ativação da camada oculta influencia o desempenho e o perfil de erros de redes neurais aplicadas à detecção de ataques DDoS?

### RQ2

Em que medida o desempenho obtido no CICDDoS2019 é preservado quando os modelos são avaliados em um conjunto de dados externo (UNSW-NB15)?

---

## 🧠 Arquiteturas Avaliadas

As três arquiteturas compartilham exatamente a mesma estrutura:

```text
Entrada
   │
   ▼
Camada Oculta (128 neurônios)
   │
   ├── Sigmoid
   ├── ReLU
   └── Tanh
   │
   ▼
Dropout (0.3)
   │
   ▼
Saída Sigmoid
```

### Hiperparâmetros

```python
Loss Function = BCELoss
Optimizer     = Adam
Learning Rate = 0.01
Epochs        = 5
Batch Size    = 1024
Train/Test    = 60/40
```

---

## 📂 Datasets Utilizados

### CICDDoS2019

Dataset utilizado para:

- Treinamento;
- Validação interna;
- Teste interno.

Escopo do estudo:

- UDP Flood;
- UDP-Lag.

**Fonte:**

https://www.unb.ca/cic/datasets/ddos-2019.html

---

### UNSW-NB15

Dataset utilizado exclusivamente para:

- Avaliação externa;
- Testes de generalização.

**Fonte:**

https://research.unsw.edu.au/projects/unsw-nb15-dataset

---

## 🔬 Features Utilizadas

O estudo utiliza exclusivamente métricas estatísticas de fluxo de rede, evitando atributos excessivamente dependentes do ambiente de captura.

Exemplos:

```text
Flow Duration
Total Fwd Packets
Total Backward Packets
Flow Bytes/s
Flow Packets/s
Fwd Packet Length Mean
Bwd Packet Length Mean
Flow IAT Mean
Active Mean
Idle Mean
Average Packet Size
```

---

## ⚙️ Fluxo Experimental

```text
CICDDoS2019
      │
      ▼
Pré-processamento
      │
      ▼
Treinamento
      │
      ▼
Teste Interno
      │
      ▼
Modelo Treinado
      │
      ▼
UNSW-NB15
      │
      ▼
Inferência
      │
      ▼
Avaliação da Generalização
```

---

## 📊 Principais Resultados

### Avaliação no CICDDoS2019

| Modelo | Acurácia |
|----------|----------|
| Sigmoid | 97.02% |
| ReLU | 95.56% |
| Tanh | 96.45% |

---

### Avaliação no UNSW-NB15

| Modelo | Acurácia |
|----------|----------|
| Sigmoid | 71.46% |
| ReLU | 74.31% |
| Tanh | 69.28% |

---

### Retenção de Desempenho

| Modelo | Retenção de Acurácia |
|----------|----------|
| Sigmoid | 73.65% |
| ReLU | 77.76% |
| Tanh | 71.83% |

---

## 📈 Conclusão Principal

Embora a função de ativação **Sigmoid** tenha apresentado o melhor desempenho no domínio de treinamento (CICDDoS2019), a função **ReLU** demonstrou maior robustez e capacidade de generalização quando avaliada no domínio externo (UNSW-NB15).

Os resultados sugerem que o melhor desempenho em um único dataset não implica necessariamente melhor desempenho em cenários reais ou domínios distintos.

---

## 📁 Estrutura do Projeto

```text
T.C.C/
│
├── datasets/
│   ├── CICDDoS2019/
│   └── UNSW-NB15/
│
├── notebooks/
│
├── models/
│
├── results/
│   ├── metrics/
│   ├── confusion_matrix/
│   └── plots/
│
├── src/
│   ├── preprocessing/
│   ├── training/
│   ├── evaluation/
│   └── inference/
│
├── requirements.txt
└── README.md
```

> Ajuste esta seção conforme a estrutura real do repositório.

---

## 🚀 Como Executar

### 1. Clonar o repositório

```bash
git clone https://github.com/RvXp/T.C.C.git
cd T.C.C
```

### 2. Criar ambiente virtual

```bash
python -m venv venv
```

Linux/macOS:

```bash
source venv/bin/activate
```

Windows:

```powershell
venv\Scripts\activate
```

### 3. Instalar dependências

```bash
pip install -r requirements.txt
```

### 4. Executar treinamento

```bash
python train.py
```

### 5. Executar inferência

```bash
python inference.py
```

---

## 🛠 Tecnologias Utilizadas

- Python
- PyTorch
- Scikit-Learn
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

---

## ⚠️ Limitações

As conclusões deste estudo são restritas ao cenário experimental avaliado:

- Redes neurais densas (MLP);
- Ataques UDP Flood e UDP-Lag;
- Dataset CICDDoS2019;
- Dataset UNSW-NB15;
- Classificação binária (Benigno × Ataque).

Portanto, os resultados não devem ser generalizados para todos os tipos de ataques ou ambientes operacionais sem validações adicionais.

---

## 📚 Referência

Caso utilize este código ou os resultados deste trabalho em pesquisas futuras, cite:

```bibtex
@misc{pimenta2026activation,
  author = {Rafael Vinicius Xavier Pimenta},
  title = {Impacto das Funções de Ativação na Generalização de Redes Neurais para Detecção de Ataques DDoS},
  year = {2026},
  school = {Universidade Federal de Uberlândia},
  type = {Trabalho de Conclusão de Curso}
}
```

---

## 👨‍💻 Autor

**Rafael Vinicius Xavier Pimenta**

Bacharelado em Sistemas de Informação  
Universidade Federal de Uberlândia (UFU)

**Orientador:** Prof. Dr. Diego Nunes Molinos  
**Coorientador:** Prof. Dr. Augusto Tannus Silva

---

⭐ Caso este projeto seja útil para sua pesquisa ou estudo, considere deixar uma estrela no repositório.
