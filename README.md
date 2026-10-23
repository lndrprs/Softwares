----

<div align="center">
<h6>
░██████╗░█████╗░███████╗████████╗░██╗░░░░░░░██╗░█████╗░██████╗░███████╗░██████╗
██╔════╝██╔══██╗██╔════╝╚══██╔══╝░██║░░██╗░░██║██╔══██╗██╔══██╗██╔════╝██╔════╝
╚█████╗░██║░░██║█████╗░░░░░██║░░░░╚██╗████╗██╔╝███████║██████╔╝█████╗░░╚█████╗░
░╚═══██╗██║░░██║██╔══╝░░░░░██║░░░░░████╔═████║░██╔══██║██╔══██╗██╔══╝░░░╚═══██╗
██████╔╝╚█████╔╝██║░░░░░░░░██║░░░░░╚██╔╝░╚██╔╝░██║░░██║██║░░██║███████╗██████╔╝
╚═════╝░░╚════╝░╚═╝░░░░░░░░╚═╝░░░░░░╚═╝░░░╚═╝░░╚═╝░░╚═╝╚═╝░░╚═╝╚══════╝╚═════╝░
</div>
</h6>

----

<details>
  <summary><b> 1. Observabilidade </b></summary>
  <div align="left">

<br>

<details>
  <summary><b> 1.1. Prometheus - Referência: <a href="https://prometheus.io/docs/introduction/overview/"> Documentação Técnica</a></b></summary>
  <div align="left">
    
<br>
    
  <details>
  <summary> 1.1.1. Glossário </summary>
  <div align="Center">

<br>

| Termo | Descrição |
|-------|-----------|
| Alerting Rule | Regra baseada em PromQL que dispara um alerta quando uma condição é satisfeita. | 
| Alertmanager | Componente separado responsável por gerenciar alertas enviados pelo Prometheus. |
| Counter | Métrica cumulativa que só aumenta, para contagem de eventos. |
| Exporter | Software auxiliar que expõe métricas de sistemas que não suportam nativamente o formato prometheus. (Node_exportar, mysql_exporter). |
| Federação | Recurso que permite um servidor Prometheus coletar subconjunto de métricas de outro servidor Prometheus. | 
| Gauge | Métrica que pode subir ou descer livremente. |
| Histogram | mètrica que amostra observações e as agrupa em buckets configuráveis. | 
| Instant Vector | Conjunto de Séries Temporais Contendo um único valor para cada série em um dado momento. | 
| Label | Par Chave-Valor que permite dimensionar uma métrica, diferenciando séries temporais dentro da mesma métrica. |
| Métrica | Medida numérica de algum aspecto do sistema. |
| Prometheus | Sistema de monitoramento e alerta, de código aberto. Coleta e Armazena Métricas como Séries Temporais. |
| PromQL | Linguagem de Consulta Funciona usada para selecionar e agregar dados. | 
| Pushgateway | Componente intermediário que permite que jobs de curta duração (batch), enviem métricas via Push. | 
| Range Vector | Conjunto de Séries Temporais contendo intervalo de valores ao longo do tempo. |
| Recording Rule | Regra que pré-computa expressoes PromQL frequentes ou custosas, e salva o resultado como uma nova série temporal. | 
| Remote Write / Remote Read | Recursos que permitem enviar ou ler dados de armazenamentos externos (Thanos, Cortex, Mimir). |
| Retention | Período de tempo pelo qual os dados são mantidos localmente antes de serem descartados. | 
| Sample | Único ponto de dado dentro de uma série temporal. Composto por um valor float64 e um timestamp em milissegundos. |
| Scrape | Processo de busca de métricas, ativamente de um endpoint. (Pull) |
| Service Discovery | Mecanismo para descobrir Targets automaticamente. | 
| Silence | Configuração Temporária no Alertmanager para suprimir notificações de determinados alertas. |
| Summary | Similar ao Histogram, mas calcula quantis diretamente no cliente ao longo de uma janela deslizante. | 
| Target | Endpoint monitorado pelo Prometheus. |
| Time Series | Fluxo de valores numéricos associados a um timestamp, identificado por um nome de métrica e um conjunto de chaves-valor (labels). |
| Time Series Data Base (TSDB) | Banco de dados de séries temporais embutido no Prometheus. |
| Write Ahead Log (WAL) | Log usado pelo TSDB para garantir durabilidade dos dados antes de serem persistidos definitivamente. |

