# Matriz de Rastreabilidade - Horizontal e Vertical

| Requisito | Fonte | Caso de Uso | Classe/Entidade | Status |
|------------|--------|--------------|-----------------|--------|
| RF01 - Agendar Consulta | Entrevista / Sistema Análogo | UC01 | Consulta | Implementado |
| RF02 - Cancelar Consulta | Entrevista | UC02 | Consulta | Implementado |
| RF03 - Registrar Prontuário | Psicólogo / LGPD | UC03 | Prontuario | Implementado |
| RF04 - Controlar Pagamentos | Secretária / Sistema Análogo | UC04 | Pagamento | Em Desenvolvimento |
| RF05 - Enviar Lembretes Automáticos | Sistema / Paciente | UC05 | Lembrete | Planejado |
| RNF01 - Conformidade LGPD | Lei 13.709/2018 | Todos | Todas | Implementado |
| RNF02 - Interface Responsiva | Requisitos de Usabilidade | UC01, UC02 | - | Planejado |

---

## Rastreabilidade Vertical

| Nível | Elemento | Relacionamento |
|--------|-----------|----------------|
| Objetivo de Negócio | Melhorar gestão de atendimentos | Deriva → RF01, RF02 |
| Requisito Funcional | RF01 Agendar Consulta | Implementado em → UC01 |
| Caso de Uso | UC01 Agendar Consulta | Associado à classe → Consulta |
| Código | Classe Consulta / Controller Agenda | Implementa → UC01 |
