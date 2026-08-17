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
  <summary><b> 1. Prometheus </b></summary>
  <div align="left">
    
<br>
    
  <details>
  <summary> 1.1 Visão Geral </summary>
  <div>

    - Prometheus é um sistema de monitoramento e alerta Open Source, criado originalmente na SoundCloud;
    - Foi adicionado na CNCF (Cloud Native Computing Foundation) em 2016, sendo o segundo projeto hospedado após Kubernetes.  
  
    - Características: 
      • Modelo de dados multidimensional, com dados de séries temporais identificados pelo nome da métrica e por pares de chave/valor. Exemplo:  
        - http_requests_total{method="GET", status="200", endpoint="/users"}
          - Métrica: http_requests_total
          - Labels: method="GET" | status="200" | endpoint="/users"  

      • Utiliza PromQL: Linguagem de consulta;
      • Nenhuma dependência de armazenamento distribuído;
      • A coleta de séries temporais ocorre por modelo PULL, via HTTP;
      • O Envio (Push) de Séries Temporais é compatível por meio de um gateway intermediário;
      • Os targets / alvos são descobertos por meio do Service Discovery ou Configuração Estática; 
      • Suporte a vários modos de geração de gráficos e Dashboards 

  </div>
  </details>

<br>