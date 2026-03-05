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

| **Subdomínio**                  | **Descrição**                                                                                   | **Tipo**      |
|--------------------------------|-------------------------------------------------------------------------------------------------|---------------|
| Coletar preferências dos usuários | Através de perguntas abertas, entender e validar o perfil do viajante, para que a viagem possa ser moldada a partir disso.| Core Domain   |
| Curadoria de dados dos locais   | Avaliação qualitativa dos locais por meio da análise de opiniões e feedbacks dos usuários.      | Core Domain   |
| Gestão de dados dos locais      | Gestão dos dados brutos sobre pontos turísticos, atividades e locais de viagem.                 | Support       |
| Gestão de orçamentos            | Registrar e acompanhar os custos durante a viagem.                                              | Support       |
| Controle de feedbacks           | Armazenar feedbacks dos usuários para melhorar recomendações futuras.                           | Support       |
| Passagens aéreas                | Integração com APIs para consulta de valores e opções de passagens.                              | Generic       |
| Mapas e climas                  | Fornecer localização, rotas e informações climáticas para navegação.                             | Generic       |
| Autenticação                    | Gerenciar cadastro, login e permissões dos usuários.                                            | Generic       |
| Assinaturas                     | Processar pagamentos e gerenciar planos premium.                                                | Generic       |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context**      | **Responsabilidade**                                                                                         | **Subdomínios Relacionados**                                      |
|--------------------------|---------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| Perfil do Viajante       | Coletar, armazenar e analisar as preferências, interesses e perfil dos usuários para personalizar viagens.   | Coletar preferências dos usuários, Controle de feedbacks          |
| Gestão de Destinos       | Gerenciar informações sobre destinos, pontos turísticos, atividades e dados locais.                          | Gestão de dados dos locais, Curadoria de dados dos locais          |
| Planejamento de Viagem   | Criar, organizar e otimizar o planejamento da viagem, integrando perfil, orçamento e recomendações.          | Gestão de orçamentos, Coletar preferências dos usuários, Controle de feedbacks |
| Mapas e Navegação        | Fornecer mapas, rotas, localização e meteorologia para apoio à navegação.                                     | Mapas e climas                                                    |
| Identidade e Acesso      | Gerenciar cadastro, autenticação e controle de permissões dos usuários.                                      | Autenticação                                                      |
| Faturamento e Assinatura | Processar pagamentos, gerenciar planos e controlar assinaturas premium da plataforma.                        | Assinaturas                                                       |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.


| **De (Origem)**           | **Para (Destino)**        | **Tipo de Relacionamento** | **Explicação**                                                                 | **Forma de Comunicação**     | **Exemplo de Evento/Chamada**                         |
|---------------------------|----------------------------|----------------------------|--------------------------------------------------------------------------------|------------------------------|--------------------------------------------------------|
| Perfil do Viajante        | Planejamento de Viagem     | Cliente / Fornecedor       | O Planejamento depende das preferências e do perfil do usuário para gerar roteiros personalizados. | API REST                     | Obter preferências do viajante                         |
| Gestão de Destinos        | Planejamento de Viagem     | Cliente / Fornecedor       | O Planejamento consome dados de destinos e atividades para compor o roteiro.   | API REST                     | Obter informações de destinos                          |
| Perfil do Viajante        | Gestão de Destinos         | Kernel Compartilhado       | O conceito de Preferência é compartilhado para classificar destinos compatíveis com o viajante.     | Kafka com Change Data Capture| Atualização de preferências quando perfil é atualizado |
| Planejamento de Viagem    | Mapas e Navegação          | ACL (Anticorruption Layer) | O Planejamento utiliza serviços externos de mapas sem depender diretamente de suas estruturas internas. | API com camada de adaptação | Tradução de coordenadas, locais e horários              |
| Identidade e Acesso       | Perfil do Viajante         | Conformista                | O Perfil aceita o modelo de autenticação existente sem impor adaptações.       | API REST                     | Autenticação válida: True / False                      |
| Faturamento e Assinatura  | Planejamento de Viagem     | Cliente / Fornecedor       | O Planejamento consulta o status da assinatura para liberar recursos premium.  | API REST                     | Verificar plano do usuário                              |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**             | **Descrição**                                                                  |
|-----------------------|--------------------------------------------------------------------------------|
| Viajante              | Usuário que planeja ou participa de uma viagem.                                |
| Viagem                | Plano organizado com destino, datas, orçamento e atividades.                   |
| Roteiro               | Sequência de experiências dentro da viagem.                                    |
| Perfil de Viajante    | Representação dos interesses e histórico do usuário.                           |
| Recomendação          | Sugestão personalizada gerada por IA.                                          |
| Estilo de Viagem      | Classificação do perfil do viajante.                                           |
| Orçamento             | Limite financeiro da viagem.                                                   |
| Conquista             | Reconhecimento obtido por metas concluídas.                                    |
| Meta de Viagem        | Objetivo pessoal do viajante.                                                  |
| Otimização de Roteiro | Ajuste automático visando melhor custo e experiência.                          |
| Jornada de Planejamento | Processo completo de criação e organização de uma viagem.                    |
| Experiência           | Atividade ou vivência realizada durante a viagem.                              |
| Pacote de Viagem      | Conjunto estruturado de roteiro, orçamento e experiências.                     |
| Preferência           | Critério individual do viajante para personalização da viagem.                 |
| Histórico de Viagens  | Registro das viagens anteriores do usuário.                                    |

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
