# Diagrama de Classes - Sistema de Clínica de Psicologia

```mermaid
classDiagram
    class Paciente {
        +int id
        +string nome
        +string cpf
        +string telefone
        +string email
        +date data_nascimento
        +string endereco
    }

    class Psicologo {
        +int id
        +string nome
        +string crp
        +string email
        +string telefone
        +string especialidade
    }

    class Consulta {
        +int id
        +date data
        +time horario
        +string status
        +string tipo
    }

    class Prontuario {
        +int id
        +date data_registro
        +string observacoes
        +string evolucao_clinica
    }

    class Pagamento {
        +int id
        +float valor
        +date data_pagamento
        +string metodo
        +string status
    }

    class Lembrete {
        +int id
        +string mensagem
        +date data_envio
        +string tipo
    }

    %% RELACIONAMENTOS
    Paciente "1" --> "n" Consulta : realiza >
    Psicologo "1" --> "n" Consulta : atende >
    Consulta "1" --> "1" Prontuario : gera >
    Consulta "1" --> "1" Pagamento : possui >
    Consulta "1" --> "n" Lembrete : envia >
