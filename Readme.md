# Análise por meio de grafos das bolsas de iniciação científca da UFRN 

## 📋 Descrição do Projeto

Este projeto implementa uma análise referente aos dados de bolsas de iniciação científica da Universidade Federal do Rio Grande do Norte(UFRN) utilizando **teoria dos grafos** e **análise de redes**. O sistema processa dados em formato CSV para criar grafos representando as relações entre discentes, orientadores e departamentos acadêmicos.

## 🎯 Objetivos

- **Modelar relações acadêmicas** através de grafos tripartidos
- **Identificar padrões** de orientação e colaboração
- **Visualizar estruturas** de rede acadêmica
- **Analisar métricas** como densidade
- **Gerar subgrafos** específicos por departamento

## 🏗️ Estrutura do Projeto

```
Grafos---Bolsas-IC-UFRN/
├── GrafoPrincipal.ipynb           # Grafo completo e análise gráfica do mesmo
├── Subgrafos.ipynb                # Visualização de subgrafos por departamento
├── Iniciação_Ciêntifica - Dados Abertos.csv  # Dataset de entrada
└── Readme.md                      # Arquivo de documentação
```

## 📊 Estrutura dos Dados

O dataset deve conter as seguintes colunas:

| Coluna | Descrição | Tipo |
|--------|-----------|------|
| `DiscenteID` | Identificador único do estudante | Numérico |
| `OrientadorID` | Identificador único do orientador | Numérico |
| `Unidade` | Nome do departamento/unidade acadêmica | Texto |
| `Codigo_Projeto` | Código identificador do projeto | Texto/Numérico |

## 🔧 Tecnologias Utilizadas

- **Python 3.13+**
- **NetworkX** - Manipulação e análise de grafos
- **Pandas** - Processamento de dados
- **Matplotlib** - Visualização de grafos
- **NumPy** - Operações numéricas
- **Scipy** - Algoritmos de layout para grafos
- **Jupyter Notebook** - Ambiente de desenvolvimento
- **Gemini 2.5** - Itelingência Artifical

## 📈 Funcionalidades Principais

### 1. Criação do Grafo Tripartido (`GrafoPrincipal.ipynb`)

#### Estrutura do Grafo:
- **Nós de Discentes**: Estudantes de iniciação científica
- **Nós de Orientadores**: Professores orientadores
- **Nós de Departamentos**: Unidades acadêmicas

#### Tipos de Arestas:
- **Orientação**: Conecta discentes aos seus orientadores
- **Afiliação**: Conecta orientadores aos departamentos (com peso = número de estudantes)

#### Métricas Calculadas:
- **Densidade do grafo**
- **Número total de nós e arestas**
- **Distribuição de graus**

### 2. Análises Estatísticas

#### Identificação de Elementos Destacados:
- ✅ **Professor com mais orientandos**
- ✅ **Departamento com mais discentes**
- ✅ **Top 5 orientadores por grau**
- ✅ **Top 5 departamentos por conectividade**

#### Análises de Distribuição:
- 📊 **Histograma de graus dos nós**
- 📈 **Distribuição de orientandos por professor**
- 🏆 **Ranking de departamentos por número de discentes com bolsa de iniciação científica**

### 3. Visualização de Subgrafos (`Subgrafos.ipynb`)

#### Funcionalidades:
- **Seleção interativa** de departamentos
- **Extração de subgrafos** específicos por unidade
- **Visualização otimizada** com diferentes layouts
- **Legendas e cores** diferenciadas por tipo de nó
- **Tamanhos proporcionais** baseados no número de conexões

#### Layouts Disponíveis:
- `spring_layout` (padrão) - Layout baseado em forças
- `kamada_kawai_layout` - Layout de energia mínima
- `circular_layout` - Disposição circular
- `random_layout` - Posicionamento aleatório

## 🚀 Como Executar

### Pré-requisitos

```bash
# Instalar dependências (se necessário)
pip install pandas networkx matplotlib scipy numpy jupyter
```

### Execução

1. **Clone ou baixe o projeto**
2. **Coloque seu arquivo CSV** na pasta do projeto
3. **Abra o Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```
4. **Execute os notebooks na ordem**:
   - Primeiro: `GrafoPrincipal.ipynb`
   - Segundo: `Subgrafos.ipynb`

### Configuração do Dataset

No início dos notebooks, altere o caminho do arquivo:
```python
caminho_do_seu_arquivo = "./seu_arquivo.csv"  # Substitua pelo nome do seu arquivo
```

## 📊 Exemplos de Resultados

### Métricas do Grafo Principal
```
Número total de nós: 28.212
Número total de arestas: 33.618
Densidade do grafo: 0.0000845
```

### Análises Identificadas
```
Professor com mais orientandos:
ID do Professor: 5752963
Número de orientandos: 97

