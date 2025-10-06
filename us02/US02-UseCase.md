# US02 - (Título do Objetivo da User Story)

## 1. Descrição
Como <tipo de utilizador> quero <objetivo> para <benefício>.

Exemplo:
Como Operador quero consultar e atualizar o estado de uma Entidade X para garantir que a informação está atualizada.

## 2. Atores
- Utilizador (Primário)
- Sistema Externo (se existir)

## 3. Stakeholders e Interesses
- Utilizador: Realizar a ação rapidamente e com feedback claro.
- Organização: Manter integridade e rastreabilidade dos dados.

## 4. Pré-condições
- Utilizador autenticado.
- Entidade alvo existe (ou critério de pesquisa válido).

## 5. Pós-condições
- Dados atualizados (em caso de sucesso).
- Operação registada em log/audit (se aplicável).

## 6. Trigger
Utilizador seleciona a opção "Executar US02" na interface.

## 7. Fluxo Principal (SUCESSO)
1. Utilizador inicia a operação US02.
2. Sistema solicita dados necessários.
3. Utilizador fornece dados.
4. Sistema valida dados.
5. Sistema obtém informação complementar na BD.
6. Sistema processa regras de negócio.
7. Sistema persiste alterações/resultados.
8. Sistema apresenta confirmação ao utilizador.

## 8. Fluxos Alternativos
A1 - Dados inválidos:
  4a. Validação falha.  
  4b. Sistema apresenta lista de erros.  
  4c. Utilizador corrige e volta ao passo 3.

A2 - Registo não encontrado:
  5a. Sistema não encontra dados.  
  5b. Informa utilizador.  
  5c. Caso aplicável pode tentar nova pesquisa (volta ao passo 2) ou termina.

A3 - Conflito (concorrência):
  7a. Outro utilizador alterou entretanto.  
  7b. Sistema informa conflito e apresenta versão atual.  
  7c. Utilizador decide reenviar (volta ao passo 6) ou cancelar.

## 9. Fluxos de Exceção
E1 - Erro de BD:
  - Sistema regista erro técnico.
  - Mensagem genérica apresentada.

E2 - Serviço externo indisponível:
  - Sistema cancela operação e informa indisponibilidade.

## 10. Regras de Negócio (exemplos)
- RB01: Campos obrigatórios: A, B, C.
- RB02: Estado só pode transitar de PENDENTE -> ATIVO -> ARQUIVADO.
- RB03: Operação auditável (guardar timestamp, userId).

## 11. Requisitos Não Funcionais
- Tempo de resposta < 2s (95% das vezes).
- Log de erros centralizado.
- Aderente a RGPD (se houver dados pessoais).

## 12. Critérios de Aceitação (exemplos)
- CA01: Dado válido -> operação concluída apresenta mensagem "Atualizado com sucesso".
- CA02: Campo obrigatório em falta -> mensagem específica listada.
- CA03: Tentativa de editar registo inexistente -> mensagem "Não encontrado".
- CA04: Conflito concorrente -> apresenta versão atual e não sobrescreve automaticamente.

## 13. Dados / Campos (exemplos)
| Campo | Tipo | Obrigatório | Observações |
|-------|------|-------------|------------|
| id | UUID | Sim | Identificador |
| estado | Enum | Sim | {PENDENTE, ATIVO, ARQUIVADO} |
| descricao | Texto | Não | Máx 255 |
| atualizadoPor | UUID | Automático | Preenchido pelo sistema |

## 14. Questões em Aberto
- Quais estados efetivamente?
- Existe aprovação em duas fases?
- Notificação a outros sistemas?

## 15. Notas
Adaptar termos ao domínio real do projeto.