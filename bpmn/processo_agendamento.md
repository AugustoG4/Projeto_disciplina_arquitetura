flowchart TB
A[Paciente solicita agendamento] --> B{Disponibilidade?}

B -- Sim --> C[Agendamento criado]

B -- Não --> D[Oferecer opções alternativas]

D --> A

C --> E[Enviar confirmação e lembretes]

E --> F[Paciente comparece?]

F -- Sim --> G[Atendimento - presencial ou teleconsulta]

F -- Não --> H[Registrar falta / notificar financeiro]

G --> I[Registrar sessão no prontuário]

I --> J[Gerar cobrança / registrar pagamento]

J --> K[Fim]

H --> K
