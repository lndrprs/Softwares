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
  <summary> 1.1 Visão Geral </summary>
  <div>

    - Prometheus é um sistema de monitoramento e alerta Open Source, criado originalmente na SoundCloud;
    - Foi adicionado na CNCF (Cloud Native Computing Foundation) em 2016, sendo o segundo projeto hospedado após Kubernetes. Ou seja, é Cloud Native;
    - A maioria dos componentes do Prometheus são escritos em Go; 
    - Prometheus não coleta Logs, sendo voltado para métricas; 
    - Para Alertas, é usado o Alertmanager;
    - Para Exportadores: https://prometheus.io/docs/instrumenting/exporters/
  
    - Características: 
      • Modelo de dados multidimensional, com dados de séries temporais identificados pelo nome da métrica e por pares de chave/valor.  
        - Exemplo: http_requests_total{method="GET", status="200", endpoint="/users"}
          - Métrica: http_requests_total
          - Labels / Rótulos: method="GET" | status="200" | endpoint="/users"  

      • Utiliza PromQL: Linguagem de consulta.
        - Exemplo: rate(http_requests_total[5m])
        - Calcula a taxa de requisições por segundo, nos últimos 5 minutos referente a métrica.
      
      • Nenhuma dependência de armazenamento distribuído.
        - O próprimo Prometheus coleta e armazena os dados localmente;
        - No entanto, podem ser utilizadas integrações com outros armazenamentos no caso de algo escalável ou retenção longa usando Remote Write/Remote Read, como:
          - Thanos;
          - Cortex; 
          - AWS Timestream;
          - Azure Data Explorer;
          - Entre outras. 

      • A coleta de séries temporais ocorre por modelo PULL, via HTTP.
        - Ou seja, a Aplicação expõe as métricas através de um endpoint, e o Prometheus "Puxa" automaticamente e periodicamente as métricas, desde que configurado.  

      • O Envio (Push) de Séries Temporais é compatível por meio de um gateway intermediário;
        - Vamos supor que exista um serviço que rode por 30 segundos. Quando o Prometheus tentar fazer o Pull, o Job não estará sendo executado; 
        - Nisso, entra o Pushgateway. O serviço envia as métricas ao Pushgateway, e a partir dele, o Prometheus coleta usando o PULL;
        - Existem outras ferramentas, como StatsD, Graphite e Collectd (Que expõem as métricas /metrics). Assim transformam as métricas Push em Pull ao Prometheus. 
        - Arquiteturas de Exemplo:
          - App/Metrics <- Pull | Prometheus 
          - Job / Serviço -> Push | Pushgateway <- Pull | Prometheus 
          - Prometheus -> Push | Armazenamento Remoto (Remote Write)

      • Os targets / alvos são descobertos por meio do Service Discovery ou Configuração Estática;
        - Prometheus consegue descobrir automaticamente os alvos;
        - Isso porque ele verifica o "namespace" total, e não os pods de forma unitária.

      • Suporte a vários modos de geração de gráficos e Dashboards 
        - É possível verificar acessando o endpoint /graph 

  </div>
  </details>

  <details>
  <summary> 1.2 Conceitos </summary>
  <div>

    - Prometheus armazena todos os dados como séries temporais: sequências de valores associados a timestamps que pertencem à mesma métrica;
    - Cada série temporal é identificada exclusivamente por:
      - Nome da Métrica;
      - Pares opcionais de Chave / Valors (Labels) 

    - Dimensões diferentes da métrica são "modelos de dados dimensionais";
    - Labels são instâncias diferentes de uma mesma métrica - ou seja, as dimensões diferentes;

    - Tipos de Métricas 
      - Counter: Métrica cumulativa que representa um único contador crescente
        - Só pode aumentar;
        - Pode ser reiniciado para zero quando há restart;
        - Para números que podem diminuir, counter não é indicado;
        - "Quanto já aconteceu". 

      - Gauge: Métrica de único valor número que pode aumentar ou diminuir livremente; 
        - Temperatura, utilização de memória, CPU, conexões, etc.; 
        - "Quanto existe agora". 

      - Histogram: Registra observações, como duração das requisições, tamanho das respostas, latência...
        - Contabiliza essas observaçoes em buckets / intervalos configuráveis; 
        - Também fornece a soma de todos os valores observados e quantidade total de observações.  
          
      - Summary: Similar ao Histogram, gera amostras de observações e calcula quantis configuráveis em uma janela de tempo;
        - Exemplo: p50, p90, p99. 

    - Jobs e Instâncias
      - Um endpoint que pode ser "raspado" é uma instância, correspondendo a um processo; 
      - Conjuntos de instâncias com o mesmo propósito, é um job. Exemplo:
          - job: api-server 
            - instância 1: 1.2.3.4:5670
            - instância 3: 1.2.3.4:5671

  </div>
  </details>  

  <details>
  <summary> 1.3 Servidor Prometheus </summary>
  <div>

    - Prometheus coleta as métricas a partir da configuração de alvos / targets, raspando endpoints HTTP;
    - Ele mesmo expões métricas próprias para monitoramento da própria saúde: localhost:9090/metrics;
    - A configuração é feita no arquivo: prometheus.yml 
      - Guia de Configuração: https://prometheus.io/docs/prometheus/latest/configuration/configuration/

    - Para montagem de um ambiente teste com o Docker, ver as imagens: https://hub.docker.com/u/prom
      - Demais processos de instalação: https://prometheus.io/docs/prometheus/latest/installation/

    - Prometheus possui 2 tipos de regras:
      - Recording Rules: Pré-carrega expressões pesadas e salva o resultado como um novo conjunto de série temporal (Sendo mais rápido para consultar);
      - Alerting Rules: Permite definir condições de alerta baseados nas expressões e envia notificações para serviços externos.     
      - Os arquivos de regras devem ser carregados na configuração, em rule_files; 

    - Templates 
      - Servem para gerar conteúdos dinâmicos dentro das regras de alerta, anotações ou mensagens do AlertManager; 
      - Como se fossem mini scripts dentro das regras, formatando strings, acessando labels, fazendo cálculos simples, etc. 
      - Referências de Templates: https://prometheus.io/docs/prometheus/latest/configuration/template_reference/

    - Promtool
      - Ferramenta CLI do Prometheus, usada para testar, validar e depurar configurações e alertas; 
      - Ele verifica YAML inválido, regras quebradas, alertas que não disparam, expressões PromQL malformadas, ou erros que só aparecem em runtime;
      - Muito útil para ambientes de produção. 

    - Agent Mode 
      - No binário do Prometheus há também o modo Agente integrado; 
        - Utiliza as mesmas APIs, semântica, configuração e mecanismos de descoberta do modo Servidor;
        - Porém, alguns recursos são desativados: Consultas locais, TSDB, Alertas e Avaliação de Regras;
        - O binário é otimizado para realizar a raspagem e enviar as métricas por meio do Remote Write;
        - Utiliza apenas uma fração de recursos, em comparação ao modo Servidor;
        - Para utilizar o modo agente: prometheus --agent 

    - Remote Write 
        - Encaminha toas ou parte das métricas coletadas, para um local remoto; 
        - O Prometheus pode enviar as métricas para um ou mais destinos que suportem a API Remote Write.

    - HTTP API   
      - Para ver especificações da API: http://localhost:9090/api/v1/openapi.yml
      - Exemplos de Consultas: 
        - curl.exe 'localhost:9090/api/v1/query?query=up'          
        - curl.exe 'localhost:9090/api/v1/labels'
        - curl.exe 'localhost:9090/api/v1/query?query=node_cpu_seconds_total'
      - Documentação para API: https://prometheus.io/docs/prometheus/latest/querying/api/ 

      - Para Leitura Remota: curl.exe 'localhost:9090/api/v1/read'

    - PromQL | Querying | Consultas
      - Linguagem de consultas funcional: Prometheus Query Language; 
      - Permite selecionar e agregar dados de séries temporais em tempo real; 
      - Tipos de Consulta:
        - Instantânea (Instant Query): único ponto no tempo;
        - Intervalo (Range Query): intervalos igualmente espaçados entre um horário inicial e final.
        - Na Interface Web do Prometheus, Table é para instantâneas e Graph para Intervalo.   
      - Para Regras de Consulta do PromQL: https://prometheus.io/docs/prometheus/latest/querying/basics/          

    - Federação 
      - Permite que um servidor Prometheus colete séries temporais selecionadas de outro servidor Prometheus;   
      - Usado para obter configurações de Prometheus escaláveis ou trazer métricas de um serviço para outro;
      - Usa o endpoint: "/federate"

      - Federação Hierárquica 
        - Escala o prometheus para ambientes com dezenas de data centers e milhões de nós; 
        - A topologia se assemelha a uma árvore;
        - Exemplo:
          - Uma configuração pode consistir em vários servidores Prometheus que coletam dados em alto nível de detalhe;
          - E outro conjunto de servidores Prometheus globais que coletam e armazenam apenas dados agregados, dos servidores locais. 

    - HTTP SD (Service Discovery)
      - Configuração: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#http_sd_config
      - Integrações SD: https://prometheus.io/docs/operating/integrations/#http-service-discovery
      - Permite descobrir alvos em um endpoint HTTP, é uma alternativa ao File-Based Service Discovery;       
      - O Prometheus armazena em cache as listas de targets. Se ocorrer um erro ao buscar uma lista atualizada, continua usando a atual;
        - A lista de targets não é salva entre reinicializações. 

    - Management API 
      - Prometheus possui um conjunto de APIs de gerenciamento, que facilitam a automação e integração:
        1. Health Check: /healthy - Retorna a saúde do Servidor;
        2. Readiness Check: /ready - Retorna se consegue responder consultas / servir tráfego; 
        3. Reload: /reload - Permite recarregar a configuração do Prometheus; 
        4. Quit: /quit - Desativa o Prometheus, graciosamente.     

    - Linha de Comando 
      - Para Flags relacionadas ao Prometheus: https://prometheus.io/docs/prometheus/latest/command-line/prometheus/
      - Para Comandos Promtool: https://prometheus.io/docs/prometheus/latest/command-line/promtool/

    - Segurança 
      - A flag --web.enable-admin-api controla acesso administrativo a API HTTP, que inclui funcinaonlidades como deleção de séries temporais. 
        - É desativada por padrão, mas caso ativa, o endpoint é /api/*/admin/ (Também funciona para Pushgateway); 

      - Outra flag: --web.enable-lifecycle controla recarregamentos e desligamentos do Prometheus via HTTP, que também é desativado por padrão; 
        - Ao ser ativada, ficam acessíveis em /-/reload e /-/quit  

      - Para configuração de API e UI usando criptografia: https://prometheus.io/docs/guides/tls-encryption/; 
        - É possível usar Autenticação Básica HTTP sem TLS, mas expõe usuários e senhas em texto limpo através da rede;
        - No lado do servidor, senhas da autenticação básica são armazenadas como hashes com algoritmo bcrypt;
        - Há uma opção chamada insecure_skip_verify que pula a verificação SSL. 

  </div>
  </details>    

  <details>
  <summary> 1.4 Armazenamento </summary>
  <div>

    - Prometheus possui um banco de dados local de séries temporais em disco;
      - Opcionalmente, pode integrar-se a sistemas de armazenamento remoto. 

    - Armazenamento Local 
      - As amostras recebidas são agrupadas em blocos de duas horas. Cada bloco consiste em um diretório que possui:
        - Diretório de Chunks: Todas as amostras das séries temporais daquele período (Segmentadas por até 512 MB por padrão);
        - Arquivo de metadados;
        - Arquivo de Índice: Mapeia nomes de métricas e labels para as séries temporais presentes no diretório Chunks;
        - Arquivo Tombstones: Séries excluídas por meio da API. 

      - Flags mais importantes de configuração do armazenamento local:
        --storage.tsdb.path: Onde o Prometheus grava o banco de dados (Padrão: data/)
        --storage.tsdb.retention.time: Por quanto tempo deve reter amostras no armazenamento; 
        --storage.tsdb.retention.size: Número máximo de bytes de blocos de armazenamento a reter;   
        --storage.tsdb.wal-compression: Habilita compressão do WAL. 

      - Fórmula aproximada para calcular a capacidade de um servidor Prometheus:
        - Espaço em Disco Necessário = Tempo de retenção em segundos * Amostras por Segundo * Bytes por Amostra 

        Obs.: Para reduzir a taxa de amostras ingeridas, pode reduzir o número de séries temporais coletadas (Menos targets / menos séries por target), ou aumentar o intervalo de coleta (Scrape Interval). Sendo o primeiro mais eficaz. 

      - WAL - Write Ahead Log   
        - O bloco atual que recebe novas amostras, fica mantido em memória e não é totalmente persistido; 
        - Para proteção contra falhas, o Prometheus usa WAL (Write Ahead Log), que pode ser reproduzido quando o servidor Prometheus é reiniciado. 
        - Os arquivos WAL ficam no diretório "wal", em segmentos de 128 MB;
          - Possuem dados brutos que não foram compactados, e são significativamente maiores que os arquivos de blocos normais;
          - Um servidor prometheus mantém no mínimo 3 arquivos WAL. Servidores com alto tráfego podem possuir mais. 

        - O armazenamento local não é clusterizado, e nem replicado. Não oferecendo escalabilidade ou durabilidade em caso de falha de disco / nó;
        - Deve ser administrado como qualquer outro banco de dados de nó único;
        - Ainda sim, com uma arquitetura adequada, pode manter anos de dados no armazenamento local. 

    - Backups 
      - Os snapshots são recomendados para backups;
        - Backups sem snapshots podem perder os dados registrados desde a criação do último bloco da TSDB, que ocorre a cada duas horas; 
        - É possível utilizar armazenamento externo por meio das APIs de Remote Read / Remote Write. 

    - Compactação 
      - Em segundo plano, os blocos iniciais de duas horas são compactados em blocos maiores; 
      - A compactação cria blocos maiores contendo dados que abrangem até 10% do tempo de retenção, ou 31 dias; 
      - Tanto o bloco de origem quanto o bloco compactado devem coexistir no disco, o tamanho do disco pode exceder;
      - O excesso é liberado quando a próxima limpeza de retenção remove os blocos de origem. 

    - Integrações de Armazenamento Remoto 
      - Há quatro maneiras de conexão com armmazenamentos remotos:
        1. Ingestão de amostras através de uma URL Remota usando Remote Write; 
        2. Recebimento de amostras de outros clientes em Remote Write; 
        3. Ler dados de amostras de uma URL Remota com Remote Read; 
        4. Retornar dados de amostras solicitos pelos clientes, em Remote Read. 
      
      - Remote Write: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#remote_write
      - Remote Read: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#remote_read

      - Integrações: https://prometheus.io/docs/operating/integrations/#remote-endpoints-and-storage

    - Backfilling 
      - Cria blocos no banco de dados de séries temporais (TSDB) do Prometheus a partir de dados que já existiam antes; 
      - Preenche retroativamente o histórico do Prometheus com dados que não foram ingeridos no momento em que ocorreram;
      - Pode ser usado para migrar métricas de outro sistema de monitoramento ou TSDBs ao Prometheus. 


  </div>
  </details>    

  <details>
  <summary> 1.5 Visualização </summary>
  <div>

    - Navegador de Expressão 
      - Disponível no endpoint /graph;
      - Permite inserir qualquer expressão e ver seu resultado em uma tabela ou representado graficamente ao longo do tempo;
      - Usado, primariamente, para consultas ad-hoc ou debug. Para gráficos, recomendado usar Grafana ou templates de Console. 

    - Grafana
      - Plataforma open-source de visualização e análise; usado para monitorar e analisar métricas de várias origens de dados;
      - Suporta integrações com BDs como Prometheus, InfluxDB, Elasticsearch, e mais;
      - O data source do Prometheus está incluso no Prometheus desde 2015 (Versão 2.5.0).
        - Mais informações: https://prometheus.io/docs/visualization/grafana/ 

    - Perses 
      - Plataforma open-source de visualização e dashboards, projetado para observabilidade; 
      - Suporte nativo para Prometheus como origem de dados; 
      - Focado em facilidade de acesso, desenvolvimento focado em comunidade, GitOps e Dashboard as Code. 
        - Mais informações: https://prometheus.io/docs/visualization/perses/

    - Console Templates 
      - Permite a criação de consoles arbitrários usando a linguagem Go, e são servidos do servidor Prometheus; 
      - Possui curva de aprendizagem. Mais indicado começar pelo Grafana. 
        - Mais informações: https://prometheus.io/docs/visualization/consoles/

  </div>
  </details>    
  
  <details>
  <summary> 1.6 Instrumentação </summary>
  <div>

    - Client Libraries 
      - Antes de monitorar serviços, é necessário instrumentar o código via bibliotecas do Prometheus, que implementam tipos de métricas; 
      - Escolha a biblioteca que combina com a linguagem da aplicação, assim permite definir e expor métricas internas via HTTP;
        - Listagem de Bibliotecas: https://prometheus.io/docs/instrumenting/clientlibs/
        - Para criar novas Bibliotecas: https://prometheus.io/docs/instrumenting/writing_clientlibs/

    - Pushing Metrics 
      - Ocasionalmente precisará monitor componentes que não podem ser raspados; 
      - Pushgateway permite enviar séries temporais e batches curtos para um serviço intermediário, que o Prometheus consiga raspar;
      - Fácil para instrumentar scripts, sem uma biblioteca. 
        - Documentações de Linguagens: https://prometheus.io/docs/instrumenting/pushing/

    - Exporters e Integrations 
      - Há diversos exportadores terceiros para o Prometheus, alguns sendo mantidos oficialmente pelo GitHub do Prometheus: https://github.com/prometheus
      - Outro catálogo de exportadores, que podem não estar listados na lista acima: https://github.com/prometheus/prometheus/wiki/Default-port-allocations
        - Listagem da Documentação: https://prometheus.io/docs/instrumenting/exporters/#third-party-exporters

    - Writing Exporters 
      - Para Desenvolvimento de Exportadores: https://prometheus.io/docs/instrumenting/writing_exporters/
    
    - Exposition Formats 
      - Documentação de formatos de exposição oficialmente suportados: https://prometheus.io/docs/instrumenting/exposition_formats/

    - Escaping Schemes
      - Especificações de como Prometheus lida com nomes de métricas e labels; 
      - Existem quatro esquemas de "escaping" que são negociados via header HTTP durante a raspagem:
        - allow-utf-8: Permite nomes UTF-8 diretamente;
        - underscores: Substitui qualquer caractere fora do padrão por _ (Padrão);
        - dots: Substitui pontos por _dot_ e underscores por __
        - values: Codifica cada caractere não padrão como seu código Unicode em Hexadecimal, prefixado com U__ . 
      - https://prometheus.io/docs/instrumenting/escaping_schemes/ 

    - Content Negotiation 
      - Negociação com os alvos / targets sobre qual protocolo de exposição usar durante a raspagem;
      - Tipos de Protocolos:
        - PrometheusProto;
        - PrometheusText (0.0.4 e 1.0.0);
        - OpenMetricsText (0.0.1 e 1.0.0); 
      - https://prometheus.io/docs/instrumenting/content_negotiation/

  </div>
  </details>      

  <details>
  <summary> 1.7 Alertmanager </summary>
  <div>

    - Visão Geral de Alerta 
      - Regras nos servidores Prometheus enviam alertas ao Alertmanager; 
      - O Alertmanager gerencia esses alertas, incluindo o silenciamento, inibição, agregação e envio das notificações (Via e-mail, sistemas de notificação e plataformas de chat);
      - Os passos principais de configuração e notificação:
        - Instalar e Configurar o Alertmanager;
        - Configurar o Prometheus para se comunicar com o Alertmanager;
        - Criar regras de alerta no Prometheus. 

    - Alertmanager 
      - Lida com os alertas enviados por aplicações clientes, como o Prometheus; 
      - Implementações principais do Alertmanager: 
        - Agrupamento: Categoriza alertas de natureza similar em apenas uma notificação; 
        - Inibição: Supressa notificações para certos alertas se outros alertas estão disparando; 
        - Silenciamento: Mutar alertas por determinado período; 
      - Integrações de Notificação, via arquivo de Configuração: https://prometheus.io/docs/alerting/latest/integrations/
      - Configuração do Alertmanager: https://prometheus.io/docs/alerting/latest/configuration/

      - API de Gerenciamento:
        - get /-/healthy: Verificação de Saúde do Endpoint; 
        - get /-/ready: Verificação de respostas de Queries:
        - post /-/reload: Atualização do arquivo de configuração.
      
      - Alta Disponibilidade 
        - O Alertmanager suporta configuração para criação de Cluster, usando flags --cluster-*;
        - Flags de Alta Disponibilidade: https://github.com/prometheus/alertmanager#high-availability
        - Para configurações e arquiteturas de Alta Disponibilidade: https://prometheus.io/docs/alerting/latest/high_availability/

      - Limites de Alerta
        - Suporte para configuração da quantidade de alertas ativos;
        - Pode ser configurado usando a flag: --alerts.per-alertname-limit;
        - alertmanager_alerts_limited_total é uma métrica que mostra o total de alertas que foram derrubados por limite;
        - A flag alert-names-in-metrics adiciona o rótulo / label alertname à métrica. 

      - Templates de Notificações
        - As notificações enviadas aos receivers são construídas via templates; 
        - O Alertmanager já possui templates padronizados, mas podem ser customizados; 
          - Template padrão: https://github.com/prometheus/alertmanager/blob/main/template/default.tmpl
        
        - Para referências de dados usados nos Templates: https://prometheus.io/docs/alerting/latest/notifications/
        - Exemplos: https://prometheus.io/docs/alerting/latest/notification_examples/

      - Para HTTPS e Gossip: https://prometheus.io/docs/alerting/latest/https/

  </div>
  </details>      


  <details>
  <summary> 1.8 Melhores Práticas </summary>
  <div>

    - Nomeamento de Métrica e Rótulo: https://prometheus.io/docs/practices/naming/
    - Consoles e Dashboards: https://prometheus.io/docs/practices/consoles/
    - Instrumentação: https://prometheus.io/docs/practices/instrumentation/
    - Histogramas e Summaries: https://prometheus.io/docs/practices/histograms/
    - Alertas: https://prometheus.io/docs/practices/alerting/
    - Regras de Registros / Recording: https://prometheus.io/docs/practices/rules/
    - Pushgateway: https://prometheus.io/docs/practices/pushing/
    - Otimização de Escrita Remota: https://prometheus.io/docs/practices/remote_write/
    - O Zen do Prometheus: https://prometheus.io/docs/practices/the_zen/

  </div>
  </details>      

  <details>
  <summary> 1.9 Projetos </summary>
  <div align="Center">

| ID      | Título                              | Link      |
| --------| ------------------------------------|-----------|
| P1.1.1  | Exporter Customizado Simples        |           |



  </div>
  </details>        

----

</div>