<br>

  </div>
  </details>        

</div>
</details>

----

<details>
  <summary><b> 1.2. Dynatrace - Referência: <a href="https://docs.dynatrace.com/docs"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 1.2.1. Glossário </summary>
  <div align="Center">

<br>  

| Termo | Descrição |
|-------|-----------|
| ActiveGate | Componente Proxy / Gateway que gerencia comunicação entre OneAgents. |
| API Token | Credencial usada para autenticar chamadas à API REST do Dynatrace, utilizada em integrações e automações. |
| Application Performance Monitoring | Monitoramento focado em desempenho de aplicaçãos, medindo tempo de resposta, erros e throughput. |
| Application Security | Módulo do Dynatrace para detecção de vulnerabilidades em tempo de execução (runtime). |
| Baseline | Padrão de comportamento "normal" de uma métrica, aprendido automaticamente pela Davis AI ao longo do tempo. |
| Business Analytics | Transformação de dados de negócio capturados em transações, em métricas e dashboards de negócio. |
| Cloud Automation | Recurso que permite orquestrar pipelines de CD com validação automática de qualidade e desempenho (SLOs), usando dados do Dynatrace. |
| Davis AI | Motor de I.A causal do Dyna, usado para detecção automática de anomalias e identifcação de causa raiz. |
| Davis Score | Pontuação de severidade atribuída pela Davis AI a um problema. |
| Dynatrace | Plataforma de observabilidade e segurança, que unifica monitoramento de infra, aplicações, UX e segurança, usando IA para detecção automática de causas raiz. |
| Dynatrace Hub | Catálogo de extensões, integrações e aplicações que podem ser adicionadas ao ambiente Dynatrace. |
| Dynatrace Operator | Operador do Kubernetes usado para implantar e gerenciar componentes do Dynatrace (OneAgent, ActiveGate), em clusters Kubernetes. |
| Dynatrace Query Language (DQL) | Linguagem de consulta usada para analisar dados armazenados no Grail. | 
| Entity | Qualquer componente monitorado e representado no Smartscape. |
| Extension | Pacote de integração que permite o Dynatrace coletar dados de tecnologias adicionais não suportadas nativamente. |
| Grail | Mecanismo de armazenamento e análise de dados (Data Lakehouse) do Dynatrace. |
| Kubernetes Monitoring | Módulo do Dynatrace dedicado ao monitoramento de Clusters Kubernetes, incluindo Pods, Namespaces, Workloads, e Eventos do Cluster. |
| Metric Dimension | Atributo que qualifica uma métrica, permitindo segmentação (Equivalente a labels em outros sistemas). |
| Metric Expiration | Regras de retenção que definem por quanto tempo os dados de métricas ficam disponíveis para consulta. | 
| OneAgent | Agente de software instalado em hosts que coleta dados automaticamente, sem precisar de insturmentação. |
| PurePath | Tecnologia de Rastreamento Distribuído. Caputra o caminho completo de uma transação - do clique ao banco de dados. |
| Real User Monitoring | Monitoramento de Usuários Reais, capturando dados de experiência real de navegação. |
| Root Cause Analysis (RCA) | Processo automatizado de identificação de causa raiz de um problema, feito pela Davis AI. |
| Runtime Vulnerability Analytics | Análise contínua de vulnerabilidades em aplicações rodando em produção. |
| Session Replay | Reprodução visual da sessão de um usuário real para diagnóstico de problemas de UX. | 
| Smartscape | Mapa topológico dinâmico e em tempo real que representa dependências entre hosts, processos, serviços e aplicações. |
| Synthetic Monitoring | Simulação de transações e jornadas de usuário a partir de locais predefinidos. |
| Workflow | Automação configurável do Dynatrace que executa ações (notificações, remediações, integrações), em resposta a eventos ou problemas. |

<br>

  </div>
  </details>        

</div>
</details>

----

<details>
  <summary><b> 1.3. Splunk - Referência: <a href="https://docs.splunk.com/Documentation"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 1.3.1. Glossário </summary>
  <div align="Center">

<br>  

