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
    - Foi adicionado na CNCF (Cloud Native Computing Foundation) em 2016, sendo o segundo projeto hospedado após Kubernetes.  
  
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

<br>