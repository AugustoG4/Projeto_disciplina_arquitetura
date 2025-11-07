# EOR - Especificação de Objetivos e Requisitos (IEEE 830)

## 1. Introdução
### 1.1 Propósito
Definir os objetivos, requisitos e funcionalidades do sistema da clínica de psicologia.

### 1.2 Escopo
O sistema auxiliará no agendamento de consultas, registro de atendimentos, controle de pagamentos e envio de notificações.

### 1.3 Referências
- LGPD (Lei nº 13.709/2018)
- IEEE 830
- PsicoManager (sistema análogo)

---

## 2. Descrição Geral
### 2.1 Perspectiva do Produto
Sistema web modular que centraliza operações clínicas.

### 2.2 Funções do Sistema
- Agendar e cancelar consultas
- Registrar prontuários
- Gerenciar pagamentos
- Enviar lembretes automáticos

### 2.3 Características dos Usuários
Usuários com conhecimento básico em informática (pacientes, psicólogos, secretárias).

### 2.4 Restrições
- Deve seguir a LGPD
- Deve operar em navegadores modernos

---

## 3. Requisitos Específicos

### 3.1 Requisitos Funcionais
| ID | Descrição | Prioridade |
|----|------------|------------|
| RF01 | Permitir agendar consulta | Alta |
| RF02 | Permitir cancelar consulta | Alta |
| RF03 | Registrar prontuário | Alta |
| RF04 | Controlar pagamentos | Média |
| RF05 | Enviar lembretes automáticos | Média |

### 3.2 Requisitos Não Funcionais
| ID | Descrição | Prioridade |
|----|------------|------------|
| RNF01 | Cumprir LGPD | Alta |
| RNF02 | Interface responsiva | Alta |
| RNF03 | Criptografia de dados | Alta |
| RNF04 | Backup diário | Média |
| RNF05 | Tempo de resposta ≤ 2s | Média |
