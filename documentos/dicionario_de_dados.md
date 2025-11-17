# Dicionário de Dados — Sistema de Gestão da Clínica de Psicologia

## Sigla e Nome do Projeto  
**SGCP — Sistema de Gestão da Clínica de Psicologia**

---

# 1. Introdução  

Este documento apresenta o **Dicionário de Dados** do Sistema de Gestão da Clínica de Psicologia (SGCP), descrevendo detalhadamente:

- as **entidades** do Modelo Entidade-Relacionamento (MER);
- os **atributos**, seus **tipos**, **cardinalidades** e **restrições**;
- os **relacionamentos** existentes entre as entidades.

### Notação Utilizada

- O diagrama conceitual usa **Diagrama de Classes UML** e **Modelo Entidade-Relacionamento (notação Chen)**.  
- As **cardinalidades** seguem a semântica participativa do template oficial.
- Os tipos de domínio utilizam as convenções:

| Tipo | Descrição |
|------|-----------|
| Char(t) | Cadeia de caracteres de tamanho t |
| Int(i) | Número inteiro de i dígitos |
| Decimal(i,d) | Número com i casas, d decimais |
| Data | Data (AAAA-MM-DD) |
| DataHora | Data e hora completas |
| Booleano | Verdadeiro/Falso |
| Enum | Lista de valores pré-definidos |
| Binário(n) | Arquivo binário até n MB |

---

# 2. Diagrama Conceitual de Dados  
```mermaid
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
    ```

---

# 3. Convenções do Dicionário

- As entidades aparecem **em ordem alfabética**.  
- Depois, os relacionamentos também estão **em ordem alfabética**.  
- *Card* indica o número mínimo e máximo de valores para o atributo.

---

# 4. Entidades

---

## Entidade: **Paciente**

Representa um paciente que agenda consultas, recebe lembretes e realiza pagamentos.

### Restrições Gerais
- CPF é único.  
- Dados pessoais devem estar em conformidade com a **LGPD**.

### Atributos

| Mnemônico | Nome Completo | Tipo | Card | Restrições |
|-----------|----------------|-------|-------|-------------|
| idPaciente | Identificador do paciente | Int(6) | (1,1) | PK |
| nmPaciente | Nome completo | Char(120) | (1,1) | — |
| cpfPaciente | CPF | Char(11) | (1,1) | Único |
| telPaciente | Telefone | Char(15) | (0,1) | — |
| emailPaciente | Email | Char(120) | (0,1) | Deve ser válido |
| dtNascimento | Data de nascimento | Data | (0,1) | — |
| enderecoPaciente | Endereço | Char(255) | (0,1) | — |

---

## Entidade: **Psicologo**

Profissional que realiza atendimentos e registra os prontuários.

### Restrições Gerais
- CRP é obrigatório e deve ser único.

### Atributos

| Mnemônico | Nome Completo | Tipo | Card | Restrições |
|-----------|----------------|-------|-------|-------------|
| idPsicologo | Identificador | Int(6) | (1,1) | PK |
| nmPsicologo | Nome | Char(120) | (1,1) | — |
| crpPsicologo | CRP | Char(15) | (1,1) | Único |
| telPsicologo | Telefone | Char(15) | (0,1) | — |
| emailPsicologo | Email | Char(120) | (0,1) | — |
| especialidade | Especialidade | Char(120) | (0,1) | — |

---

## Entidade: **Consulta**

Atendimento agendado entre paciente e psicólogo.

### Restrições Gerais
- Uma consulta tem um único paciente e um único psicólogo.

### Atributos

| Mnemônico | Nome Completo | Tipo | Card | Restrições |
|-----------|----------------|-------|-------|-------------|
| idConsulta | Identificador | Int(6) | (1,1) | PK |
| dtConsulta | Data | Data | (1,1) | — |
| hrConsulta | Horário | Char(5) | (1,1) | HH:MM |
| statusConsulta | Status | Enum {agendada, cancelada, realizada} | (1,1) | — |
| tipoConsulta | Tipo | Enum {presencial, online} | (1,1) | — |
| idPaciente | Paciente vinculado | Int(6) | (1,1) | FK |
| idPsicologo | Psicólogo vinculado | Int(6) | (1,1) | FK |

---

## Entidade: **Prontuario**

Registro clínico da sessão.

### Restrições Gerais
- O prontuário é único por consulta.

### Atributos

| Mnemônico | Nome Completo | Tipo | Card | Restrições |
|-----------|----------------|-------|-------|-------------|
| idProntuario | Identificador | Int(6) | (1,1) | PK |
| dtRegistro | Data de registro | DataHora | (1,1) | — |
| observacoes | Observações | Char(*) | (0,1) | — |
| evolucaoClinica | Evolução clínica | Char(*) | (0,1) | Conteúdo sensível |
| idConsulta | Consulta associada | Int(6) | (1,1) | FK |

---

## Entidade: **Pagamento**

Controla recebimentos associados às consultas.

### Atributos

| Mnemônico | Nome Completo | Tipo | Card | Restrições |
|-----------|----------------|-------|-------|-------------|
| idPagamento | Identificador | Int(6) | (1,1) | PK |
| valorPago | Valor | Decimal(10,2) | (1,1) | Não negativo |
| dtPagamento | Data do pagamento | Data | (0,1) | — |
| metodoPagamento | Método | Enum {pix, credito, debito, dinheiro} | (1,1) | — |
| statusPagamento | Status | Enum {pago, pendente} | (1,1) | — |
| idConsulta | Consulta vinculada | Int(6) | (1,1) | FK |

---

## Entidade: **Lembrete**

Mensagem enviada ao paciente automaticamente.

### Atributos

| Mnemônico | Nome | Tipo | Card | Restrições |
|-----------|-------|--------|--------|-------------|
| idLembrete | Identificador | Int(6) | (1,1) | PK |
| mensagem | Mensagem | Char(255) | (1,1) | — |
| dtEnvio | Data de envio | DataHora | (1,1) | — |
| tipoLembrete | Tipo | Enum {consulta, pagamento} | (1,1) | — |
| idConsulta | Consulta relacionada | Int(6) | (1,1) | FK |

---

# 5. Relacionamentos

---

## Relacionamento: **Paciente realiza Consulta**

- Um paciente pode realizar várias consultas.  
- Uma consulta é sempre de um único paciente.  
- **Sem atributos próprios.**

---

## Relacionamento: **Psicólogo atende Consulta**

- Um psicólogo pode atender várias consultas.  
- Uma consulta pertence a um único psicólogo.  
- **Sem atributos próprios.**

---

## Relacionamento: **Consulta gera Prontuario**

- 1:1  
- **Sem atributos próprios.**

---

## Relacionamento: **Consulta possui Pagamento**

- 1:1  
- **Sem atributos próprios.**

---

## Relacionamento: **Consulta envia Lembrete**

- 1:N  
- **Sem atributos próprios.**

---

