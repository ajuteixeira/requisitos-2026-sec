# Especificação de Requisitos Não Funcionais - Sistema ENADE Comentado (SEC)

## Histórico de Versões

| Data       | Versão | Descrição                                                           | Autor     |
| ---------- | ------ | ------------------------------------------------------------------- | --------- |
| 15/05/2026 | 1.0    | Preenchimento inicial dos RNFs com base no Documento de Visão v1.3 | Juliana |

## 1. Requisitos de Produto

### 1.1. Eficiência de Desempenho

#### 1.1.1. Comportamento temporal

- **RNF-001 (Tempo de Resposta de Questões):** O sistema deve carregar o texto, alternativas e o gabarito comentado (F2.1) de uma questão em menos de 1,5 segundos sob condições normais de rede.
- **RNF-002 (Abertura de Simulados):** O início e a renderização da interface de um simulado cronometrado (F1.1) não devem exceder 3 segundos após o comando do estudante.

#### 1.1.2. Capacidade

- **RNF-003 (Usuários Simultâneos):** A infraestrutura deve suportar um mínimo de 500 usuários simultâneos realizando simulados ativamente (F1.1) sem degradação do tempo de resposta acima de 3 segundos.
- **RNF-004 (Volume do Banco de Questões):** O banco de dados SEC_BD deve ser dimensionado para armazenar e indexar eficientemente até 50.000 questões com comentários técnicos de mídia (texto e imagens).

#### 1.1.3. Uso de recursos

- **RNF-005 (Consumo no Cliente):** A aplicação SECFrontEnd (React) não deve consumir mais de 150MB de memória RAM no navegador da máquina do cliente durante a execução de simulados.

### 1.2. Flexibilidade (portabilidade)

#### 1.2.1. Escalabilidade

- **RNF-006 (Escalonamento Vertical/Horizontal):** A API construída em Node.js alocada na AWS Cloud deve possuir políticas de _Auto Scaling_ para lidar com picos de tráfego, comuns em períodos que antecedem a prova oficial do ENADE.

#### 1.2.2. Adaptabilidade

- **RNF-007 (Responsividade):** A interface web do sistema deve ser 100% responsiva, adaptando-se perfeitamente a resoluções de telas de smartphones (mínimo de 360px de largura) até monitores desktop (1080p ou superior).

#### 1.2.3. Instalabilidade

- **RNF-008 (Arquitetura Web - Zero Instalação):** O SECFrontEnd não exigirá nenhuma instalação local na máquina do cliente, sendo acessível por meio de qualquer navegador web moderno atualizado (Chrome, Firefox, Edge, Safari).

#### 1.2.4. Substituibilidade

- Não se aplica.

### 1.3. Confiabilidade

#### 1.3.1. Maturidade

- **RNF-009 (Taxa de Erro em Produção):** O sistema deve apresentar uma taxa de falhas/erros críticos de software (ex.: Erro 500) inferior a 0,5% do total de requisições HTTP em um período de 30 dias operacionais.

#### 1.3.2. Disponibilidade

- **RNF-010 (SLA de Disponibilidade):** O sistema hospedado na AWS deve garantir uma disponibilidade mínima de 99,5% do tempo (Uptime), calculada mensalmente (7x24).

#### 1.3.3. Tolerância a falhas

- **RNF-011 (Persistência do Progresso):** Em caso de queda abrupta de conexão de internet do Aluno Concluinte durante um simulado cronometrado (F1.1), o sistema deve salvar localmente (ex.: _LocalStorage_) ou no banco as respostas já assinaladas, permitindo retomar o teste de onde parou sem perda de dados após o restabelecimento.

#### 1.3.4. Recuperabilidade

- **RNF-012 (Políticas de Backup):** O banco de dados SEC_BD (PostgreSQL) deve possuir rotinas automatizadas de backup incremental diário e backup completo semanal, com tempo máximo de recuperação (RTO) de até 4 horas em caso de desastre.

### 1.4. Segurança

#### 1.4.1. Confidencialidade

