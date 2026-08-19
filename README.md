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


  </div>
  </details>    

  <details>
  <summary> 1.4 Consultas | Querying </summary>
  <div>

    - PromQL 
      - Linguagem de consultas funcional: Prometheus Query Language; 
      - Permite selecionar e agregar dados de séries temporais em tempo real; 
      - Tipos de Consulta:
        - Instantânea (Instant Query): único ponto no tempo;
        - Intervalo (Range Query): intervalos igualmente espaçados entre um horário inicial e final.
        - Na Interface Web do Prometheus, Table é para instantâneas e Graph para Intervalo.   
      - Para Regras de Consulta do PromQL: https://prometheus.io/docs/prometheus/latest/querying/basics/  


  </div>
  </details>    


----

</div>