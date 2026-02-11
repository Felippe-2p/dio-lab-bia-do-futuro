# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores relacionadas a golpes e fraudes |
| `perfil_investidor.json` | JSON | Representar perfil do cliente, histórico de incidentes e comportamento de risco |
| `produtos_financeiros.json` | JSON | Listar diferentes tipos de golpes, sinais comuns e orientações preventivas |
| `transacoes.csv` | CSV | Simular registros de tentativas de fraude em transações e contatos suspeitos   |

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

- O arquivo `historico_atendimento.csv` foi adaptado para registrar interações relacionadas a golpes e fraudes (ligações suspeitas, phishing, WhatsApp clonado, boletos falsos).  
- O arquivo `perfil_cliente.json` substituiu o antigo perfil de investidor, trazendo informações sobre histórico de incidentes, comportamento de risco e preferências de segurança.  
- O arquivo `tipos_fraudes.json` substituiu a lista de produtos financeiros, descrevendo diferentes tipos de golpes, sinais comuns e orientações preventivas.  
- O arquivo `transacoes.csv` foi adaptado para simular registros de tentativas de fraude em transações e contatos suspeitos, em vez de gastos pessoais.  
- Todos os datasets foram expandidos para incluir **mais exemplos variados de fraudes**, tornando a base de conhecimento mais robusta e realista para o agente Protege+.  


---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

```python
import json
import pandas as pd

perfil = json.load(open('./data/perfil_cliente.json', encoding='utf-8'))
transacoes = pd.read_csv('./data/transacoes.csv')
historico = pd.read_csv('./data/historico_atendimento.csv')
fraudes = json.load(open('./data/tipos_fraudes.json', encoding='utf-8'))
```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

- Os dados são consultados dinamicamente conforme a interação do cliente.  
- O agente não insere todo o dataset no system prompt; em vez disso, busca apenas os registros relevantes (ex: histórico de atendimento, perfil do cliente, tipos de fraudes).  
- As respostas são sempre baseadas nesses dados, com foco em **alertar sobre golpes e fraudes** e orientar o cliente a procurar **canais oficiais**.  
- Quando não há informação suficiente, o agente admite a limitação e reforça a necessidade de contato com o banco ou agência oficial.  


---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: Maria Oliveira
- Idade: 58
- Perfil: Conhecimento digital básico
- Preferência: Receber alertas sobre golpes comuns

Últimos incidentes registrados:
- 01/11: Ligação suspeita pedindo senha
- 03/11: E-mail de phishing solicitando atualização cadastral
- 05/11: Mensagem de WhatsApp pedindo transferência
- 07/11: SMS com link fraudulento para atualização de app
```
