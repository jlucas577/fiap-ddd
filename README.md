# Dinâmica: Design Estratégico do Projeto

## Objetivo
Identificar os subdomínios do projeto, classificá-los (Core, Supporting, Generic) e desenhar os bounded contexts, incluindo suas interações. Esse exercício ajudará a criar uma visão clara e estratégica do domínio.

---

## 1. Nome do Projeto
**TravelWall**

---

## 2. Objetivo Principal do Projeto
**Facilitar o planejamento de viagens.** - “Não perca a oportunidade de ter uma viagem fantástica”

---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

| **Subdomínio**                     | **Descrição**                                                                                                                         | **Tipo**     |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|-------------|
| Coletar preferências dos usuários  | Através de perguntas abertas, entender e validar o perfil do viajante, permitindo que a viagem seja moldada com base nessas informações. | Core Domain |
| Gestão de dados dos locais         | Envolver a coleta e gestão dos locais de viagem, incluindo pontos turísticos e opções de atividades.                                 | Core Domain |
| Gestão de orçamentos               | Registrar e acompanhar os custos durante a viagem.                                                                                    | Support     |
| Controle de feedbacks              | Armazenar feedbacks dos usuários para melhorar recomendações futuras.                                                                 | Support     |
| Passagens aéreas                   | Utilizar APIs (como Skyscanner) para consultar valores e opções econômicas de passagens aéreas.                                       | Generic     |
| Mapas                              | Fornecer informações de localização, calcular rotas e apresentar pontos de interesse próximos para apoiar o planejamento e navegação. | Generic     |
| Autenticação                       | Gerenciar cadastro, login e permissões dos usuários, garantindo acesso seguro às funcionalidades do sistema.                         | Generic     |
| Assinaturas                        | Processar transações financeiras, gerenciar assinaturas e realizar a cobrança de serviços premium da plataforma.                     | Generic     |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context**           | **Responsabilidade**                                                                                 | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------------------------|-----------------------------|
| Ex.: Contexto de Consultas    | Gerencia as consultas médicas, do agendamento à finalização, incluindo emissão de receitas.         | Gestão de Consultas         |
| Ex.: Contexto de Pagamentos   | Processa cobranças de consultas e repasses para médicos ou clínicas.                              | Pagamentos                  |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
| Contexto de Consultas        | Contexto de Pagamentos      | Mensageria (Evento)         | "Consulta Finalizada"                         |
| Contexto de Cadastro          | Contexto de Consultas      | API                         | Obter informações de um Paciente pelo ID      |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**             | **Descrição**                                                                  |
|-----------------------|--------------------------------------------------------------------------------|
| Viajante              | Usuário que planeja ou participa de uma viagem.                                 |
| Viagem                | Plano organizado com destino, datas, orçamento e atividades.                    |
| Roteiro               | Sequência de experiências dentro da viagem.                                     |
| Perfil de Viajante    | Representação dos interesses e histórico do usuário.                            |
| Recomendação          | Sugestão personalizada gerada por IA.                                           |
| Estilo de Viagem      | Classificação do perfil do viajante.                                            |
| Orçamento             | Limite financeiro da viagem.                                                    |
| Conquista             | Reconhecimento obtido por metas concluídas.                                     |
| Meta de Viagem        | Objetivo pessoal do viajante.                                                   |
| Otimização de Roteiro | Ajuste automático visando melhor custo e experiência.                           |

---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Desenvolver internamente com foco total.
- **Supporting Subdomain:** Desenvolver internamente ou parcialmente terceirizar.
- **Generic Subdomain:** Usar ferramentas ou serviços de mercado.

| **Subdomínio**              | **Estratégia**                         | **Ferramentas ou Serviços (se aplicável)** |
|-----------------------------|---------------------------------------|-------------------------------------------|
| Gestão de Consultas         | Desenvolvimento interno               |                                           |
| Cadastro de Usuários        | Interno com uso de Auth0 para login   | Auth0                                     |
| Pagamentos                  | Terceirizar usando API Stripe         | Stripe                                    |

---

## 8. Diagrama Visual (Opcional, mas Recomendado)
Desenhe um diagrama que mostre:
- Os bounded contexts.
- Como eles se comunicam.
- A relação com os subdomínios.

Use ferramentas como **Miro**, **Lucidchart** ou mesmo papel e caneta para criar seu diagrama e adicionar ao projeto.

---

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀
