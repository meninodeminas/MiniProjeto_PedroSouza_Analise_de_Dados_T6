# 📊 Análise de Dados de Varejo com Python
Mini-Projeto Avaliativo - Módulo 1 - Semana 07 - Curso de Análise de Dados com Python

📌 Sobre o projeto

Este projeto apresenta uma análise exploratória e tratamento de dados de varejo utilizando Python, aplicando técnicas fundamentais de preparação, limpeza, validação, estatística descritiva e agregação de dados.

O objetivo é transformar uma base transacional em um conjunto de dados mais consistente e estruturado, permitindo identificar padrões relacionados a:

categorias de produtos;
perfil de clientes;
quantidade de itens por compra;
distribuição das compras por gênero;
comportamento das transações ao longo da semana;
evolução do volume de compras;
qualidade e consistência dos dados.

O projeto foi desenvolvido como parte do Mini-Projeto Avaliativo do Módulo 1 — Semana 07 do Curso de Análise de Dados com Python.

🎯 Objetivos
Objetivo geral

Realizar o processo de preparação e análise exploratória de uma base de dados de varejo, utilizando Python e bibliotecas de análise de dados.

Objetivos específicos
Importar e estruturar a base de dados;
Avaliar a estrutura e os tipos das variáveis;
Padronizar variáveis de data;
Identificar valores ausentes;
Tratar categorias sem classificação;
Identificar e remover registros duplicados;
Validar a relação entre compras e itens vendidos;
Aplicar estatística descritiva;
Realizar agrupamentos com groupby;
Criar tabelas dinâmicas com pivot_table;
Calcular percentuais de participação;
Analisar o comportamento das compras por dia da semana;
Avaliar a evolução semanal das transações;
Exportar uma versão tratada da base.
🗂️ Estrutura do repositório
MiniProjeto_PedroSouza_Analise_de_Dados_T6/
│
├── BaseVarejo.csv
├── df_limpo.csv
├── Mini_Projeto_Varejo.py
├── README.md
└── .gitignore
Arquivos
Arquivo	Descrição
BaseVarejo.csv	Base de dados original utilizada na análise
Mini_Projeto_Varejo.py	Script Python responsável pelo processo de análise
df_limpo.csv	Base resultante após tratamento e limpeza
.gitignore	Arquivos e diretórios ignorados pelo Git
README.md	Documentação do projeto

A estrutura atual do repositório contém esses arquivos principais.

🧰 Tecnologias utilizadas

O projeto foi desenvolvido em Python, utilizando principalmente as seguintes bibliotecas:

🐍 Python

Linguagem utilizada para implementação de todo o processo de análise.

🐼 Pandas

Utilizado para:

leitura da base;
manipulação de DataFrames;
tratamento de valores ausentes;
conversão de tipos;
remoção de duplicidades;
agrupamentos;
tabelas dinâmicas;
análise temporal;
exportação dos dados tratados.
🔢 NumPy

Utilizado como biblioteca de apoio para operações relacionadas à manipulação e análise numérica.

📈 Matplotlib

Biblioteca utilizada como suporte à visualização e exploração dos dados.

📦 KaggleHub

Utilizado para obtenção programática da base de dados disponibilizada no Kaggle.

🔄 Pipeline de análise

O projeto segue um fluxo de tratamento e análise dividido em etapas:

          ┌─────────────────────┐
          │   Base de Varejo    │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │     Ingestão        │
          │      dos dados      │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Exploração inicial  │
          │ estrutura e tipos   │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Tratamento de tipos │
          │      e datas        │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Limpeza de nulos e  │
          │     duplicidades    │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Validação da        │
          │ estrutura de compra │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Estatística         │
          │    descritiva       │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Agrupamentos e      │
          │  tabelas dinâmicas  │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Análise temporal    │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Dataset tratado     │
          │   df_limpo.csv      │
          └─────────────────────┘
🧹 Tratamento e qualidade dos dados

Uma das primeiras etapas consiste na avaliação da estrutura da base, incluindo quantidade de registros, quantidade de colunas, nomes das variáveis e respectivos tipos.

Também são removidas colunas residuais cujo nome começa com Unnamed.

