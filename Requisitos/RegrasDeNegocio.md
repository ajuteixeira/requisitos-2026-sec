# Regras de negócio da solução (RN) - Sistema ENADE Comentado (SEC)

## Contexto

Este documento apresenta as regras de negócio essenciais para o funcionamento do sistema, cobrindo o núcleo de simulados, fóruns e a gestão do acervo de questões:

- F1.1 Realização de simulados cronometrados
- F2.2 Fórum de discussão por questão
- F4.3 Cadastro de questões por área e curso

## Histórico de Versões

| Data       | Versão | Descrição                                                            | Autor   |
| :--------- | :----- | :------------------------------------------------------------------- | :------ |
| 18/05/2026 | 1.0    | Criação das regras essenciais e mapeamento de funcionalidades do SEC | Juliana |

## Regras de Negócio

### RN1. O cadastro de questões exige estrutura padrão INEP

- **Identificador:** RN1
- **Regra:** A publicação de uma questão por professor ou administrador somente é concluída se os campos obrigatórios (texto base, enunciado, asserções e justificativa técnica) estiverem preenchidos.
- **Critério verificável:** O sistema deve impedir a gravação e exibir um alerta indicando o campo ausente caso a estrutura esteja incompleta.

### RN2. O sistema limita a manutenção de questões à área e curso do professor

- **Identificador:** RN2
- **Regra:** O professor pode visualizar, cadastrar, editar e excluir apenas questões que estejam diretamente vinculadas ao seu respectivo curso e área de conhecimento.
- **Critério verificável:** O sistema deve bloquear a operação e gerar uma mensagem de erro se o identificador do curso da questão for diferente da área de atuação do professor autenticado.

### RN3. O sistema restringe o acesso aos fóruns por vinculação acadêmica

- **Identificador:** RN3
- **Regra:** Alunos concluintes e professores acessam exclusivamente os fóruns de discussão das questões pertencentes ao seu próprio curso e área.
- **Critério verificável:** O sistema deve negar a exibição e bloquear a postagem no fórum caso o usuário não possua a mesma vinculação de curso da questão correspondente.

### RN4. O cronômetro do simulado congela em falhas de conexão

- **Identificador:** RN4
- **Regra:** O tempo restante do simulado para de contar na interface do aluno se houver perda de comunicação ativa ou queda de rede com o servidor.
- **Critério verificável:** Ao detectar a desconexão, a interface deve pausar o cronômetro imediatamente e impedir o encerramento forçado por tempo esgotado até o restabelecimento do sinal.

### RN5. O sistema registra trilha de auditoria em operações críticas

- **Identificador:** RN5
- **Regra:** As ações de inserção, alteração ou exclusão de questões no acervo geram logs imutáveis de segurança vinculando o autor ao evento.
- **Critério verificável:** O sistema deve gravar no banco de logs o ID do usuário autenticado, o tipo de operação realizada e o carimbo de data/hora (Timestamp) a cada modificação do acervo.