- **RNF-013 (Criptografia em Trânsito):** Todo o tráfego de dados entre a Máquina do Cliente e a AWS Cloud deve obrigatoriamente utilizar criptografia por meio do protocolo HTTPS (TLS 1.3).
- **RNF-014 (Criptografia em Repouso):** As senhas dos usuários e dados sensíveis devem ser armazenadas no Postgres utilizando algoritmos de hash seguros (ex.: BCrypt).

#### 1.4.2. Integridade

- **RNF-015 (Prevenção de Injeção de Dados):** A API Node.js deve implementar mecanismos de sanitização de dados e _Prepared Statements_ contra vulnerabilidades como SQL Injection e Cross-Site Scripting (XSS), protegendo o fórum (F2.2) e o cadastro de questões (F4.3).

#### 1.4.3. Não repúdio

- **RNF-016 (Log de Auditoria):** O sistema deve registrar em logs imutáveis todas as ações de inserção, edição ou exclusão de questões realizadas por Administradores (F4.2) e Professores (F4.3), vinculando a ação ao ID autenticado do usuário e carimbo de data/hora (Timestamp).

#### 1.4.4. Autenticidade (autenticação)

- **RNF-017 (Controle de Acesso Baseado em Perfis - RBAC):** O sistema deve validar via tokens seguros (ex.: JWT) o nível de acesso (Estudante, Professor, Coordenador, Administrador) em cada requisição para impedir privilégios indevidos (ex.: um Estudante tentando acessar o relatório de turmas F3.2).

#### 1.4.5. Resistência

- **RNF-018 (Proteção contra Brute Force):** O endpoint de Autenticação (F4.1) deve bloquear temporariamente (por 15 minutos) o login de um endereço IP após 5 tentativas consecutivas de acesso incorretas.

### 1.5. Privacidade

#### 1.5.1. Licitude

- **RNF-019 (Conformidade com a LGPD):** O tratamento de dados cadastrais de alunos e professores pelo SEC deve estar em total conformidade com a Lei Geral de Proteção de Dados (Lei nº 13.709/2018), exigindo o aceite explícito de um Termo de Consentimento no primeiro acesso.

#### 1.5.2. Finalidade

- **RNF-020 (Escopo do Tratamento):** Os dados coletados serão utilizados estritamente para fins pedagógicos de preparação para o ENADE (cálculo de estatísticas de evolução F3.1 e relatórios institucionais F3.2).

#### 1.5.3. Necessidade

- **RNF-021 (Minimização de Dados):** O sistema exigirá apenas as informações estritamente necessárias para o login e vinculação acadêmica (Nome, E-mail institucional, Matrícula e Curso).

#### 1.5.4. Tratamento

- **RNF-022 (Exclusão de Dados):** O usuário poderá solicitar a inativação de seu perfil, garantindo que suas interações textuais no fórum passem a ser exibidas de forma anônima ("Usuário Inativo") para preservar as discussões pedagógicas existentes.

### 1.6. Capacidade de Interação (UX, usabilidade e acessibilidade)

#### 1.6.1. Reconhecimento de adequação

- **RNF-023 (Identidade Visual):** A interface deve apresentar de forma clara logotipos institucionais e um cabeçalho identificando o SEC, permitindo que o usuário compreenda o propósito da plataforma nos primeiros 5 segundos de acesso.

#### 1.6.2. Facilidade de aprendizado (learnability)

- **RNF-024 (Autoexplicabilidade):** Um usuário Aluno Concluinte deve ser capaz de iniciar e concluir um simulado cronometrado no primeiro acesso sem a necessidade de ler manuais ou realizar treinamentos prévios.

#### 1.6.3. Operabilidade

- **RNF-025 (Padrões de Navegação):** O menu lateral ou superior deve fornecer acesso direto às principais funçõescom no máximo 2 cliques a partir da tela inicial.

#### 1.6.4. Proteção contra erros do usuário

- **RNF-026 (Confirmação de Ações Críticas):** O sistema deve exibir caixas de diálogo de confirmação (Modais) antes de o aluno "Finalizar Definitivamente o Simulado" ou antes de um professor "Excluir um rascunho de questão".

#### 1.6.5. Inclusividade (acessibilidade)

- **RNF-027 (Acessibilidade Web):** A interface em React deve seguir as diretrizes básicas da WCAG 2.1 (Web Content Accessibility Guidelines), oferecendo suporte a alto contraste e compatibilidade com leitores de tela padrão (como NVDA ou JAWS) para alunos com deficiência visual.

#### 1.6.6. Assistência ao usuário (acessibilidade)

- **RNF-028 (Mensagens de Erro Claras):** Em caso de falha de preenchimento ou validação de formulários (ex.: no cadastro de questões), o sistema deve apontar o campo exato do erro com instruções textuais claras, evitando códigos de erro técnicos e genéricos.

#### 1.6.7. Engajamento do usuário

- **RNF-029 (Estética Limpa):** O design de interface deve adotar uma estética limpa (_Clean Design Mindset_), minimizando distrações visuais nas telas de simulados para favorecer o foco na leitura e resolução das questões complexas do ENADE.

### 1.7. Manutenibilidade

#### 1.7.1. Modularidade

- **RNF-030 (Arquitetura desacoplada):** O projeto deve seguir rigidamente a separação entre a camada de apresentação e a camada de lógica de negócios, permitindo alterações visuais sem impactos no processamento de dados.

#### 1.7.2. Reusabilidade

- **RNF-031 (Componentização de UI):** No FrontEnd, elementos comuns de interface (Botões, Cards de Questões, Gráficos de Estatísticas e Cronômetros) devem ser criados como componentes genéricos reutilizáveis.

#### 1.7.3. Analisabilidade

- **RNF-032 (Rastreabilidade de Código/Erros):** O código-fonte backend deve implementar centralização de logs (ex.: utilizando bibliotecas como Winston ou serviços como AWS CloudWatch) para que comportamentos anômalos em produção possam ser analisados em poucos minutos.

#### 1.7.4. Modificabilidade

- **RNF-033 (Migração de Banco de Dados):** O banco de dados PostgreSQL deve utilizar ferramentas de _Database Migrations_ (ex.: Sequelize ou Knex.js) no código do repositório backend, garantindo alterações de esquema estruturadas, seguras e versionadas.

#### 1.7.5. Testabilidade

- **RNF-034 (Cobertura de Testes Automatizados):** A API Node.js deve conter testes unitários e de integração para os módulos de cálculo de notas dos simulados e permissões de perfis, cobrindo ao menos 70% das rotas críticas da aplicação.

### 1.8. Compatibilidade

#### 1.8.1. Interoperabilidade

- **RNF-035 (Padronização JSON):** A comunicação de dados entre o cliente e o servidor AWS deve ocorrer exclusivamente utilizando o formato JSON (JavaScript Object Notation), facilitando futuras integrações com sistemas acadêmicos das universidades.

#### 1.8.2. Coexistência

- **RNF-036 (Isolamento de Ambiente):** Por estar conteinerizado ou hospedado de forma independente em nuvem, o ecossistema do SEC não deve interferir no desempenho ou funcionamento de outros portais ou sistemas internos das instituições usuárias.

### 1.9. Segurança Operacional (safety)

#### 1.9.1. Restrição operacional

- Não se aplica.

#### 1.9.2. Identificação de riscos

- Não se aplica.

#### 1.9.3. Segurança contra falhas (fail-safe)

- **RNF-037 (Travamento de Cronômetro Seguro):** Se o servidor do SEC falhar ou perder comunicação durante um simulado em andamento, o cronômetro do cliente não deve punir o aluno com encerramento forçado por tempo esgotado na próxima reconexão; o estado deve ser congelado até a validação do servidor.

#### 1.9.4. Aviso de perigo

- Não se aplica.

#### 1.9.5. Integração segura

- Não se aplica.

### 1.10. Adequação funcional

#### 1.10.1. Completude funcional

- **RNF-038 (Alinhamento ao Escopo):** O sistema entregará todas as funcionalidades previstas na VD v1.3 (F1.1 à F4.4), cobrindo de ponta a ponta a esteira de estudos, comentários e gestão de conteúdo.

#### 1.10.2. Corretude funcional

- **RNF-039 (Precisão Estatística):** Os cálculos do painel de desempenho individual (F3.1) e dos relatórios gerenciais das turmas (F3.2) devem ser matematicamente exatos em relação às fórmulas de proporção de acertos por áreas de conhecimento do ENADE.

