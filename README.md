# 25E4-2

**Aluno:** Anderson Correa

**Disciplina:** Algoritmos de Clusterização

**Instituição:** INFNET

## Visão Geral do Projeto

Este projeto realiza análise de clusterização em dados socioeconômicos e de saúde para determinar índices de desenvolvimento de países utilizando os algoritmos K-Means e Clusterização Hierárquica.

## Requisitos

- Python 3.9+
- Ambiente virtual (venv)

## Instruções de Configuração

### 1. Criar e ativar ambiente virtual

```bash
python3 -m venv venv
source venv/bin/activate  # macOS/Linux
# venv\Scripts\activate   # Windows
```

### 2. Instalar dependências

```bash
pip install -r requirements.txt
```

### 3. Executar Jupyter Notebook

```bash
jupyter notebook projeto_25E4_2.ipynb
```

## Estrutura do Projeto

```
/
├── venv/                               # Ambiente virtual
├── projeto_25E4_2.ipynb                # Notebook principal
├── Country-data.csv                    # Dataset
├── data-dictionary.csv                 # Dicionário de dados
├── requirements.txt                    # Dependências
├── respostas_teoricas.md               # Respostas às perguntas teóricas
└── README.md
```

## Etapas da Análise

1. **Carregamento dos Dados**: Carregar dataset de desenvolvimento de países
2. **Análise Exploratória dos Dados**:
   - Contar países
   - Visualizar faixas das variáveis
   - Identificar necessidades de pré-processamento
3. **Pré-processamento dos Dados**: Padronização usando StandardScaler
4. **Clusterização K-Means**:
   - Aplicar K-Means com k=3
   - Interpretar distribuições dos clusters
   - Encontrar países representativos (mais próximos dos centróides)
5. **Clusterização Hierárquica**:
   - Aplicar Clusterização Aglomerativa
   - Gerar dendrograma
   - Interpretar resultados
6. **Comparação**: Comparar K-Means vs Clusterização Hierárquica

## Principais Descobertas

A análise agrupa países em 3 grupos baseados em indicadores socioeconômicos:

- Indicadores de nível de desenvolvimento
- Métricas de saúde
- Fatores econômicos

Os resultados são visualizados usando projeção PCA e dendrogramas.