| Termo | Descrição |
|-------|-----------|
| Alert | Ação Automatizada disparada quando os resultados de uma pesquisa salva atendem a uma condição definida, podendo enviar e-mail, executar script ou abrir um ticket. | 
| App | Pacote de configurações, dashboards, pesquisas e visualizações voltado a um caso de uso específico. |
| Bucket | DIretório onde o Splunk armazena os dados indexados de um determinado período de tempo, podendo estar nos estados: Hot, Warm, Cold, Frozen ou Thawed. |
| Cluster | Conjunto de instâncias Splunk (Indexers ou Search Heads), trabalhando juntas para prover alta disponibilidade e escalabilidade. |
| Data Model | Estrutura hierárquica de conhecimento que organiza dados em datasets relacionados, usada como Pivot para criar relatórios sem escrever SPL. |
| Dashboard | Interface visual composta por painéis que exibem resultados de pesquisas, gráficos e visualizações. |
| Deployment Server | Componente que gerencia e distribui configurações (apps), para múltiplos forwarders e instâncias Splunk. |
| Event | Um únivo registro de dado indexado pelo Splunk, geralmente correspondendo a uma linha de log com timestamp associado. |
| Event Type | Categorização de Eventos com base em critérios de pesquisa, usada para classificar e organizar dados semelhantes. |
| Field | Par chave-valor extraído de um evento, usado para pesquisa, filtragem e análise. |
| Field Extraction | Processo de identificar e extrair campos a partir do texto bruto de um evento, podendo ser automático (regex) ou definido manualmente. |
| Forwarder | Agente instalado em servidores de origem para coletar e enviar dados a um Indexer, podendo ser Universal Forwarder ou Heavy Forwarder (Com parsing). |
| Index | Repositório onde o SPlunk armazena os dados processados e indexados, permitindo pesquisas rápidas. |
| Indexer | Componente responsável por processar, indexar e armazenar os dados recebidos, tornando-os pesquisáveis. |
| Knowledge Object | Objeto criado pelo usuário para enriquecer dados, incluindo field extractions, event types, tags, lookups e data models. |
| Lookup | Recurso que permite enriquecer eventos com dados externos (Tabelas, CSV, KV Store, Scripts), com base em valores de campos correspondentes. |
| Macro | Bloco de SPL reutilizável definido uma vez e referenciado em múltiplas pesquisas, facilitando manutenção de queries complexas. | 
| Metrics Index | Tipo de Índice otimizado especificamente para armazenar dados de métricas numéricas em alta escala. |
| Machine Learning Toolkit (MLTK) | Aplicativo do Splunk que fornece algoritmos de ML para previsão, detecção de anomalias e clusterização de dados. |
| Panel | Elemento visual individual dentro de um dashboard, contendo uma tabela, gráfico ou visualização baseada em uma pesquisa. |
| Pipeline | Sequência de processamento pela qual os dados passam desde a entrada (input) até a indexação, incluindo parsing, merging e indexação. |
| Pivot | Ferramenta que permite criar relatórios e visualizações a partir de data models, sem necessidade de escrever SPL. |
| Props.conf | Arquivo de configuração que define como os dados são processados durante a ingestão (Parsing, timestamps, line breaking). |
| Report | Pesquisa salva que pode ser executada sob demanda ou agendada, e utilizada em dashboards e alertas. |
| Saved Search | Pesquisa SPL armazenada para reutilização, podendo ser agendada e servir de base para relatórios e alertas. |
| Search Head | Componente responsável por receber pesquisas do usuário, distribuí-las aos indexer e consolidar os resultados. |
| Source | Nome ou caminho de origem de um evento. |
| Sourcetype | Classificação que define o formato dos dados de um evento, determinando como ele será processado e analisado. |
| SPL (Search Processing Language) | Linguagem de pesquisa usada no Splunk para buscar, filtrar, transformar e analisar dados indexados. |
| Splunk | Plataforma de Software para busca, monitoramento, e análise de dados gerados por máquinas em tempo real. |
| Splunkbase | Repositório oficial de Apps e Add-Ons desenvolvidos pela Splunk e pela comunidade. |
| Summary Index | Índice usado para armazenar resultados pré-computados de pesquisas, melhorando desempenho de relatórios recorrentes. |
| Tag | Rótulo aplicado a um campo ou valor de campo para faciliar pesquisas e classificação de eventos relacionados. |
| Timestamp | Marca de tempo associada a cada evento, sendo essencial para ordenação e pesquisa por intervalo de tempo. |
| Transform | Operação de transformação de dados definida em transforms.conf, usada para extração de campos, mascaramento de dados ou roteamento. |
| Universal Forwarder | Versão leve do Forwarder, usada apenas para coletar e encaminhar dados brutos, sem parsing avançado. |
| KV Store | Armazenamento de dados em formato chave-valor (Baseado em MongoDB), usado por apps SPlunk para persistir dados estruturados. |

