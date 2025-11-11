# Parte 4: Respostas Teóricas - Escolha de Algoritmos

**Aluno:** Anderson Correa
**Disciplina:** Algoritmos de Clusterização
**Instituição:** INFNET

---

## Questão 1: Etapas do Algoritmo K-Médias

O algoritmo de K-médias funciona através das seguintes etapas até sua convergência:

1. **Inicialização**: Escolher k centróides iniciais aleatoriamente ou através de heurísticas

2. **Atribuição**: Para cada ponto de dados, calcular a distância até cada centróide e atribuir o ponto ao cluster do centróide mais próximo

3. **Atualização**: Recalcular a posição de cada centróide como sendo a média (baricentro) de todos os pontos atribuídos ao seu cluster

4. **Verificação de Convergência**: Verificar se os centróides mudaram significativamente:

   - Se o deslocamento dos centróides for menor que um limiar ε, ou
   - Se nenhum ponto mudou de cluster, ou
   - Se atingiu o número máximo de iterações

5. **Repetição**: Se não convergiu, voltar ao passo 2. Se convergiu, finalizar o algoritmo.

**Critério de Parada**: O algoritmo converge quando o deslocamento entre as iterações dos centróides é mínimo, indicando que a configuração dos clusters está estável.

---

## Questão 2: Adaptação do K-Médias para K-Medóides

O algoritmo de K-medóides (também conhecido como PAM - Partitioning Around Medoids) difere do K-médias ao garantir que o representante de cada cluster seja um ponto real do dataset, não um baricentro calculado.

### Algoritmo K-Medóides:

1. **Inicialização**: Selecionar k medóides iniciais aleatoriamente do conjunto de dados

2. **Atribuição**: Para cada ponto de dados, calcular a distância até cada medóide e atribuir o ponto ao cluster do medóide mais próximo

3. **Atualização dos Medóides**: Para cada cluster:

   - Para cada ponto p no cluster, calcular o custo total se p fosse o medóide:
     - Custo = soma das distâncias de todos os pontos do cluster até p
   - Selecionar como novo medóide o ponto que minimiza o custo total

4. **Verificação de Convergência**: Verificar se os medóides mudaram:
   - Se nenhum medóide mudou, finalizar
   - Caso contrário, voltar ao passo 2

### Diferenças principais:

- **K-Médias**: O centróide é o baricentro (média) - pode não ser um ponto real
- **K-Medóides**: O medóide é sempre um ponto existente no dataset
- **Vantagem**: K-medóides é mais robusto a outliers e funciona com qualquer métrica de distância

---

## Questão 3: Sensibilidade do K-Médias a Outliers

O algoritmo de K-médias é **sensível a outliers** devido à forma como calcula os centróides:

### Explicação:

1. **Cálculo da Média**: O centróide é calculado como a média aritmética de todos os pontos do cluster:

   ```
   centróide = (Σ pontos) / n
   ```

2. **Impacto de Outliers**: Como a média é sensível a valores extremos, um único outlier pode "puxar" o centróide significativamente na sua direção

3. **Efeito em Cascata**:
   - Um centróide deslocado por um outlier pode atrair pontos que deveriam pertencer a outros clusters
   - Isso pode distorcer toda a estrutura de clusterização
   - A minimização da soma dos quadrados das distâncias (função objetivo do K-médias) amplifica o efeito de pontos distantes

### Exemplo:

Se um cluster tem pontos em [1, 2, 3, 4, 5] e um outlier em [100]:

- Centróide sem outlier: (1+2+3+4+5)/5 = 3.0
- Centróide com outlier: (1+2+3+4+5+100)/6 = 19.2

O centróide é drasticamente deslocado, não representando bem o agrupamento natural dos dados.

---

## Questão 4: Robustez do DBScan a Outliers

O algoritmo **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** é robusto a outliers devido à sua natureza baseada em densidade:

### Explicação:

1. **Definição Baseada em Densidade**:

   - DBSCAN define clusters como regiões de alta densidade separadas por regiões de baixa densidade
   - Pontos: **core points** (densidade suficiente), **border points** (na borda), **noise points** (outliers)

2. **Parâmetros**:

   - **ε (epsilon)**: raio de vizinhança
   - **minPts**: número mínimo de pontos para formar uma região densa

3. **Tratamento de Outliers**:

   - Outliers são pontos que não pertencem a nenhuma região densa
   - São automaticamente classificados como **ruído (noise)**
   - **Não influenciam** a formação dos clusters
   - Não são forçados a pertencer a nenhum cluster

4. **Vantagens sobre K-Médias**:
   - Não precisa especificar k (número de clusters) previamente
   - Pode encontrar clusters de formas arbitrárias
   - Identifica e isola outliers automaticamente
   - Os clusters são definidos pela densidade local, não por centróides globais

### Por que é Robusto:

- **Isolamento**: Outliers ficam isolados em regiões de baixa densidade e são marcados como ruído
- **Sem Centróides**: Não usa médias globais que possam ser afetadas por valores extremos
- **Densidade Local**: Decisões são baseadas em vizinhanças locais, limitando o impacto de pontos distantes
- **Flexibilidade**: Pode detectar clusters de diferentes densidades e formas irregulares

---

## Conclusão

Cada algoritmo tem seus pontos fortes:

- **K-Médias**: Rápido e eficiente para clusters esféricos e bem separados, mas sensível a outliers
- **K-Medóides**: Mais robusto que K-médias, garante representantes reais
- **DBSCAN**: Ideal para dados com ruído e outliers, clusters de formas irregulares

A escolha do algoritmo deve considerar as características dos dados e os objetivos da análise.
