# 📊 Análise de Dados de Varejo com Python
Mini-Projeto Avaliativo - Módulo 1 - Semana 07 - Curso de Análise de Dados com Python

Projeto de análise exploratória e preparação de dados de varejo desenvolvido em Python, com foco em ETL, Data Cleaning, validação de dados, estatística descritiva e análise de transações.

O projeto parte de uma base com 830.000 registros e 14 colunas, realiza o tratamento de inconsistências estruturais e categóricas, remove duplicidades, valida a relação entre itens e compras por meio do identificador CO_ID e produz um dataset tratado com 733.447 registros e 10 colunas.

A análise também investiga o perfil dos clientes, composição do mix de produtos, distribuição por gênero e comportamento das transações ao longo do tempo.

## 📌 1. Sobre o Projeto
O objetivo é transformar uma base transacional de varejo em um conjunto de dados mais consistente, estruturado e adequado para análises posteriores.

O projeto contempla as seguintes atividades:
· ingestão da base de dados;
· exploração inicial da estrutura;
· identificação e remoção de colunas residuais;
· conversão e validação de datas;
· tratamento de categorias sem classificação;
· identificação e remoção de registros duplicados;
· validação da unidade de análise por meio de CO_ID;
· estatística descritiva da quantidade de filhos dos clientes;
· análise do mix de produtos;
· análise de compras por gênero;
· análise percentual;
· análise temporal das transações;
· exportação do dataset tratado.

O fluxo implementado no projeto segue a lógica de Extração → Transformação → Validação → Análise → Exportação, aproximando o exercício acadêmico de um fluxo básico de ETL aplicado a dados de negócio.

## 🧰 2. Tecnologias Utilizadas
Aqui está uma tabela com as tecnologias e suas aplicações:

| Tecnologia: | Aplicação: |
|---|---|
| **Python:** | Linguagem principal utilizada no desenvolvimento. |
| **Pandas:** | Leitura, transformação, limpeza, agrupamento e análise dos dados. |
| **NumPy:** | Operações numéricas e suporte à análise. |
| **Matplotlib:** | Exploração e visualização dos dados. |
| **KaggleHub:** | Obtenção programática da base de dados disponibilizada no Kaggle. |

## 🔄 3. Etapas Realizadas
Aqui está a tabela com as etapas, atividades e resultados:

| Etapa: | Atividade: | Resultado: |
|---|---|---|
| 1 | Extração: | Base carregada com 830.000 registros. |
| 2 | Exploração Inicial: | Identificação de 14 colunas e estrutura dos dados. |
| 3 | Limpeza Estrutural: | Remoção de 4 colunas residuais. |
| 4 | Tratamento de Datas: | Conversão da coluna DATA para datetime. |
| 5 | Tratamento Categórico: | Padronização de registros #N/D. |
| 6 | Remoção de Duplicidades: | Exclusão de 96.553 registros duplicados. |
| 7 | Validação de CO_ID: | Identificação de 18.471 compras únicas. |
| 8 | Estatística Descritiva: | Análise da variável CL_FHL. |
| 9 | Agrupamentos: | Análises por categoria e gênero. |
| 10 | Tabela Dinâmica: | Cruzamento entre categoria e gênero. |
| 11 | Análise Temporal: | Avaliação por dia da semana e semana do ano. |
| 12 | Exportação: | Geração do arquivo df_limpo.csv. |

As etapas de transformação, limpeza, validação de CO_ID, estatística descritiva, agrupamentos e exportação estão implementadas no script do projeto.

## 🧹 4. Decisões de Limpeza
Aqui está a tabela com os problemas identificados e tratamentos realizados:

| Problema Identificado: | Tratamento Realizado: | Justificativa: |
|---|---|---|
| 4 colunas Unnamed. | Remoção das colunas. | Eram colunas residuais sem conteúdo analítico. |
| DATA armazenada como texto. | Conversão para datetime utilizando %d/%m/%Y. | Permitir análises temporais e operações específicas de datas. |
| Datas inválidas. | Conversão com errors="coerce". | Permitir identificar eventuais registros impossíveis de converter sem interromper o processamento. |
| PR_CAT = #N/D. | Substituição por Sem Categoria. | Preservar a venda sem atribuir artificialmente uma categoria. |
| Valores nulos em PR_CAT. | Preenchimento com Sem Categoria. | Preservar o registro e explicitar a ausência de classificação. |
| Registros duplicados. | drop_duplicates(). | Remover repetições integralmente idênticas. |
| Múltiplas linhas para o mesmo CO_ID. | Não remover. | Uma compra pode conter múltiplos itens; portanto, linhas não representam necessariamente compras distintas. |
| Ausência de variável monetária. | Não foi realizada imputação. | A base não apresenta preço/receita; criar valores monetários artificialmente introduziria informação não observada. |

A lógica de tratamento de PR_CAT, remoção de duplicidades e validação de CO_ID segue a implementação do script do projeto.

## 📈 5. Resultado da Limpeza
Aqui está a tabela com os indicadores antes e depois da limpeza:

| Indicador: | Antes da Limpeza: | Depois da Limpeza: | Variação: |
|---|---|---|---|
| Registros. | 830.000 | 733.447 | -96.553 (-11,63%) |
| Colunas. | 14 | 10 | -4 (-28,57%) |
| Colunas Unnamed. | 4 | 0 | -4 |
| Duplicidades Exatas. | 96.553 | 0 | -96.553 |
| Datas Inválidas. | 0 | 0 | Sem alteração. |
| #N/D em PR_CAT. | 3.650 | 0 | -3.650 |
| Sem Categoria. | 0 | 3.228 | Categoria preservada após remoção de duplicidades. |
| Compras Únicas (CO_ID). | 18.471 | 18.471 | Mantidas. |

**📌 Impacto da Limpeza:**

A limpeza eliminou 96.553 registros duplicados, correspondentes a aproximadamente 11,63% da base original.

Além disso, as quatro colunas residuais foram eliminadas, reduzindo a estrutura de 14 para 10 colunas.

A transformação de #N/D para Sem Categoria preservou a informação das transações, evitando a exclusão de registros apenas porque a classificação do produto estava ausente.

## 🛒 6. Regra de negócio — CO_ID

**Conceito:**
O CO_ID representa a identificação da compra/transação.

A principal regra de negócio identificada é:

*Uma linha da base representa um item comprado; um CO_ID representa uma compra, que pode conter um ou vários itens.*

Portanto:

*Quantidade de linhas ≠ quantidade de compras.*

Para calcular o número de compras, deve-se utilizar:

df["CO_ID"].nunique()

Enquanto a quantidade de itens associados a cada compra pode ser obtida por:

df.groupby("CO_ID").size()

Essa distinção é fundamental para evitar que uma compra com vários produtos seja contabilizada como várias compras. A própria implementação do projeto utiliza essa lógica para validar CO_ID.

**Indicadores de CO_ID:**
| Indicador: | Resultado: |
|---|---:|
| Registros após Limpeza: | 733.447 |
| Compras únicas (CO_ID): | 18.471 |
| Itens médios por compra: | 39,71 |
| Mediana de itens por compra: | 41 |
| Mínimo de itens em uma compra: | 1 |
| Máximo de itens em uma compra: | 81 |
| Compras com apenas 1 item: | 207 |
| Compras com múltiplos itens: | 18.264 |
| % de compras com múltiplos itens: | 98,88% |
| % de compras com apenas 1 item: | 1,12% |

**📌 Interpretação:**

Os dados demonstram que **18.264 das 18.471 compras**, ou aproximadamente **98,88%**, possuem mais de um item.

Esse resultado reforça que a unidade correta para análises de **transações/tickets** é o CO_ID, enquanto a unidade correta para análises de itens vendidos é a linha do dataset.

## 📊 7. Estatística Descritiva — Número de Filhos
A variável analisada é CL_FHL, correspondente à quantidade de filhos.
| Estatística: | Resultado: |
|---|---:|
| Quantidade de observações: | 733.447 |
| Média: | 1,15 |
| Mediana: | 0 |
| Moda: | 0 |
| Desvio Padrão: | 1,42 |
| Mínimo: | 0 |
| 1º Quartil — 25%: | 0 |
| 2º Quartil — 50%: | 0 |
| 3º Quartil — 75%: | 2 |
| Máximo: | 4 |

**📌 Interpretação:**

A média de 1,15 filho é superior à mediana de 0, indicando uma **distribuição assimétrica**.

A moda igual a **0** demonstra que esse **é o número de filhos mais frequente na base**.

O terceiro quartil igual a 2 significa que **75% das observações possuem até 2 filhos**, enquanto o **máximo observado é de 4 filhos**.

## 💡 8. Principais Insights
📊 A categoria **ALIMENTOS concentra 384.197 itens**, representando **52,38% de todos os registros após a limpeza**. HIGIENE aparece em segundo lugar, com 137.702 itens (18,77%), enquanto LIMPEZA representa 128.632 itens (17,54%).

📈 **Somadas, as categorias ALIMENTOS, HIGIENE e LIMPEZA representam aproximadamente 88,69% de todos os itens**, demonstrando forte concentração do mix nesses três grupos.

🏷️ **A categoria Sem Categoria representa** apenas 3.228 registros, ou **0,44% da base tratada**, indicando que a ausência de classificação possui baixo peso relativo no conjunto analisado.

🛒 **Em relação às compras, foram identificados 18.471 CO_ID distintos**. Como 98,88% das compras possuem múltiplos itens, utilizar a contagem de linhas como proxy para quantidade de compras produziria uma interpretação incorreta do volume transacional.

👥 **Na distribuição por gênero, foram identificadas 9.615 compras únicas associadas ao gênero F (52,05%) e 8.856 ao gênero M (47,95%)**, indicando uma diferença de aproximadamente 4,10 pontos percentuais.

👩‍👨 Entre as categorias, **a participação feminina varia de 51,65% a 53,13%, enquanto a participação masculina varia de 46,87% a 48,35%**. A maior participação masculina ocorre em BEBIDAS (48,35%), seguida por PET (48,14%).

