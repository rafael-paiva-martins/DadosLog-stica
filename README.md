# DadosLogística
Este mini-projeto tem como objetivo desenvolver e documentar um conjunto de dashboards logísticos no Power BI, explorando a performance operacional por meio de KPIs estratégicos de entrega. O foco é avaliar pontualidade, eficiência de equipes e desempenho de vendedores, com base em dados de entregas reais.

📁 Etapas da Análise
🔹 Carregamento e Verificação dos Dados

Após o carregamento do dataset no Power BI, foi realizada uma análise inicial para garantir:

Reconhecimento correto da linha de cabeçalho;

Tipagem adequada das colunas, especialmente as datas;

Ausência de inconsistências que possam comprometer os visuais.

Essa verificação é essencial para que os gráficos e indicadores representem os dados corretamente.

📊 KPIs e Visualizações Criadas
1️⃣ Total de Entregas no Prazo por Canal de Entrega

Visual: Gráfico de área

Eixo X: Canal de entrega

Eixo Y: Total de entregas

Métrica: COUNT(ID_Pedido) (não SUM)

Filtro aplicado: Status_Entrega = "No Prazo"

💡 O Power BI define automaticamente “Sum” ao adicionar campos numéricos. O analista deve substituir por “Count” para obter a contagem correta de pedidos.

2️⃣ Percentual de Entregas Antecipadas por Equipe

Visual recomendado: Gráfico de barras horizontais (clustered bar chart)

Eixo X: Count(ID_Pedido) → Show value as percentage

Eixo Y: Equipe_Entrega

💬 Evitar gráfico de pizza quando houver mais de 5 categorias, pois o excesso de fatias prejudica a legibilidade.

3️⃣ Total de Entregas por Mês

Campo de tempo: Data_Entrega_Realizada

Visual: Gráfico de linhas

Eixo X: Mês (removendo agregações de trimestre, semana, dia)

Eixo Y: Contagem de Status_Entrega

🧠 Quando o mesmo campo é usado em múltiplos gráficos com filtros diferentes, é recomendável criar uma medida central para facilitar futuras alterações.

🔧 Medida criada:
TotalEntregas = COUNTROWS(Logística)


Assim, qualquer alteração na definição de “Total de Entregas” pode ser feita diretamente na medida, e se refletirá em todos os visuais.

4️⃣ Total de Entregas por ID_Vendedor (Top 5)

Legenda: ID_Vendedor

Valores: [TotalEntregas]

Filtro: N Superior (Top 5) com base na medida [TotalEntregas]

📉 O gráfico de rosca não é ideal aqui, pois as diferenças entre vendedores são pequenas. Optou-se por representar os dados em formato de tabela.

5️⃣ Total de Entregas em Atraso por Cidade

Filtro: Status_Entrega = "Em Atraso"

Visual: Tabela

Campo: ID_Cidade

Ajuste: Definir campo como “Não Resumir” para evitar somatórios automáticos.

Critério adicional: Exibir apenas cidades com mais de 300 entregas atrasadas (ajustável conforme necessidade da área de negócios).

📋 Quando há grande volume de dados, a tabela é mais apropriada do que visuais complexos.

⭐ Classificação com Star Rating

Menu: Modeling → New Quick Measure → Calculations / Text / Star Rating

Valor base: [TotalEntregas]

Número de estrelas: 5

Menor valor: 1500

Maior valor: 2500

🔆 Esse recurso converte valores numéricos em classificações visuais, permitindo uma leitura imediata de performance.

🧮 Expressão DAX: Entregas no Prazo

Para agrupar entregas antecipadas e no prazo, criamos a medida:

TotalEntregasPrazo =
CALCULATE(
    [TotalEntregas],
    FILTER(
        Logistica,
        Logistica[Status_Entrega] = "Antecipado"
        || Logistica[Status_Entrega] = "No Prazo"
    )
)

🧩 Boas Práticas Aplicadas

Contagens sempre por ID_Pedido, evitando somatórios incorretos.

Criação de medidas reutilizáveis para facilitar manutenção.

Escolha de visuais guiada por clareza e propósito analítico.

Uso de filtros direcionados em cada gráfico para evitar redundâncias.

🛠️ Ferramentas Utilizadas

Power BI Desktop

Power Query

DAX

Modelagem de Medidas Rápidas (Quick Measures)