<br>

  </div>
  </details>        

</div>
</details>

----

<details>
  <summary><b> 1.4. OpenTelemetry - Referência: <a href="https://opentelemetry.io/docs/"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 1.4.1. Glossário </summary>
  <div align="Center">

<br>  

| Termo | Descrição |
|-------|-----------|
| Agent | Componente que roda junto da aplicação ou host para coleta de telemetria localmente, enviando a um coletor ou backend. |
| Aggregation Temporality | Define se os valores de uma métrica são acumulados desde o início (cumulativa) ou apenas desde a última coleta (Delta). |
| API | Interface usada para instrumentar o código. Define como criar spans, métricas e logs, mas não implementa processamento e nem a exportação dos dados. |
| Attribute | Par chave-valor que adiciona contexto a spans, métricas, logs ou recursos. | 
| Backend | Sistema que armazena, consulta e visualiza telemetria (Jaeger, Prometheus, Tempo, Datadog etc.). |
| Baggage | Conjunto de pares chave-valor propagado junto com contexto entre serviços, permmmitindo que informações estejam disponíveis em toda a cadeia de chamadas. |
| Cardinality | Número de combinações únicas de valores de atributos em uma métrica. Se muito alta, aumenta custo e degrada o backend. |
| Collector | Processo independente que recebe, processa e exporta telemetria, desacoplando as aplicações dos backends. |
| Connector | Componente do Collector que funciona como exporter de um pipeline e receiver de outro. |
| Context | Carrega valores com escopo de execução, dentro de um processo. | 
| Contrib | Repositório e distribuição do Collector com componentes mantidos pela comunidade, além dos componentes do núcleo. |
| Counter | Instrumento de métrica que acumula valores crescentes. |
| Exemplar | Amostra de trace associada a um ponto de métrica, permitindo navegar de uma métrica para um trace específico. |
| Exporter | Componente que envia telemetria à um destino, como um Collector ou Backend. |
| Extension | Componente do Collector que oferece funcionalidades auxiliares fora do pipeline de dados, como health check, autenticação e profilling. |
| Gateway | Modo de implantação do Collector em que ele funciona como ponto central que recebe dados de vários serviços ou agentes. |
| Gauge | Instrumento de métrica que registra um valor instantâneo que pode subir ou descer. Como memória ou temperatura. |
| Head-Based Sampling | Amostragem em que a decisão é tomada no início do trace, antes de se saber o resultado completo da requisição. |
| Histogram | Instrumento de métricas que registra a distribuiçao de valores em faixas (buckets), útil para latências e tamanhos de payload. |
| Instrumentation | Adição de código ou bibliotecas para que uma aplicação emita telemetria. |
| Link | Referência de um span a outro span, possivelmente de outro trace. |
| Log Record | Registro de Log no modelo de dados do OpenTelemetry, com timestamp, severidade, corpo, atributos, e ID do traace e do span. |
| Manual Instrumentation | Instrumentação feita diretamente no código com a API do OTel, para capturar lógica específica do negócio. |
| Meter | Objeto usado para criar instrumentos de métrica. |
| Meter Provider | Ponto de entrada do SDK para métricas, responsável por criar meter e configurar a coleta e a exportação. |
| Metric | Medição numérica agregada ao longo do tempo, como taxa de requisições, uso de CPU ou latência. | 
| Observability | Capacidade de entender o estado interno de um sistema a partir dos dados que ele emite. |
| OpenTelemetry | Projeto Open Source da CNCF que define APIs, SDKs, ferramentas e um protocolo padrão para gerar, coletar e exportar telemetria, sem depender do fornecedor. | 
| OTLP (OpenTelemetry Protocol) | Protocolo nativo do OTel para transmissão de traces, métricas e logs, sobre gRPC ou HTTP. |
| Pipeline | Sequência configurada no Collector que liga receiver, processors e exporters para um tipo de sinal. |
| Processor | Componente que transforma, filtra, enriquece ou agrupa telemetria antes da exportação, no SDK ou no Collector. |
| Profiles | Sinal mais recente, ainda em evolução, para dados de profiling contínuo (Como uso de CPU por função). |
| Propagator | Componente que injeta e extrai o contexto em uma requisição ou mensagem, como propagador W3C Trace Context. |
| Receiver | Componente do colecctor que recebe telemetria, seja por Push ou por Pull. | 
| Resource | Conjunto de atributos que descreve a entidade que produz a telemetria, como nome do serviço, versão, host e ambiente. |
| Root Span | Primeiro span de um trace, sem span pai. |
| Sampling | Processo de decisão sobre traces que serão mantidos, para reduzir volume e custo de armazenamento. |
| SDK | Implementação da API que cuida de amostragem, processamento, agregação e exportação dos dados. |
| Semantic Coventions | Nomes e valores padronizados para atributos, spans e métricas, garantindo que dados de diferentes origens tenham o mesmo significado. |
| Severity | Nível de importância de um log (Trace, Debug, Info, Warn, Error, Fatal). |
| Signal | Categoria de telemetria. Os principais são traces, métricas, logs e baggage. |
| Span | Unidade de trabalho dentro de um trace (uma chamada HTTP, uma query ao banco, uma função), com nome, início, duração, atributos, eventos e status. |
| Span Context | Dados imutáveis de um span propagados entre processos: Trace ID, Span ID, Trace Flags e Trace State. |
| Span Event | Registro com data e hora dentro de um span, usado para marcar algo que aconteceu durante a operação, como uma exceção. |
| Span Kind | Tipo do Span, que descreve seu papel na interação: Internal, Server, Client, Producer ou Consumer. |
| Span Status | Resultado da operação: Unset, Ok, ou Error. |
| Tail-Based Sampling | Amostragem em que a decisão é tomada depois que o trace termina, permitindo manter traces com alta latência, erros, etc. Normalmente feita no Collector. |
| Telemetry | Dados emitidos por uma aplicação ou infraestrutura para descrever seu comportamento. | 
| Trace | Registro do caminho completo de uma requisição ao passar por vários serviços, formado por um conjunto de spans. |
| Trace Flags | Indicadores binários do trace, como o flag de "sampled". |
| Trace ID | Identificador único (16 Bytes), compartilhado por todos os spans de um mesmo trace. | 
| Trace State | Campo que carrega informações específicas de fornecedores junto com o contexto do trace, em pares chave-valor definidos pela especificação W3C. |
| Tracer | Objeto usado para criar spans. | 
| Tracer Provider | Ponto de entrada do SDK para traces, responsável por criar Tracers e configurar amostragem, processadores e exporters. |
| Up Down Counter | Instrumento de métrica que acumula valores que podem aumentar ou diminuir, como itens em uma fila. |
| Vendor-Neutral | Característica do OpenTelemetry de funcionar com diferentes backends sem a necessidade de reinstrumentar o código. |
| View | Configuração do SDK que personaliza como uma métrica é agregada, renomeada ou filtrada antes de ser exportada. |
| W3C Trace Context | Padrão do W3C que define os cabeçalhos HTTP traceparent e tracestate, para propagar o contexto de trace entre serviços. | 

  </div>
  </details>        