👶 **A análise de CL_FHL mostra que 0 filhos é simultaneamente a moda e a mediana, enquanto a média é de 1,15**, evidenciando concentração de observações em valores baixos e uma distribuição com dispersão relevante.

## 🔄 9. Reflexão sobre o Fluxo ETL e Aplicação
O projeto demonstra, em escala acadêmica, as principais etapas de um processo ETL — Extract, Transform, Load.

| Etapa: | Descrição: |
|---|---|
| **Extract** *ou Extração* | A base é obtida programaticamente e carregada em um DataFrame utilizando Pandas. |
| **Transform** *ou Transformação* | É realizada a transformação dos dados por meio de: remoção de colunas residuais; conversão de tipos; tratamento de categorias; identificação de duplicidades; validação de identificadores; criação de indicadores; agrupamentos; estatística descritiva; criação de variáveis temporais. |
| **Load** *ou — Carga* | Após o tratamento, o conjunto de dados é exportado para df_limpo.csv, criando uma camada de dados preparada para análises posteriores. |

**Aplicação Profissional:**

Em um cenário empresarial, esse fluxo poderia ser ampliado para:

Aqui está o fluxograma em formato de tabela:

| # | Etapa: | Descrição: |
|---|---|---|---|
| 1 | Fonte de Dados: | Origem dos dados a serem analisados. |
| 2 | Extração Automatizada: | Obtenção programática dos dados. |
| 3 | Staging (Dados Brutos): | Armazenamento temporário dos dados brutos. |
| 4 | Validação da Qualidade: | Verificação da integridade e consistência. |
| 5 | Transformação e Limpeza: | Tratamento, limpeza e preparação dos dados. |
| 6 | Dados Tratados: | Dados prontos para análise. |
| 7 | Data Warehouse / Data Lake: | Armazenamento centralizado de dados. |
| 8 | Power BI / Dashboard / Analytics: | Visualização e análise exploratória. |
| 9 | Tomada de Decisão: | Insights e ações estratégicas. |

O principal aprendizado do projeto é que a **qualidade da análise depende diretamente da qualidade e da correta interpretação dos dados**. Antes de calcular indicadores, é necessário compreender a unidade de análise, identificar duplicidades, tratar inconsistências e validar as regras de negócio.

Uma evolução natural seria incorporar validações automatizadas de qualidade, testes de dados, dicionário de dados, pipeline agendado e integração com ferramentas de BI.

## 🚀 10. Como Executar:
| Etapa: | Atividade: | Comando: |
|---|---|---|
| 1 | Clonar o Repositório: | `git clone https://github.com/meninodeminas/MiniProjeto_PedroSouza_Analise_de_Dados_T6.git` |
| 2 | Acessar a Pasta: | `cd MiniProjeto_PedroSouza_Analise_de_Dados_T6` |
| 3 | Criar um Ambiente Virtual: | `python -m venv .venv` |
| 4 | Ativar o Ambiente Virtual (Windows): | `.venv\Scripts\activate` |
| 4 | Ativar o Ambiente Virtual (Linux/macOS): | `source .venv/bin/activate` |
| 5 | Instalar as Dependências: | `pip install pandas numpy matplotlib kagglehub` |
| 6 | Executar o Projeto: | `python Mini_Projeto_Varejo.py` |

Esses comandos estão alinhados ao fluxo de execução documentado no repositório.

*Observação: o script atual utiliza kagglehub para realizar a obtenção da base. Caso seja utilizada a base CSV local, o código pode ser adaptado para ler diretamente o arquivo com pd.read_csv().*

## 📁 11. Estrutura do Projeto

· 📄 BaseVarejo.csv: Base de dados original.

· 📄 df_limpo.csv: Base após tratamento e limpeza.

· 🐍 Mini_Projeto_Varejo.py: Script de análise, transformação e tratamento.

· 📄 README.md: Documentação do projeto.

· 📄 .gitignore: Arquivos e diretórios ignorados pelo Git.

A estrutura acima corresponde aos principais arquivos atualmente presentes no repositório.

## 🎯 Conclusão
O projeto demonstra a aplicação prática de conceitos fundamentais de Análise de Dados com Python, especialmente em ETL, Data Cleaning, Validação de Dados, Estatística Descritiva e Análise Exploratória.

O processo **transformou uma base de 830.000 registros em um dataset tratado de 733.447 registros, removendo 96.553 duplicidades e 4 colunas residuais, além de padronizar a classificação de produtos sem categoria**.

A análise também **evidenciou que o CO_ID é essencial para diferenciar item vendido de compra realizada**, uma vez que quase 99% das transações possuem múltiplos itens.

Como evolução, **o projeto pode incorporar dados financeiros, segmentação de clientes, indicadores de ticket médio, dashboards, testes automatizados de qualidade e um pipeline ETL completo**.

## 👨‍💻 Autor

Pedro Henrique de Paula Souza

🔗 GitHub: @meninodeminas

📚 Projeto desenvolvido para fins acadêmicos no Curso de Análise de Dados com Python.
