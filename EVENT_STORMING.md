# Event Storming do TravelWall

## Objetivo
Mapear o fluxo fim a fim de planejamento de viagem no TravelWall, validando eventos de domínio, comandos, políticas e integrações entre bounded contexts.

---

## 1. Processo central escolhido
**Planejar uma viagem personalizada com controle de orçamento e roteiro.**

---

## 2. Linha do tempo de eventos de domínio
Os eventos abaixo estão em ordem cronológica e no passado.

1. **PreferenciasColetadas**
2. **PerfilDeViajanteValidado**
3. **ViagemCriada**
4. **OrcamentoDefinido**
5. **DestinosCurados**
6. **RoteiroGerado**
7. **ViagemConfirmada**
8. **ViagemIniciada**
9. **GastoRegistrado**
10. **ViagemFinalizada**
11. **FeedbackRegistrado**

---

## 3. Comandos, atores e eventos gerados

| Comando | Ator | Evento gerado |
|---|---|---|
| ColetarPreferenciasDoViajante | Viajante | PreferenciasColetadas |
| ValidarPerfilDoViajante | Serviço de Perfil | PerfilDeViajanteValidado |
| CriarViagem | Viajante | ViagemCriada |
| DefinirOrcamentoDaViagem | Viajante | OrcamentoDefinido |
| CurarDestinosCompativeis | Serviço de Curadoria | DestinosCurados |
| GerarRoteiro | Serviço de Planejamento | RoteiroGerado |
| ConfirmarViagem | Viajante | ViagemConfirmada |
| IniciarViagem | Sistema (por data) ou Viajante | ViagemIniciada |
| RegistrarGasto | Viajante | GastoRegistrado |
| FinalizarViagem | Sistema (por data) ou Viajante | ViagemFinalizada |
| RegistrarFeedbackDaViagem | Viajante | FeedbackRegistrado |

---

## 4. Políticas e regras de negócio validadas

1. O período da viagem deve ser válido: data de início menor que data de fim.
2. Não é permitido confirmar ou iniciar viagem sem ao menos uma atividade no roteiro.
3. Não é permitido adicionar ou remover atividades quando a viagem estiver Finalizada.
4. O orçamento total não pode ser negativo.
5. Cada gasto deve ter valor positivo.
6. O total gasto deve ser a soma dos gastos registrados e não pode ultrapassar o orçamento total.
7. A transição Confirmada -> EmAndamento só pode ocorrer na data de início ou após ela.
8. A transição EmAndamento -> Finalizada só pode ocorrer após a data final.
9. Recursos premium de planejamento dependem de assinatura ativa.

---

## 5. Bounded contexts envolvidos

| Bounded Context | Responsabilidade principal | Eventos relevantes |
|---|---|---|
| Perfil do Viajante | Coletar e validar perfil de preferências | PreferenciasColetadas, PerfilDeViajanteValidado |
| Gestão de Destinos | Curadoria e manutenção de destinos | DestinosCurados |
| Planejamento de Viagem | Criação da viagem, roteiro, estado e orçamento | ViagemCriada, OrcamentoDefinido, RoteiroGerado, ViagemConfirmada, ViagemIniciada, GastoRegistrado, ViagemFinalizada |
| Faturamento e Assinatura | Gestão de plano e recursos premium | AssinaturaAtivada, AssinaturaExpirada |
| Mapas e Navegação | Rotas, geolocalização e clima | RotaCalculada, ClimaConsultado |

---

## 6. Integrações externas mapeadas

1. APIs de mapas e clima para enriquecer o roteiro.
2. APIs de passagens e destinos para opções de viagem.
3. Gateway de pagamento para assinatura premium.

---

## 7. Riscos e pontos de atenção

1. Mudanças tardias de preferência podem invalidar parte do roteiro já gerado.
2. Falha de integração externa não deve impedir persistência do estado principal da viagem.
3. Eventos de integração devem ser publicados após commit para evitar inconsistência entre contextos.

---

## 8. Critérios de validação do fluxo

1. Todo evento deve nascer de um comando identificado.
2. Todo comando deve ter ator responsável.
3. Regras críticas do agregado Viagem precisam estar refletidas nas transições de estado.
4. Eventos de integração não devem expor detalhes internos desnecessários do agregado.