#### 1.10.3. Adequação funcional

- **RNF-040 (Fidelidade ao Padrão INEP):** Os formulários de cadastro de questões (F4.2 e F4.3) devem conter campos estruturados específicos (Texto base, Imagem de suporte, Enunciado, Asserções e Justificativa/Comentário Técnico) para induzir os professores a seguir rigorosamente o padrão de avaliação oficial fornecido pelo INEP.

## 2. Requisitos Externos

### 2.1. Ético

- **RNF-041 (Código de Conduta nos Fóruns):** A plataforma deve exibir os termos de uso ético antes do primeiro envio de mensagem nos Fóruns por Questão (F2.2), proibindo termos ofensivos, plágio de gabaritos e compartilhamento de materiais externos protegidos por direitos autorais.

### 2.2. Regulatório

- **RNF-042 (Padrões INEP):** As taxonomias de classificação de áreas de conhecimento, cursos e componentes (Formação Geral vs. Conhecimento Específico) inseridas no banco devem seguir fielmente as diretrizes e manuais técnicos oficiais publicados periodicamente pelo INEP/MEC.

### 2.3. Legislativo

- **RNF-043 (Legislação de Acessibilidade):** O software web deve respeitar as exigências estabelecidas na Lei Brasileira de Inclusão da Pessoa com Deficiência (Lei nº 13.146/2015) no que tange ao acesso a plataformas digitais educacionais.

## 3. Requisitos Organizacionais

### 3.1. Ambientais

- **RNF-044 (Hospedagem):** Toda a camada de processamento de backend e armazenamento persistente deve estar localizada na região `sa-east-1` (São Paulo) da AWS, visando a redução de latência para os usuários finais situados no Brasil.

### 3.2. Operacionais

- **RNF-045 (Janela de Manutenção):** Atualizações de software planejadas no ambiente de produção devem ser efetuadas obrigatoriamente fora do horário comercial e de pico acadêmico, preferencialmente entre as 23h00 e as 05h00 (horário de Brasília).

### 3.3. Desenvolvimento

- **RNF-046 (Stack Tecnológica Obrigatória):** O desenvolvimento do sistema deve obedecer à pilha tecnológica homologada e desenhada nos diagramas UML da arquitetura da demanda: FrontEnd construído em **React**, BackEnd utilizando **Node.js** e o Banco de Dados Relacional **PostgreSQL**.
- **RNF-047 (Versionamento):** O código-fonte completo deve ser versionado em repositório privado utilizando Git, seguindo uma estratégia de ramificação organizada (ex.: _GitFlow_).

## 4. Checklist de Validação do Artefato (RNF)

### 4.1. Estrutura e escopo

- [x] O documento possui histórico de versões preenchido.
- [x] O escopo da solução está claro no documento.
- [x] Há requisitos registrados nas seções aplicáveis (produto, externos e organizacionais).
- [x] Requisitos não aplicáveis estão explicitamente marcados como "Não se aplica", quando necessário.

### 4.2. Qualidade dos requisitos

- [x] Cada requisito está escrito de forma objetiva e verificável.
- [x] Cada requisito possui critério mensurável (tempo, percentual, limite, condição ou evidência).
- [x] Não há requisito ambíguo com termos vagos (ex.: "rápido", "seguro", "fácil") sem métrica.
- [x] Requisitos duplicados ou conflitantes foram eliminados.

### 4.3. Conformidade e rastreabilidade

- [x] Requisitos regulatórios/legais relevantes foram registrados.
- [x] Requisitos de privacidade e segurança foram contemplados quando aplicáveis.
- [x] Os requisitos estão alinhados com visão da demanda, glossário e casos de uso.
- [x] Existe rastreabilidade dos requisitos para fontes de negócio, norma ou decisão técnica.

### 4.4. Prontidão para uso

- [x] Os requisitos podem ser usados como base para implementação e testes.
- [x] Há insumos suficientes para criar critérios de aceitação.
- [x] O documento foi revisado por pares.
- [x] A versão está pronta para aprovação/publicação.
