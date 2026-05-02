# Visão da Demanda (VD) - Sistema ENADE Comentado (SEC)

## Histórico de Versões

| Data | Versão | Descrição | Autor |
| :--- | :--- | :--- | :--- |
| 02/05/2026 | 1.0 | Criação do documento de visão e definição do escopo inicial | Juliana |

## 1. Objetivo

Definir a proposta de valor e o escopo do sistema de questões comentadas do ENADE, detalhando as necessidades dos estudantes de graduação, coordenações de curso e professores. O projeto foca na aplicação da engenharia de requisitos para especificar uma solução web/mobile que auxilie no preparo para o exame.

## 2. Proposta de valor

O sistema permitirá democratizar o acesso a materiais de estudo de alta qualidade, oferecendo uma plataforma organizada para a prática de simulados com feedback imediato. Espera-se uma melhoria significativa no desempenho dos estudantes e o fornecimento de indicadores reais de qualidade para a gestão acadêmica.

## 3. Descrição da demanda

A demanda surge da dificuldade enfrentada pelos estudantes em se preparar para o ENADE devido à escassez de materiais organizados e simulados práticos. O sistema funcionará como um hub educacional para:
* Prática de **simulados cronometrados**.
* Consulta de **gabaritos detalhados e comentados**.
* Acompanhamento de **estatísticas de desempenho** por área de conhecimento.
* Interação colaborativa através de **fóruns de discussão**.

Todo o processo será digital, com autenticação de usuários e histórico de simulados e comentários.

Permitirá também ao estudante consultar o banco de questões por área de conhecimento, bem como o acompanhamento de sua evolução pedagógica.

Não está no escopo dessa demanda a emissão de certificados oficiais de conclusão de curso ou a inscrição formal no exame junto ao MEC.

## 4. Partes interessadas

| Nome | Papel | Responsabilidades | Representante |
| :--- | :--- | :--- | :--- |
| **Estudante** | Usuário Final | Realizar simulados, consultar gabaritos e interagir no fórum. | - |
| **Coordenação de Curso** | Cliente | Acompanhar indicadores de desempenho e evolução das turmas. | - |
| **Professores** | Stakeholder | Prover apoio pedagógico e validar comentários técnicos. | - |
| **Equipe de TI** | Desenvolvimento | Implementar e manter o sistema. | - |
| **INEP** | Fornecedor | Prover a base oficial de questões e gabaritos. | - |

## 5. Personas

### 5.1. Aluno concluinte
- **Descrição:** Aluno matriculado em curso de ensino superior que deve realizar o ENADE como componente curricular obrigatório.
- **Objetivo:** Praticar com questões reais, entender erros através de comentários e monitorar sua evolução por área de conhecimento.

### 5.2. Coordenador de curso
- **Descrição:** Responsável pela gestão acadêmica do curso de graduação
- **Objetivo:** Identificar lacunas de aprendizado no corpo discente através das estatísticas de desempenho fornecidas pelo sistema

### 5.3. Professor
- **Descrição:** Docente especialista responsável por prover apoio pedagógico e técnico aos estudantes na plataforma.
- **Objetivo:** Inserir comentários técnicos nas questões e sanar dúvidas acadêmicas dos alunos nos fóruns de discussão.

### 5.4. Administrador
- **Descrição:** Integrante da equipe de suporte técnico.
- **Objetivo:** Manter o banco de questões atualizado conforme as publicações do INEP, gerenciar permissões de usuários e moderar fóruns de discussão.

## 6. Necessidades e funcionalidades

### Necessidade 1: Prática e simulação de exame

#### F1.1 Realização de simulados cronometrados
* **Descrição:** Permite realizar testes com tempo limitado para simular a experiência real do exame.
* **Incluída**
* **Atores:** Estudante
* **Frequência:** Alta
* **Valor:** Alto

#### F1.2 Seleção de questões por filtro
* **Descrição:** Filtro por ano, curso e tipo de componente (Formação Geral ou Conhecimento Específico).
* **Incluída**
* **Atores:** Estudante
* **Frequência:** Média
* **Valor:** Médio

---

### Necessidade 2: Feedback e estudo dirigido

#### F2.1 Exibição de gabarito comentado
* **Descrição:** Apresenta explicações detalhadas sobre a resposta correta e as incorretas.
* **Incluída**
* **Atores:** Estudante
* **Frequência:** Alta
* **Valor:** Alto

#### F2.2 Fórum de discussão por questão
* **Descrição:** Espaço para troca de conhecimento e dúvidas entre usuários em cada item do banco.
* **Incluída**
* **Atores:** Estudante, Professor
* **Frequência:** Média
* **Valor:** Médio

---

### Necessidade 3: Monitoramento de desempenho

#### F3.1 Painel de estatísticas individuais
* **Descrição:** Gráficos de desempenho por área de conhecimento para o aluno.
* **Incluída**
* **Atores:** Estudante
* **Frequência:** Média
* **Valor:** Alto

#### F3.2 Relatório gerencial de turmas
* **Descrição:** Visão consolidada para a coordenação identificar lacunas de aprendizagem.
* **Incluída**
* **Atores:** Coordenador
* **Frequência:** Média
* **Valor:** Alto

---

### Necessidade 4: Gestão de acesso e dados

#### F4.1 Autenticação e Perfil
* **Descrição:** Login seguro para diferenciar estudantes, professores, coordenador e administrador.
* **Incluída**
* **Atores:** Todos os usuários
* **Frequência:** Alta
* **Valor:** Alto

#### F4.2 Manutenção do banco de questões
* **Descrição:** Permite cadastrar, editar e organizar questões do portal INEP.
* **Incluída**
* **Atores:** Administrador
* **Frequência:** Baixa
* **Valor:** Médio

## 7. Arquitetura da demanda

### Descrição da arquitetura

O sistema será uma aplicação **web e mobile**, estruturada para suportar alta escalabilidade de dados (banco de questões).

#### 1. Frontend
* Acesso via navegador e dispositivos móveis
* Interfaces para: Estudante, professor, coordenador e administrador

#### 2. Backend
Responsável pela lógica de negócio e regras do sistema:
* Módulo de gestão de conteúdo (questões)
* Módulo de avaliação e simulação
* Módulo de colaboração (fórum)
* Módulo pedagógico (gabaritos)
* Módulo analítico e estatístico
* Módulo de segurança e autenticação

#### 3. Banco de dados
Armazena informações como:
* Questões
* Gabaritos
* Usuários
* Comentários
* Histórico de simulados

---

## Checklist de Validação do Documento de Visão

- [X] O objetivo está claro e alinhado ao problema/necessidade? 
- [X] A proposta de valor é mensurável e relevante? 
- [X] Todas as partes interessadas estão listadas com papéis definidos? 
- [X] Existem pelo menos duas personas descritas?
- [X] Todas as necessidades e funcionalidades estão relacionadas a atores? 
- [X] Há indicação de valor e frequência para cada funcionalidade?
- [ ] A arquitetura está ilustrada (através de diagramas UML em anexo)? 
- [X] O documento está escrito em linguagem clara e objetiva?
