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

----

</div>