</div>
</details>

----

<details>
  <summary><b> 1.5. InfluxDB - Referência: <a href="https://docs.influxdata.com/"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 1.5.1. Glossário </summary>
  <div align="Center">

<br>  

| Termo | Descrição |
|-------|-----------|
| Aggregate Function | Função que reduz um conjunto devalores a um só: mean(), sum(), count(), max() |
| Apache Arrow | Formato de dados colunar em memória, usado para processamento rápido de consultas. |
| Apache DataFusion | Motor de Consultas em Rust, baseado em Arrow. Executa as queries SQL e InfluxQL. |
| Apache Parquet | Formato de arquivo colunar e compactado, usado para persistir os Dados. |
| API Token | Credencial de autenticação com permissões de leitura e / ou escrita sobre recursos específicos. |
| Bucket | Local nomeado onde os dados de séries temporais são armazenados, com um retention period associado. |
| Cardinality | Número de valores únicos em um conjunto de dados. |
| Check | Consulta agendada que avalia dados e atribui um status. |
| Chronograf | Interface web de visualização e administração do TICK Stack. |
| CLI | Ferramenta de linha de comando (influx, influxdb3), para gerenciar o banco, escrever e consultar dados. |
| Compactor | Componente que reorganiza e otimiza arquivos parquet para melhor a performance de leitura. |
| Continuous Query (CQ) | Consulta InfluxQL executada automaticamente em intervalos, geralmente para downsampling. |
| Dashboard | Painel com visualizações - gráficos, medidores, tabelas -, de dados do InfluxDB. |
| Database | Contêiner lógico de Dados. |
| Downsampling | Redução da resolução dos dados para economizar armanzemanto e acelerar consultas históricas. |
| Edge Data Replication (EDR) | Replicação de dados de uma instância OSS local para o InfluxDB Cloud. |
| Field | Par chave-valor com os dados medidos. |
| Field Key / Field Value | Nome e valor de um field. |
| Flight SQL | Protocolo para consultar bancos via SQL sobre Arrow Flight, usado como interface de consulta. |
| Flux | Linguagem Funcional de Script e Consulta de Dados. | 
| Garbage Collector | Componenet que remove dados e metadados expirados ou excluídos. |
| Group Key | Lista de Colunas que define quais registros pertencem à mesma tabela de saída em um resultado Flux. |
| Ingester | Componenet que recebe, valida e persiste os dados escritos. |
| InfluxDB IOx | Novo motor de armazenamento, escrito em Rust e baseado em Arrow, DataFusion e Parquet. |
| InfluxDB OSS (Open Source Software) | Versão de código aberto, instalada e gerenciada pelo próprio usuário. |
| InfluxQL | Linguagem de consulta semelhante a SQL. | 
| Kapacitor | Motor de processamento de dados, alertas, e ETL do TICK Stack, com a linguagem TICKscript. | 
| Last Value Cache (LVC) | Cache que guarda os valores mais recentes de séries, acelerando consultas de "último valor". |
| Line Protocol (LP) | Formato de Texto para Escrever Dados. |
| Measurement | Nome que agrupa dados relacionados, análogo a uma tabela. |
| Notebook | Documento interativo na UI que combina consultas, visualizações e anotações. |
| Notification Endpoint / Rule | Destino (Slack, PagerDuty, HTTP), e regra que define quando enviar alertas. |
| Organization (org) | Espaço de trabalho que agrupa usuários, buckets, dashboards e tasks. |
| Pipe-Forward Operation | Operador do Flux que encadeia funções, passando a saída de uma como entrada da próxima. |
| Point | Registro únivo de dados, composto por measurement, tag, set, field set e timestamp. |
| Precision | Granularidade do timestamp: ns, us, ms, s | 
| Processing Engine | Ambiente embutido para rodar plugins em Python. |
| Querier | Component que executa consultas lendo dados do ingester e do object store. | 
| Retention Period | Tempo pela qual os dados são mantidos antes de serem removidos automaticamente. |
| Retention Policy (RP) | Regra que define duração, replicação e shard duration dos dados de um database. |
| Router | Componente que recebe as requisições de escrita e as encaminha aos ingesters. |
| Scraper | Coletor que busca métricas em endpoints Prometheus e as grava no InfluxDB. |
| Series | Conjunto de Point com o mesmo Measurement e tag set. |
| Series Cardinality | Número total de series únicas em um database ou bucket. |
| Shard / Shard Group | Unidade física de armazenamento que contém dados de um intervalo de tempo. |
| SQL | Linguagem padrão de consulta, suportada nativamente. |
| Tag | Par chave-valor indexado, usado para filtrar e agrupar. Valores são sempre strings. |
| Tag Key / Tag Value / Tag Set | Nome da Tag, seu valor e o conjunto de todas as tags de um point. |
| Task | Script Flux agendado, usado para processar dados periodicamente. |
| Telegraf | Agente de Coleta baseado em Plugins, que reune métricas de diversas fontes e as envia ao InfluxDB ou outros destinos. |
| TICK Stack | Conjunto de ferramentas Telegraf, InfluxDB, Chronograf e Kapacitor. |
| Time Series | Sequência de pontos de dados indexados por tempo. |
| Timestamp | Data e hora associada a um point, armazenada em UTC. É a chave primária temporal. |
| TSDB (Time Series Database) | Banco de dados otimizado para dados indexados por tempo. |
| TSI (Time Series Index) | Índice em disco para séries, que permite lidar com alta cardinalidade, sem esgotar a memória. |
| TSM (Time Structured Merge Tree) | Motor de armazenamento em disco otimizado para escrita e compressão séries temporais. |
| Variable | Valor dinâmico usado em queries de dashboards para torná-las reutilizáveis. |
| WAL (Write-Ahead Log) | Log de escritas gravado antes dos dados serem persistidos definitivamente, garantindo durabilidade em caso de falhas. |
| Window | Agrupamento de dados por intervalos de tempo. |  

  </div>
  </details>        