A variável DATA, originalmente armazenada como texto, é convertida para o tipo datetime, utilizando o formato brasileiro:

df["DATA"] = pd.to_datetime(
    df["DATA"],
    format="%d/%m/%Y",
    errors="coerce"
)

Registros que não possam ser convertidos corretamente são transformados em NaT, permitindo posterior identificação e tratamento.

🔎 Tratamento de valores ausentes

A variável PR_CAT, responsável pela categoria do produto, apresenta registros classificados como #N/D e valores nulos.

Esses registros são convertidos para:

Sem Categoria

A estratégia preserva a informação da venda sem atribuir artificialmente uma categoria ao produto.

df["PR_CAT"] = df["PR_CAT"].replace(
    "#N/D",
    "Sem Categoria"
)

df["PR_CAT"] = df["PR_CAT"].fillna(
    "Sem Categoria"
)
♻️ Tratamento de duplicidades

O projeto também verifica a existência de registros duplicados.

Como a duplicação ocorre em registros integralmente iguais, esses registros são removidos:

df = df.drop_duplicates()

Antes da remoção, o script registra a quantidade de linhas existentes para permitir a mensuração do impacto do tratamento.

🧾 Validação das compras

Uma etapa importante da análise é a validação da variável CO_ID.

O identificador representa a compra/transação e pode estar associado a mais de um item.

Por isso, o projeto diferencia:

linhas da base → itens comprados;
CO_ID distintos → compras únicas.

A análise utiliza:

df["CO_ID"].nunique()

e:

df.groupby("CO_ID").size()

Essa abordagem evita interpretar cada linha como uma compra independente quando uma mesma transação contém múltiplos produtos.

📊 Estatística descritiva

O projeto realiza uma análise estatística da variável CL_FHL, relacionada à quantidade de filhos dos clientes.

São calculadas as seguintes métricas:

média;
mediana;
desvio padrão;
moda;
valor mínimo;
valor máximo;
quantidade de observações;
quartis.

Exemplo:

media = df["CL_FHL"].mean()
mediana = df["CL_FHL"].median()
desvio_padrao = df["CL_FHL"].std()
moda = df["CL_FHL"].mode()[0]

Essa etapa permite compreender a distribuição da variável e identificar suas principais características estatísticas.

🛒 Análise por categoria

Uma das análises realizadas identifica a quantidade de itens vendidos por categoria:

itens_por_categoria = (
    df.groupby("PR_CAT")
      .size()
      .sort_values(ascending=False)
)

A análise permite compreender a composição do mix de produtos comercializados.

Entre os resultados obtidos no próprio script, ALIMENTOS representa aproximadamente 52% dos itens, enquanto HIGIENE representa aproximadamente 19%.

👥 Análise por gênero

O projeto também calcula a quantidade de compras únicas por gênero:

compras_por_genero = (
    df.groupby("CL_GENERO")["CO_ID"]
      .nunique()
      .sort_values(ascending=False)
)

Além disso, é construída uma tabela dinâmica cruzando:

Categoria × Gênero

por meio de pivot_table.

pivot_categoria_genero = pd.pivot_table(
    df,
    index="PR_CAT",
    columns="CL_GENERO",
    values="CO_ID",
    aggfunc="count",
    fill_value=0
)

Essa estrutura possibilita analisar a distribuição dos itens entre os gêneros dentro de cada categoria.

📈 Análise de participação percentual

Além das contagens absolutas, o projeto calcula indicadores relativos.

Participação das categorias
pct_categoria_total = (
    itens_por_categoria /
    itens_por_categoria.sum() * 100
).round(2)
Participação dos gêneros
pct_genero_total = (
    compras_por_genero /
    compras_por_genero.sum() * 100
).round(2)
Distribuição de gênero dentro de cada categoria
pct_dentro_categoria = (
    pivot_categoria_genero
    .div(pivot_categoria_genero.sum(axis=1), axis=0)
    * 100
)

Esses indicadores complementam as contagens e permitem analisar a representatividade relativa de cada grupo.

📅 Análise temporal

O projeto também incorpora uma dimensão temporal à análise.

A partir da variável DATA, são criadas:

DIA_SEMANA;
SEMANA_DO_ANO.
df["DIA_SEMANA"] = (
    df["DATA"]
    .dt.day_name()
    .map(dias_pt)
)

df["SEMANA_DO_ANO"] = (
    df["DATA"]
    .dt.isocalendar()
    .week
)

Com essas variáveis, são analisadas:

quantidade de compras por dia da semana;
quantidade de compras por semana;
crescimento percentual semana a semana;
dia com maior volume de compras;
semana com maior quantidade de transações.




💡 Principais insights

A análise realizada no projeto identificou alguns pontos relevantes:

🛍️ Mix de produtos

A categoria ALIMENTOS concentra aproximadamente 52% dos itens registrados, seguida por HIGIENE, com aproximadamente 19%.

👥 Distribuição por gênero

A distribuição entre homens e mulheres apresenta diferenças relativamente pequenas na maior parte das categorias analisadas.

🐾 Categorias PET e BEBIDAS

O script identifica uma participação masculina ligeiramente superior à média masculina geral nessas duas categorias.

Essa diferença é pequena e deve ser interpretada como uma característica descritiva da amostra analisada, não como evidência de causalidade ou comportamento geral da população.

🏷️ Dados sem categoria

Os registros classificados como Sem Categoria representam aproximadamente 0,44% dos itens, segundo a análise realizada no próprio projeto.

🧾 Estrutura das compras

A validação de CO_ID demonstra que uma mesma compra pode conter múltiplos itens. Portanto, análises de compras devem considerar o identificador da transação quando o objetivo for mensurar tickets/compras, em vez de simplesmente contar linhas.

💰 Limitação da base

A base analisada não apresenta uma variável monetária de preço ou receita.

Consequentemente, a análise está concentrada principalmente em volume de itens e quantidade de compras, não sendo possível calcular diretamente:

faturamento;
ticket médio;
receita por categoria;
margem;
contribuição financeira por produto.

Uma possível evolução seria integrar uma tabela de preços utilizando PR_ID.

🚀 Como executar
1. Clone o repositório
git clone https://github.com/meninodeminas/MiniProjeto_PedroSouza_Analise_de_Dados_T6.git
2. Acesse a pasta
cd MiniProjeto_PedroSouza_Analise_de_Dados_T6
3. Crie um ambiente virtual
python -m venv .venv
4. Ative o ambiente virtual
Windows
.venv\Scripts\activate
Linux/macOS
source .venv/bin/activate
5. Instale as dependências
pip install pandas numpy matplotlib kagglehub
6. Execute o projeto
python Mini_Projeto_Varejo.py

O script realiza o processamento da base e gera o arquivo:

df_limpo.csv

com os dados após as etapas de tratamento.

📚 Conceitos aplicados

Este projeto demonstra conhecimentos práticos em:

Python para análise de dados

Pandas

NumPy

Matplotlib

Importação de dados

Data Cleaning

Tratamento de valores ausentes

Tratamento de duplicidades

Conversão de tipos

Manipulação de datas

Estatística descritiva

groupby

pivot_table

Análise percentual

Análise temporal

Validação de dados

Exportação de datasets

🔮 Possíveis evoluções

Como próximos passos para transformar o projeto em uma análise mais próxima de um cenário profissional, podem ser incorporadas:

Análise de faturamento, mediante integração com dados de preço;
Ticket médio por cliente e categoria;
Análise de frequência de compra;
Segmentação de clientes;
Análise de sazonalidade;
Visualizações exploratórias com Seaborn ou Plotly;
Dashboard interativo em Power BI;
Automatização do pipeline de tratamento;
Validações automatizadas da qualidade dos dados;
Documentação de um dicionário de dados.
🎓 Contexto acadêmico

Projeto: Mini-Projeto Avaliativo — Módulo 1 — Semana 07
Curso: Análise de Dados com Python
Autor: Pedro Henrique de Paula Souza

O projeto possui finalidade acadêmica e demonstra a aplicação prática de conceitos fundamentais de análise e tratamento de dados utilizando Python.

👨‍💻 Autor

Pedro Henrique de Paula Souza

🔗 GitHub: @meninodeminas