🚀 Como Visualizar

Baixe o arquivo .pbix do projeto

Abra no Power BI Desktop

Navegue entre as páginas para visualizar os KPIs e filtros aplicados

🤝 Conecte-se comigo no [LinkedIn](https://www.linkedin.com/in/rafael-paiva-martins) para acompanhar outros projetos de Business Intelligence e compartilhar aprendizados sobre modelagem, DAX e visualização de dados.


🚚 Logistics KPI Analysis

This mini-project aims to develop and document a set of logistics dashboards in Power BI, focusing on key performance indicators (KPIs) for delivery operations.
The goal is to evaluate on-time delivery rates, team efficiency, and seller performance based on real delivery data.

📁 Data Preparation and Initial Review
🔹 Data Loading and Validation

After importing the dataset into Power BI, an initial review was carried out to ensure:

The header row was correctly identified;

Columns had the appropriate data types, especially date fields;

No inconsistencies would affect visuals or measures.

This validation step ensures accurate and reliable visualizations.

📊 KPIs and Visuals
1️⃣ Total On-Time Deliveries by Delivery Channel

Visual: Area chart

X-axis: Delivery Channel

Y-axis: Total Deliveries

Metric: COUNT(ID_Pedido) (not SUM)

Filter applied: Status_Entrega = "On Time"

💡 Power BI automatically uses “Sum” for numeric fields. The analyst must manually change it to “Count” to reflect the actual number of deliveries.

2️⃣ Percentage of Early Deliveries by Team

Recommended Visual: Horizontal clustered bar chart

X-axis: Count(ID_Pedido) → Show value as percentage

Y-axis: Delivery_Team

💬 Avoid pie charts with more than five categories, as they become cluttered and harder to read.

3️⃣ Total Deliveries per Month

Time Field: Delivery_Date_Completed

Visual: Line chart

X-axis: Month (remove automatic grouping by quarter, week, or day)

Y-axis: Count of Delivery_Status

🧠 When using the same field across multiple visuals with different filters, it’s best to create a central measure for consistency and easier maintenance.

🔧 Created Measure:
TotalDeliveries = COUNTROWS(Logística)


Any future change to the definition of “Total Deliveries” can be made directly in the measure, automatically updating all visuals.

4️⃣ Total Deliveries by Seller (Top 5)

Legend: Seller_ID

Values: [TotalDeliveries]

Filter: Top N (Top 5) by [TotalDeliveries]

📉 The donut chart was replaced by a table since small differences between sellers make it difficult to interpret using proportional visuals.

5️⃣ Total Late Deliveries by City

Filter: Delivery_Status = "Late"

Visual: Table

Field: City_ID

Adjustment: Set field to “Don’t Summarize” to avoid unwanted aggregation.

Business rule: Display only cities with more than 300 late deliveries (this threshold may vary based on business needs).

📋 When handling large data volumes, tables are often more practical than complex visuals.

⭐ Star Rating Visualization

Menu: Modeling → New Quick Measure → Calculations / Text / Star Rating

Base Value: [TotalDeliveries]

Number of Stars: 5

Minimum Value: 1500

Maximum Value: 2500

🔆 This feature converts numeric values into star-based ratings, allowing instant visual comparison of performance.

🧮 DAX Expression: On-Time Deliveries

Deliveries marked as early or on time are grouped under one measure:

TotalOnTimeDeliveries =
CALCULATE(
    [TotalDeliveries],
    FILTER(
        Logistica,
        Logistica[Delivery_Status] = "Early"
        || Logistica[Delivery_Status] = "On Time"
    )
)

🧩 Best Practices Applied

Always use count of IDs instead of sums for categorical metrics.

Build reusable measures to simplify updates and ensure consistency.

Choose visuals based on clarity and analytical purpose.

Apply specific filters per visual to maintain focus and avoid redundancy.

🛠️ Tools Used

Power BI Desktop

Power Query

DAX

Quick Measures

🚀 How to View the Dashboard

Download the .pbix file from this repository.

Open it using Power BI Desktop.

Navigate through the pages to explore KPIs and applied filters.

🤝 Connect

Connect with me on [LinkedIn](https://www.linkedin.com/in/rafael-paiva-martins) to explore more Business Intelligence projects and share insights about data modeling, DAX, and visualization techniques.