</div>
</details>

----

</div>
</details>

----

<details>
  <summary><b> 2. CI / CD </b></summary>
  <div align="left">

<br>

<details>
  <summary><b> 2.1. ArgoCD - Referência: <a href="https://argo-cd.readthedocs.io/en/stable/"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 2.1.1. Glossário </summary>
  <div align="Center">

<br>  

| Termo | Descrição |
|-------|-----------|
| App of Apps | Padrão onde uma Application aponta para um repositório que contém outras Applications, permitindo gerenciamento e provisionamento a partir de um único ponto de entrada. |
| Application | CRD que representa uma instância implantada: Liga uma origem a um destino - Source -> Cluster / Namespace. | 
| Application Controller | Componente que monitora aplicações, compara o "Live State" com o "Desired State", executando o Sync. |
| ApplicationSet | CRD e Controller que geram várias Applications a partir de um Template e de Generatores (App por Cluster ou por pasta do Git.) |
| AppProject / Project | Agrupamento lógico de aplicações com restrições: repositórios de origem permitidos, destinos, tipos de recursos e papéis de acesso. |
| Argo CD Image Updater | Ferramenta complementar que detecta novas versões de imagens de contêiner e atualiza as aplicações automaticamente. |
| Argo Rollouts | Projeto irmão para Progressive Delivery (Canary, Blue / Green), que se integra ao ArgoCD. |
| Auto-Sync (Automated Sync) | Política que aplica automaticamente no cluster as mudanças detectadas no Git, sem ação manual. |
| CLI (argocd) | Ferramenta de linha de comando para gerenciamento de aplicações, projeetos, clusters, repositórios e contas. | 
| Cluster | Cluster Kubernetes registrado no ArgoCD como destino de Deploy. |
| ConfigMap (argocd-cm, argocd-rbac-cm) | Objetos de configuração do ArgoCD: argocd-cm guarda ajustes gerais e o argocd-rbac-cm define as políticas de RBAC. |
| Config Management Plugin (CMP) | Mecanismo para gerar manifestos com ferramentas personalizadas, além de Helm, Kustomize e Jsonnet. |
| CRD (Custom Resource Definition) | Recurso do Kubernetes que estende a API com novos tipos de objeto. Os principais são: Application, ApplicationSet e AppProject. |
| Declarative Setup | Configuração do Próprio ArgoCD definida como manifestos YAML versionados. |
| Degraded | Status de Saúde que indica falha em um recurso. |
| Desired State / Target State | Estado Desejado, definido pelos manifestos no Git. |
| Dex | Provedor de Identidade OIDC embutido, usado para integrar Single Sign On com provedores externos (GitHub, LDAP, SAML etc.). |
| Diff | Comparação entre Desired State e o Live State, que determina se a aplicação está OutOfSync. |
| Drift | Divergência do Cluster em relação ao Git, geralmente causada por alterações manuais. |
| Finalizer | Marcador (resources-finalizer.argocd.argoproj.io) que faz o ArgoCD remover os recursos gerenciados ao excluir a Application (Cascading Delete). |
| Generator | Componente do ApplicationSet que produz os parâmetros usados no template. Tipos comuns: List, Cluster, Git, Matrix, Merge, Pull Request e SCM Provider. |
| Git Repository | Fonte da verdade do GitOps, onde ficam os manifestos (ou charts), que descrevem o estado desejado. |
| GitOps | Prática em que o Git é a fonte única da verdade da infraestrutura e das aplicações, e um agente mantém o cluster sincronizado com ele. |
| Health Status | Estado de saúde de um recurso ou aplicação: PreSync, Sync, PostSync, SyncFail e PostDelete. |
| Helm | Gerenciador de pacotes (charts) do Kubernetes, suportado nativamente como ferramenta de renderização de manifestos. |
| Hook (Resource Hook) | Recurso executado em fases específicas do Sync: PreSync, Sync, PostSync, SyncFail e PostDelete. |
| ignoreDifferences | Configuração que faz o ArgoCD ignorar campos específicos na comparação. |
| In-cluster | Destino que representa o mesmo cluster em que o ArgoCD está instalado. |
| Jsonnet | Linguagem de Templates de Dados, Suportada para Gerar Manifestos. |
 
  </div>
  </details>        

</div>
</details>

</div>
</details>

----
