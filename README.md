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
  <summary><b> 1. Prometheus - Referência: <a href="https://prometheus.io/docs/introduction/overview/"> Documentação Técnica</a></b></summary>
  <div align="left">
    
<br>
    
  <details>
  <summary> 1.1 Glossário </summary>
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


  </div>
  </details>        

  <details>
  <summary> 1.2 Projetos </summary>
  <div align="Center">

<br>

| ID      | Título                               | Descrição  |
| --------| ------------------------------------|-----------|
| P1.2.1  | Exporter Customizado Simples         | Exportador Python Expondo Métricas ao Prometheus|



  </div>
  </details>        


</div>
</details>

----

<details>
  <summary><b> 2. Dynatrace - Referência: <a href="https://docs.dynatrace.com/docs"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 2.1 Glossário </summary>
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


  </div>
  </details>        

  <details>
  <summary> 2.2 Projetos </summary>
  <div align="Center">

<br>

  </div>
  </details>        


</div>
</details>

----

<details>
  <summary><b> 3. Splunk - Referência: <a href="https://docs.splunk.com/Documentation"> Documentação Técnica</a></b></summary>
  <div align="left">

<br>
    
  <details>
  <summary> 3.1 Glossário </summary>
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

  </div>
  </details>        

  <details>
  <summary> 3.2 Projetos </summary>
  <div align="Center">

<br>

  </div>
  </details>        


</div>
</details>

----