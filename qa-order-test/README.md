-- Visão Geral
Este projeto tem como objetivo demonstrar a capacidade de planejamento, execução e automação de testes em uma API de pedidos.  
A API possui processamento assíncrono e regras de idempotência, simulando um cenário comum de integrações distribuídas.  
O foco principal foi garantir a qualidade dos fluxos críticos, priorizando cenários de maior risco para o negócio.


--Escopo;
- Endpoint **POST /orders**
- Endpoint **GET /orders/{orderId}**
- Validação de payload e contrato da API
- Testes de fluxo assíncrono (status PENDING → PROCESSED)
- Testes de idempotência (orderId duplicado)
- Testes de cenários negativos (payload inválido)

--Estratégia de Testes
A estratégia adotada foi baseada em risco, priorizando os cenários que podem gerar maior impacto ao negócio caso apresentem falhas.  
Os testes foram concentrados nos de API por serem mais rápidos, estáveis e permitirem validações precoces das regras de negócio.

Foram utilizados:
- Testes funcionais de API
- Testes negativos
- Validação de contrato
- Automação dos fluxos críticos

Risco

- Idempotência
  - Impacto: Alto
  - Prioridade: Alta  
  Falhas nesse cenário podem gerar pedidos duplicados e impacto financeiro.

- Payload inválido
  - Impacto: Médio/Alto
  - Prioridade: Alta  
  Dados inconsistentes podem vir à comprometer a integridade do sistema.

- Fluxo assíncrono
  - Impacto: Média
  - Prioridade: Média  
  Erros podem causar pedidos presos em estado incorreto.

-- Casos de Teste Principais
Os principais cenários cobertos foram:

- Happy Path: criação de pedido com payload válido
- Validação de contrato da resposta da API
- Idempotência: envio do mesmo `orderId` mais de uma vez
- Payload inválido (campos ausentes ou valores inválidos)
- Consulta do status do pedido via GET

-- Automação de Testes
A automação foi realizada utilizando o Postman, permitindo fácil execução e manutenção dos testes de API.  
Os testes automatizados validam:

- Status code HTTP
- Estrutura do payload de resposta
- Regras de negócio
- Comportamento em cenários negativos
OBS: Os fluxos críticos foram priorizados para automação, garantindo rápida detecção de falhas.

-- Testes de Fluxo Assíncrono
O fluxo assíncrono foi validado através da seguinte abordagem:

1. Envio de um pedido via POST /orders
2. Consulta periódica do status via GET /orders/{orderId}
3. Validação da transição de status de `PENDING` para `PROCESSED`
Mesmo em ambiente simulado o comportamento segue o raciocínio de filas/workers.
## Bug Report
Foi criado um bug report documentando um cenário em que a API aceita um payload inválido.  
O bug está descrito de forma clara, contendo passos para reprodução, resultado esperado, resultado atual, evidências e severidade, demonstrando a capacidade de comunicação de problemas.

---

-- Limitações
- A API utilizada é fictícia, sem backend real, o que resultou em bastante pesquisa para poder criar um ambiente propício.
- Alguns comportamentos são simulados para fins de demonstração
- Os testes automatizados representam o raciocínio e a abordagem, não a execução real em produção