Departamento com mais discentes:
Departamento: CENTRO DE CIÊNCIAS DA SAÚDE - CCS
Número de discentes: 2.468
```

## 🔍 Algoritmos e Complexidade

### Otimizações Implementadas:
- **Uso de sets** para operações de interseção O(1)
- **Evitar loops aninhados** desnecessários
- **Cache de cálculos** de grau e centralidade
- **Operações vetorizadas** com pandas

### Performance:
- ⚡ **Tempo de criação do grafo**: ~2 segundos
- ⚡ **Tempo de análises**: ~85ms
- 💾 **Uso de memória**: Otimizado para grandes datasets

## 🎨 Visualizações

### Características das Visualizações:
- **Cores diferenciadas** por tipo de nó:
  - 🔵 Azul: Discentes
  - 🟢 Verde: Orientadores  
  - 🔴 Vermelho: Departamentos
- **Tamanhos proporcionais** ao número de conexões
- **Transparência ajustável** para melhor visualização
- **Legendas informativas**

## 🔧 Configurações Avançadas

### Personalização de Layouts:
```python
# Spring Layout com parâmetros ajustáveis
pos = nx.spring_layout(subgrafo, k=0.5, iterations=50)

# Configurações de visualização
plt.figure(figsize=(18, 18))
nx.draw(grafo, pos, node_color=cores, node_size=tamanhos,
        with_labels=True, font_size=7, alpha=0.9)
```

### Ajuste de Performance:
```python
# Para datasets muito grandes, considere:
- Usar GraphX para datasets > 100k nós
- Implementar sampling para visualizações
- Cache de layouts computados
```

## 🐛 Troubleshooting

### Problemas Comuns:

1. **Erro "No module named 'scipy'"**:
   ```bash
   pip install scipy
   ```

2. **Erro de encoding no CSV**:
   - Verifique se está usando `encoding='latin-1'`
   - Teste outros encodings: `utf-8`, `cp1252`

3. **Performance lenta**:
   - Reduza o tamanho do dataset para testes
   - Use sampling para visualizações grandes

4. **Visualização ilegível**:
   - Aumente o `figsize`
   - Ajuste `font_size` e `node_size`
   - Use layouts diferentes

## � Links Úteis

### 📚 Documentação das Bibliotecas
- [NetworkX Documentation](https://networkx.org/documentation/stable/) - Documentação oficial do NetworkX
- [Pandas Documentation](https://pandas.pydata.org/docs/) - Guia completo do Pandas
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html) - Exemplos de visualizações
- [SciPy Documentation](https://docs.scipy.org/doc/scipy/) - Documentação do SciPy

### 📊 Teoria dos Grafos
- [Graph Theory Tutorial](https://www.tutorialspoint.com/graph_theory/index.htm) - Tutorial básico de teoria dos grafos
- [NetworkX Tutorial](https://networkx.org/documentation/stable/tutorial.html) - Tutorial oficial do NetworkX
- [Graph Analysis with Python](https://www.datacamp.com/tutorial/networkx-python-graph-tutorial) - Análise de grafos com Python

### 🎓 Recursos Acadêmicos
- [UFRN - Portal de Dados Abertos](https://dados.ufrn.br/) - Portal oficial de dados da UFRN
- [The Atlas for the Aspiring Network Scientist v2](https://www.springer.com/gp/book/9781846289699) - Livro gratuito sobre teoria dos grafos

### 💻 Ferramentas e Ambientes
- [Jupyter Notebook](https://jupyter.org/) - Ambiente interativo de desenvolvimento
- [Google Colab](https://colab.research.google.com/) - Ambiente online gratuito para notebooks
- [Anaconda](https://www.anaconda.com/) - Distribuição Python para ciência de dados
- [Visual Studio Code](https://code.visualstudio.com/) - Editor de código recomendado

## �📄 Licença

Este projeto foi desenvolvido para fins acadêmicos como parte da disciplina de **Algoritmos e Estruturas de Dados 2** do curo de Engenharia da Computação da UFRN ministrada pelo professor Ivanovitc Medeiros Dantes da Silva.

## 👥 Autor

Desenvolvido por **Lucas Marques** e **Diego Rabelos**.

