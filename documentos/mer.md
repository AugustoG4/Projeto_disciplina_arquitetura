erDiagram
    PACIENTE {
        int id_paciente PK
        string nome
        string cpf
        string telefone
        string email
        date data_nascimento
        string endereco
    }

    PSICOLOGO {
        int id_psicologo PK
        string nome
        string crp
        string email
        string telefone
        string especialidade
    }

    CONSULTA {
        int id_consulta PK
        date data
        string horario
        string status
        string tipo
        int id_paciente FK
        int id_psicologo FK
    }

    PRONTUARIO {
        int id_prontuario PK
        date data_registro
        string observacoes
        string evolucao_clinica
        int id_consulta FK
    }

    PAGAMENTO {
        int id_pagamento PK
        float valor
        date data_pagamento
        string metodo
        string status
        int id_consulta FK
    }

    LEMBRETE {
        int id_lembrete PK
        string mensagem
        date data_envio
        string tipo
        int id_consulta FK
    }

    PACIENTE ||--o{ CONSULTA : "realiza"
    PSICOLOGO ||--o{ CONSULTA : "atende"
    CONSULTA ||--|| PRONTUARIO : "gera"
    CONSULTA ||--|| PAGAMENTO : "possui"
    CONSULTA ||--o{ LEMBRETE : "envia"
