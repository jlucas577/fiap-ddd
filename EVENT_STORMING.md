# 📌 Roteiro para a Atividade de Event Storming

## **1️⃣ Preparação (5-10 min)**
- Cada aluno ou grupo escolhe um **processo central** do trabalho.
  - Exemplo: Cadastro de clientes, processo de pagamento, controle de estoque, gestão de chamados.
---

## **2️⃣ Mapeamento de Eventos de Domínio (15-20 min)**
- Pergunta-chave: **"O que acontece no processo?"** *(sempre no passado)*
- Cada grupo lista eventos importantes.
  - **Exemplo para um sistema de vendas:**
    - **Pedido Criado**
    - **Pagamento Aprovado**
    - **Pedido Enviado**
    - **Pedido Entregue**
- Organizar os eventos em ordem cronológica.

---

## **3️⃣ Identificação de Comandos e Atores (10-15 min)**
- Pergunta-chave: **"O que causou esse evento?"**
- Relacionar **comandos** (ações ativas) com os **atores** (usuários ou sistemas externos).
  - **Exemplo:**
    - **Comando:** "Finalizar Pedido"
    - **Ator:** Cliente
    - **Evento gerado:** "Pedido Criado"

---

## **4️⃣ Descobrindo Regras e Políticas de Negócio (10-15 min)**
- Pergunta-chave: **"Quais regras precisam ser seguidas nesse processo?"**
- Identificar **políticas** (regras automáticas ou manuais).
  - **Exemplo:**
    - **Se o pagamento não for aprovado em 24h, cancelar pedido.**
- Mapear **integrações externas** (ex: APIs, sistemas de terceiros).

---

## **5️⃣ Identificação dos Bounded Contexts (10 min)**
- Pergunta-chave: **"Quem é responsável por cada parte do processo?"**
- Separar os eventos e comandos em **diferentes áreas do sistema**.
  - **Exemplo:**
    - **Contexto de Pedidos** (Criação e status dos pedidos)
    - **Contexto de Pagamento** (Autorização financeira)
    - **Contexto de Logística** (Entrega e rastreamento)

---

## **6️⃣ Discussão e Refinamento (15 min)**
- Cada grupo apresenta seu fluxo.
- **Perguntas para discussão:**
  - Há eventos que poderiam ser melhor detalhados?
  - Existem regras de negócio não mapeadas?
  - Algum comando ou evento depende de um sistema externo?
- Refinar o modelo conforme necessário.

---

## **🎯 Dicas para Facilitar a Atividade**
✅ **Eventos são sempre no passado** e os comandos no presente.  
✅ **O foco é explorar e aprender**, não a perfeição.  
✅ **Usar cores diferentes para cada tipo de post-it** (como na legenda da imagem de Event Storming).  
✅ **Pensar no fluxo real do dia a dia do trabalho** para tornar a atividade mais prática.  

---
## Links Úteis:

✅ https://medium.com/@jonesroberto/event-storming-guia-b%C3%A1sico-216498f5dd2d

✅ https://www.linkedin.com/pulse/o-que-%C3%A9-eventstorming-e-como-este-formato-de-workshop-rodrigues/

