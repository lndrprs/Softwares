----
<div align="center">
<h6>

██████╗░██████╗░░█████╗░░░░░░██╗███████╗████████╗░█████╗░░██████╗
██╔══██╗██╔══██╗██╔══██╗░░░░░██║██╔════╝╚══██╔══╝██╔══██╗██╔════╝
██████╔╝██████╔╝██║░░██║░░░░░██║█████╗░░░░░██║░░░██║░░██║╚█████╗░
██╔═══╝░██╔══██╗██║░░██║██╗░░██║██╔══╝░░░░░██║░░░██║░░██║░╚═══██╗
██║░░░░░██║░░██║╚█████╔╝╚█████╔╝███████╗░░░██║░░░╚█████╔╝██████╔╝
╚═╝░░░░░╚═╝░░╚═╝░╚════╝░░╚════╝░╚══════╝░░░╚═╝░░░░╚════╝░╚═════╝░

░██████╗░█████╗░███████╗████████╗░██╗░░░░░░░██╗░█████╗░██████╗░███████╗░██████╗
██╔════╝██╔══██╗██╔════╝╚══██╔══╝░██║░░██╗░░██║██╔══██╗██╔══██╗██╔════╝██╔════╝
╚█████╗░██║░░██║█████╗░░░░░██║░░░░╚██╗████╗██╔╝███████║██████╔╝█████╗░░╚█████╗░
░╚═══██╗██║░░██║██╔══╝░░░░░██║░░░░░████╔═████║░██╔══██║██╔══██╗██╔══╝░░░╚═══██╗
██████╔╝╚█████╔╝██║░░░░░░░░██║░░░░░╚██╔╝░╚██╔╝░██║░░██║██║░░██║███████╗██████╔╝
╚═════╝░░╚════╝░╚═╝░░░░░░░░╚═╝░░░░░░╚═╝░░░╚═╝░░╚═╝░░╚═╝╚═╝░░╚═╝╚══════╝╚═════╝░
</h6>
</div>


----

<details>
  <summary><b> 1.9 Prometheus </b></summary>
  <div align="left">

<br>

  <details>
  <summary> 1.9.1 Exporter Customizado Simples </summary>
  <div>
    
    - Projeto criado no Docker, usando Python como Exportador;  
    - A ideia é ter métricas de um sistema fictício, uma fila de pedidos, usando 4 tipos de métricas e convenções de nomenclatura;  
      - Os 4 tipos de métricas: Counter, Gauge, Histogram, Summary;  
      - Convenções de Nomeamento: _total, _seconds, _bytes, prefixo de domínio;  
      - Endpoint /metrics e formato de exposição;  
      - Boas práticas de rótulos (evitando alta cardinalidade).   

    - Estrutura do Projeto:
     - Exporter Customizado Simples [Diretório]
       - exportador.py (Arquivo do Exportador em Python);
       - requirements.txt (Dependências para serem instaladas no Contêiner);
       - Dockerfile (Receita para construção da imagem Docker do exportador. Ou seja, o contêiner do Exportador);
       - docker-compose.yml (Orquestração de múltiplos contêineres, sendo o exportador e o Prometheus);
       - prometheus.yml (Arquivo de configuração a ser usado no contêiner do Prometheus).
      
     - Arquitetura
       - A Rede do Docker Compose terá dois contêineres: Exportador e Prometheus; 
       - Prometheus fará GET das métricas a cada 5 Segundos no Exportador;
       - Da sua máquina, conseguirá verificar tanto o endpoint /metrics do Exportador, quanto a interface de usuário do Prometheus; 
       - Docker Compose(Exportador <--- Prometheus) <--- Host

     - Arquivos
       - Depois de copiar o conteúdo dos arquivos, criando-os no diretório, rodar: docker-compose up -d 
       
<details>
<summary><code>requirements.txt</code></summary>

```
prometheus_client==0.20.0
```

</details>

<details>
<summary><code>Dockerfile</code></summary>

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY exporter.py .
EXPOSE 8000
CMD ["python", "exporter.py"]
```

</details>

<details>
<summary><code>prometheus.yml</code></summary>

```yaml
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: "order-queue-exporter"
    static_configs:
      - targets: ["exporter:8000"]
```

</details>

<details>
<summary><code>docker-compose.yml</code></summary>

```yaml
version: "3.8"
services:
  exporter:
    build: .
    ports:
      - "8000:8000"

  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
    depends_on:
      - exporter
```

</details>

<details>
<summary><code>exporter.py</code></summary>

```python


import random
import time
import threading
from prometheus_client import start_http_server, Counter, Gauge, Histogram, Summary

# ---- COUNTER ----
# Só cresce. Use _total como sufixo (convenção de naming).
orders_processed_total = Counter(
    "orderqueue_orders_processed_total", # <---- Troca de Nome de Métrica
    "Total de pedidos processados",
    ["status"]  # label de baixa cardinalidade: success/failed
)

# ---- GAUGE ----
# Sobe e desce. Representa um valor instantâneo.
queue_size = Gauge(
    "orderqueue_queue_size", # <---- Troca de Nome de Métrica
    "Número atual de pedidos na fila"
)

# ---- HISTOGRAM ----
# Mede distribuição (ex: duração). Sufixo de unidade no singular _seconds.
order_processing_duration_seconds = Histogram(
    "orderqueue_order_processing_duration_seconds", # <---- Troca de Nome de Métrica
    "Duração do processamento de um pedido",
    buckets=[0.05, 0.1, 0.25, 0.5, 1, 2.5, 5, 10]
)

# ---- SUMMARY ----
# Similar ao histogram, mas calcula quantis no client-side.
order_payload_size_bytes = Summary(
    "orderqueue_order_payload_size_bytes", # <---- Troca de Nome de Métrica
    "Tamanho do payload do pedido em bytes"
)


def simulate_queue():
    """Simula produção e consumo de pedidos continuamente."""
    current_size = 0
    while True:
        # Simula chegada de novos pedidos na fila
        arrivals = random.randint(0, 5)
        current_size += arrivals
        queue_size.set(current_size)

        # Simula processamento de um pedido
        if current_size > 0:
            start = time.time()
            time.sleep(random.uniform(0.05, 1.5))  # trabalho simulado
            duration = time.time() - start

            order_processing_duration_seconds.observe(duration)
            order_payload_size_bytes.observe(random.uniform(200, 5000))

            success = random.random() > 0.1  # 90% de sucesso
            status = "success" if success else "failed"
            orders_processed_total.labels(status=status).inc()

            current_size -= 1
            queue_size.set(current_size)

        time.sleep(1)


if __name__ == "__main__":
    start_http_server(8000)  # expõe /metrics na porta 8000
    print("Exporter rodando em http://localhost:8000/metrics")
    simulate_queue()
```

</div>
</details>    

----
