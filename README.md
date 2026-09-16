# EduQuest

## Plataforma Educacional Gamificada com Aprendizagem Adaptativa

EduQuest é uma plataforma educacional gamificada projetada para transformar o processo de aprendizagem em uma experiência interativa, progressiva e personalizada.

A plataforma combina conteúdo educacional, gamificação, avaliações adaptativas, inteligência artificial e acompanhamento familiar em um ecossistema integrado para Web e Android.

O objetivo é criar uma experiência na qual o aluno possa aprender, praticar, evoluir e acompanhar seu próprio progresso enquanto responsáveis possuem ferramentas para acompanhar o desenvolvimento educacional.

---

# 1. Visão do produto

O EduQuest será estruturado como um ambiente de aprendizagem baseado em progressão.

O aluno poderá:

* realizar uma avaliação diagnóstica;
* receber um perfil inicial de aprendizagem;
* estudar diferentes disciplinas;
* resolver desafios;
* acumular XP;
* subir de nível;
* receber moedas e estrelas;
* desbloquear conteúdos;
* personalizar seu avatar;
* conquistar recompensas;
* participar de missões;
* acompanhar sua evolução;
* receber recomendações personalizadas;
* utilizar um tutor baseado em inteligência artificial.

A experiência deverá combinar elementos educacionais com mecânicas de jogos sem permitir que a gamificação substitua o objetivo pedagógico.

---

# 2. Disciplinas

A primeira versão deverá contemplar:

* Matemática
* Português
* Biologia
* Física
* Química

A arquitetura deverá permitir a inclusão futura de novas disciplinas sem necessidade de alteração estrutural significativa do sistema.

---

# 3. Modelo de aprendizagem

O sistema não deverá trabalhar somente com progresso por disciplina.

A progressão deverá ocorrer principalmente por:

```text
Disciplina
    ↓
Tópico
    ↓
Habilidade
    ↓
Desafio
    ↓
Questão
    ↓
Tentativa
    ↓
Progresso
```

Essa estrutura permitirá identificar com maior precisão quais habilidades o aluno domina e quais precisam de reforço.

Exemplo:

```text
Matemática
   └── Frações
        ├── Identificação de frações
        ├── Comparação de frações
        ├── Soma de frações
        └── Multiplicação de frações
```

O sistema deverá utilizar esse nível de granularidade para alimentar as recomendações de aprendizagem.

---

# 4. Arquitetura geral

A arquitetura será baseada em três principais aplicações:

```text
                   ┌───────────────────┐
                   │     WEB APP       │
                   │ React / TypeScript│
                   └─────────┬─────────┘
                             │
                             │
                   ┌─────────▼─────────┐
                   │     SUPABASE      │
                   │                   │
                   │ PostgreSQL        │
                   │ Auth              │
                   │ Storage           │
                   │ Edge Functions    │
                   │ Realtime          │
                   │ RLS               │
                   └───────┬───────────┘
                           │
             ┌─────────────┼──────────────┐
             │             │              │
             ▼             ▼              ▼
          ANDROID         IA        INTEGRAÇÕES
          APP             ENGINE    EXTERNAS
```

O Supabase será o núcleo de persistência, autenticação, autorização e serviços de backend.

---

# 5. Arquitetura Supabase

O Supabase será responsável principalmente por:

* PostgreSQL;
* autenticação;
* autorização;
* Row Level Security;
* armazenamento de arquivos;
* Edge Functions;
* Realtime;
* integração com aplicações Web e Android.

A aplicação cliente não deverá possuir lógica responsável por acessar diretamente dados que necessitem de privilégios administrativos.

Operações sensíveis deverão ser executadas por:

* PostgreSQL;
* funções SQL;
* Edge Functions;
* serviços backend autorizados.

---

# 6. Banco de dados

O banco será organizado em módulos.

## 6.1 Usuários e responsáveis

```text
profiles
children
parent_child
```

### profiles

Representa o usuário autenticado no Supabase.

Principais responsabilidades:

* identificação do usuário;
* nome;
* papel;
* preferências;
* informações básicas.

Papéis previstos:

```text
parent
admin
teacher
student
```

A autenticação será realizada pelo Supabase Auth.

---

## 6.2 Crianças

```text
children
parent_child
```

Uma criança poderá estar relacionada a um ou mais responsáveis conforme as regras definidas pelo sistema.

O relacionamento deverá ser utilizado pelas políticas de RLS para garantir isolamento dos dados.

Exemplo:

```text
Responsável A
     │
     ├── Criança 1
     └── Criança 2

Responsável B
     │
     └── Criança 3
```

Um responsável não deverá conseguir consultar dados de crianças que não estejam relacionadas a ele.

---

# 7. Estrutura educacional

```text
subjects
topics
skills
```

Relacionamento:

```text
Subject
   │
   └── Topics
          │
          └── Skills
```

Essa estrutura será utilizada por desafios, avaliações, recomendações e acompanhamento de progresso.

---

# 8. Mundos e níveis

A gamificação deverá possuir uma estrutura hierárquica:

```text
World
   │
   ├── Level
   │      ├── Challenge
   │      ├── Challenge
   │      └── Challenge
   │
   └── Level
```

Tabelas:

```text
worlds
world_levels
```

Os mundos poderão representar temas ou etapas da jornada educacional.

Exemplo:

```text
Mundo 1 — Fundamentos
Mundo 2 — Exploradores
Mundo 3 — Desafios
Mundo 4 — Mestres
```

A estrutura deverá permitir expansão futura para mapas, bosses, pets, eventos e temporadas.

---

# 9. Desafios e questões

Tabelas principais:

```text
challenges
questions
challenge_attempts
```

Um desafio poderá conter uma ou mais questões.

Cada tentativa deverá registrar informações suficientes para analisar o desempenho do aluno.

Exemplo:

```text
Aluno
  ↓
Desafio
  ↓
Questão
  ↓
Resposta
  ↓
Resultado
  ↓
XP / progresso
```

As tentativas serão utilizadas posteriormente pelo mecanismo de aprendizagem adaptativa.

---

# 10. Sistema de progresso

O progresso deverá ser armazenado por habilidade sempre que possível.

Tabela principal:

```text
progress
```

O sistema deverá conseguir identificar:

* habilidade;
* nível atual;
* percentual de domínio;
* quantidade de tentativas;
* acertos;
* erros;
* última atividade;
* evolução.

Isso permitirá que a plataforma diferencie:

```text
Aluno forte em Matemática
```

de:

```text
Aluno forte em Matemática,
mas com dificuldade específica em Frações.
```

---

# 11. Avaliação diagnóstica

O EduQuest deverá possuir uma avaliação inicial.

Estrutura:

```text
assessments
assessment_questions
```

Fluxo:

```text
Cadastro
   ↓
Avaliação inicial
   ↓
Análise das respostas
   ↓
Perfil de aprendizagem
   ↓
Recomendações
   ↓
Primeiros desafios
```

A avaliação não deverá simplesmente classificar o aluno.

Seu objetivo será identificar habilidades já dominadas e pontos que necessitam de desenvolvimento.

---

# 12. Inteligência Artificial

A IA será utilizada como camada de apoio ao sistema educacional.

Principais funções:

* avaliação adaptativa;
* análise de desempenho;
* identificação de dificuldades;
* recomendações;
* seleção de desafios;
* adaptação de dificuldade;
* tutor inteligente.

Estrutura:

```text
Learning Data
      ↓
AI Engine
      │
      ├── Assessment
      ├── Learning Analysis
      ├── Recommendations
      ├── Challenge Selection
      └── Tutor
```

Tabelas relacionadas:

```text
learning_profiles
learning_recommendations
ai_interactions
```

A implementação da camada de IA poderá utilizar Python.

A IA não deverá ter acesso irrestrito ao banco de dados.

O acesso deverá ocorrer somente aos dados necessários para cada operação.

---

# 13. Gamificação

O sistema de gamificação será dividido em diferentes elementos.

## XP

Representa a experiência acumulada pelo aluno.

```text
xp_transactions
```

## Moedas

Utilizadas para recompensas e elementos da economia do jogo.

```text
coins_transactions
```

## Estrelas

Utilizadas como indicador de desempenho ou conquistas.

```text
stars_transactions
```

O sistema deverá manter histórico das transações.

Isso permite evitar uma arquitetura baseada somente em um saldo atual.

Exemplo:

```text
Aluno
 │
 ├── +100 XP
 ├── +50 moedas
 ├── +3 estrelas
 ├── -20 moedas
 └── +150 XP
```

---

# 14. Recompensas

Tabela:

```text
rewards
```

As recompensas poderão estar relacionadas a:

* XP;
* moedas;
* estrelas;
* itens;
* desbloqueios;
* conquistas;
* conteúdos especiais.

---

# 15. Avatar e inventário

Estrutura:

```text
avatars
avatar_items
child_avatar_items
```

Relacionamento:

```text
Avatar
   │
   └── Items
          │
          └── Child Inventory
```

O aluno poderá desbloquear e utilizar itens para personalizar seu personagem.

Possíveis categorias:

* roupas;
* acessórios;
* personagens;
* fundos;
* pets;
* itens especiais.

---

# 16. Conquistas

Tabelas:

```text
achievements
child_achievements
```

Exemplos:

```text
Primeiro desafio
10 desafios concluídos
Primeira semana de estudos
1000 XP
Mestre da Matemática
Sequência de estudos
```

A estrutura deverá permitir a criação de novas conquistas sem alteração da arquitetura principal.

---

# 17. Missões

As missões serão diferentes dos desafios individuais.

Estrutura:

```text
missions
mission_challenges
```

Exemplo:

```text
Missão:
"Explorador da Matemática"

Objetivos:

1. Resolver 5 desafios
2. Acertar 80%
3. Estudar durante 30 minutos
```

Ao concluir a missão, o aluno poderá receber recompensas.

---

# 18. Área dos responsáveis

A área dos responsáveis deverá apresentar:

* dashboard;
* crianças cadastradas;
* progresso;
* desempenho;
* metas;
* agenda;
* sessões de estudo;
* notificações;
* contatos autorizados;
* políticas de uso;
* informações de aprendizagem.

Estrutura:

```text
Responsável
      ↓
Dashboard
      │
      ├── Crianças
      ├── Progresso
      ├── Relatórios
      ├── Agenda
      ├── Metas
      └── Configurações
```

---

# 19. Agenda de estudos

Tabelas:

```text
study_schedule
study_sessions
```

A agenda deverá permitir que responsáveis definam períodos de estudo.

Exemplo:

```text
Segunda
18:00 - 19:00
Matemática

Quarta
18:00 - 19:00
Português
```

As sessões realizadas poderão ser registradas para análise de frequência e consistência.

---

# 20. Controle de foco no Android

O aplicativo Android poderá implementar recursos de controle de foco durante períodos definidos pelos responsáveis.

Tabelas:

```text
device_profiles
app_policies
app_policy_rules
authorized_contacts
```

Exemplo conceitual:

```text
Período de estudo
       ↓
Política ativa
       ↓
Aplicativos configurados
       ↓
Android aplica a política
```

O banco de dados armazenará as regras.

A aplicação efetiva de bloqueios, sobreposições ou restrições será responsabilidade do aplicativo Android utilizando APIs e permissões oficiais da plataforma.

O Supabase não será responsável diretamente por bloquear aplicativos no dispositivo.

---

# 21. Contatos autorizados

A plataforma poderá permitir que responsáveis configurem contatos autorizados durante períodos de foco.

Tabela:

```text
authorized_contacts
```

A política deverá permitir futuramente regras como:

```text
Modo estudo ativo

Redes sociais
→ restringir

Aplicativos de entretenimento
→ restringir

Contatos autorizados
→ permitir comunicação
```

As regras efetivas dependerão das capacidades e permissões disponíveis no Android.

---

# 22. Google Calendar

A plataforma deverá possuir integração com Google Calendar.

Tabelas:

```text
calendar_integrations
calendar_events
```

Fluxo:

```text
Responsável
      ↓
Google OAuth
      ↓
Google Calendar
      ↓
EduQuest
      ↓
Agenda de estudos
```

O sistema poderá sincronizar eventos de estudo automaticamente.

Tokens e credenciais de integração não deverão ser expostos ao frontend.

Sempre que possível, operações relacionadas a credenciais deverão ser executadas através de Edge Functions ou backend seguro.

---

# 23. Notificações

Tabela:

```text
notifications
```

As notificações poderão ser utilizadas para:

* lembretes de estudo;
* conclusão de desafios;
* conquistas;
* recomendações;
* atividades pendentes;
* comunicação com responsáveis;
* eventos da agenda.

Canais futuros:

```text
in-app
email
push
```

---

# 24. Supabase Storage

O Storage poderá ser utilizado para:

* imagens de avatar;
* itens;
* materiais educacionais;
* imagens de questões;
* arquivos administrativos;
* documentos necessários ao funcionamento da plataforma.

O acesso aos arquivos deverá respeitar as regras de autorização.

---

# 25. Row Level Security

O RLS é um requisito central da arquitetura.

As políticas deverão garantir que:

```text
Responsável A
      ↓
somente seus filhos
      ↓
somente dados autorizados
```

Um usuário autenticado não deverá conseguir consultar ou alterar dados pertencentes a outro responsável.

As políticas deverão ser implementadas diretamente no PostgreSQL/Supabase.

Funções auxiliares poderão ser utilizadas para centralizar regras como:

```text
is_parent_of()
is_admin()
```

---

# 26. Segurança e privacidade

Como o EduQuest possui público infantil, segurança e privacidade serão requisitos fundamentais.

O projeto deverá considerar:

* LGPD;
* consentimento dos responsáveis;
* proteção de dados de crianças e adolescentes;
* minimização de dados;
* Row Level Security;
* autenticação segura;
* controle de acesso;
* criptografia;
* auditoria;
* controle de sessões;
* proteção das APIs;
* segurança das integrações externas.

A plataforma deverá coletar somente os dados necessários para suas finalidades.

Informações sensíveis não deverão ser armazenadas ou expostas sem necessidade.

---

# 27. Modelo de dados consolidado

A estrutura inicial do Supabase será composta pelos seguintes grupos.

## Identidade

```text
profiles
children
parent_child
```

## Educação

```text
subjects
topics
skills
```

## Game

```text
worlds
world_levels
challenges
questions
missions
mission_challenges
```

## Aprendizagem

```text
challenge_attempts
progress
assessments
assessment_questions
learning_profiles
learning_recommendations
```

## Gamificação

```text
rewards
xp_transactions
coins_transactions
stars_transactions
achievements
child_achievements
```

## Avatar

```text
avatars
avatar_items
child_avatar_items
```

## Agenda

```text
study_schedule
study_sessions
```

## Android

```text
device_profiles
app_policies
app_policy_rules
authorized_contacts
```

## Integrações

```text
calendar_integrations
calendar_events
notifications
```

## Inteligência Artificial

```text
ai_interactions
```

---

# 28. Estrutura física do projeto

A estrutura recomendada será:

```text
eduquest/
│
├── web/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── layouts/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── contexts/
│   │   ├── types/
│   │   └── lib/
│   │
│   └── package.json
│
├── android/
│   └── EduQuest/
│
├── ai/
│   ├── app/
│   │   ├── assessment/
│   │   ├── learning/
│   │   ├── recommendations/
│   │   ├── challenges/
│   │   └── tutor/
│   │
│   └── requirements.txt
│
├── supabase/
│   ├── migrations/
│   ├── functions/
│   ├── seed/
│   └── config.toml
│
├── docs/
│   ├── architecture/
│   ├── database/
│   ├── api/
│   ├── ai/
│   ├── android/
│   └── product/
│
└── README.md
```

---

# 29. Organização das migrations

O banco não deverá depender de um único arquivo SQL gigantesco.

As migrations deverão ser organizadas por responsabilidade.

Exemplo:

```text
supabase/migrations/

001_extensions.sql
002_profiles_children.sql
003_education.sql
004_worlds_challenges.sql
005_assessments_learning.sql
006_gamification.sql
007_avatar_achievements.sql
008_study_schedule.sql
009_android_policies.sql
010_google_calendar.sql
011_notifications_ai.sql
012_indexes.sql
013_functions.sql
014_rls.sql
```

Dados iniciais poderão ficar separados:

```text
supabase/seed/

subjects.sql
topics.sql
worlds.sql
achievements.sql
development.sql
```

Essa organização facilita:

* manutenção;
* versionamento;
* deploy;
* rollback;
* testes;
* evolução do banco.

---

# 30. Edge Functions

As Edge Functions deverão ser utilizadas para operações que não devem ser executadas diretamente pelo cliente.

Exemplos:

```text
supabase/functions/

ai-assessment/
ai-recommendation/
ai-tutor/
calendar-sync/
calendar-oauth/
send-notification/
admin-actions/
```

A nomenclatura poderá ser alterada conforme a implementação.

---

# 31. Regras de arquitetura

Algumas regras deverão ser consideradas obrigatórias.

### Regra 1 — Banco como fonte oficial

O Supabase PostgreSQL será a fonte oficial dos dados da aplicação.

O frontend não deverá depender de dados simulados ou arquivos locais para representar dados reais.

### Regra 2 — Histórico de transações

XP, moedas e estrelas deverão possuir histórico de transações.

### Regra 3 — Progresso por habilidade

Sempre que possível, o progresso deverá ser relacionado a habilidades específicas.

### Regra 4 — Segurança no servidor

Operações administrativas ou sensíveis não deverão depender exclusivamente de validações no frontend.

### Regra 5 — RLS

Toda tabela que possuir dados privados deverá possuir políticas adequadas de RLS.

### Regra 6 — IA isolada

A IA deverá receber somente os dados necessários para realizar determinada tarefa.

### Regra 7 — Android independente

As políticas de foco armazenadas no Supabase não significam que o banco irá controlar o dispositivo.

A aplicação Android será responsável pela execução das políticas.

---

# 32. Stack tecnológica

## Web

* React
* TypeScript
* Vite
* React Router
* TanStack Query
* React Hook Form
* Zod
* Framer Motion
* Recharts
* Supabase Client

## Android

* Kotlin
* Jetpack Compose
* Android SDK
* APIs nativas do Android

## Backend

* Supabase PostgreSQL
* Supabase Auth
* Supabase Storage
* Supabase Edge Functions
* Row Level Security
* Supabase Realtime

## Inteligência Artificial

Serviço independente, com possibilidade de implementação em Python.

Responsabilidades:

* avaliação adaptativa;
* análise de desempenho;
* recomendações;
* seleção de desafios;
* tutor inteligente.

---

# 33. Fluxo principal do aluno

```text
Cadastro
   ↓
Perfil
   ↓
Avaliação diagnóstica
   ↓
Perfil de aprendizagem
   ↓
Recomendação
   ↓
Desafio
   ↓
Resposta
   ↓
Análise
   ↓
XP / Moedas / Estrelas
   ↓
Atualização do progresso
   ↓
Novo desafio
```

O sistema deverá utilizar os resultados anteriores para melhorar progressivamente a seleção das próximas atividades.

---

# 34. Fluxo dos responsáveis

```text
Login
  ↓
Dashboard
  ↓
Selecionar criança
  ↓
Visualizar progresso
  ↓
Definir metas
  ↓
Configurar agenda
  ↓
Configurar políticas
  ↓
Acompanhar sessões
  ↓
Receber notificações
```

---

# 35. Roadmap de desenvolvimento

## Fase 1 — Fundação

* [ ] Criar repositório
* [ ] Configurar Supabase
* [ ] Criar migrations
* [ ] Criar RLS
* [ ] Configurar autenticação
* [ ] Criar aplicação Web
* [ ] Criar estrutura Android
* [ ] Estruturar documentação
* [ ] Definir identidade visual

## Fase 2 — Banco e núcleo educacional

* [ ] Profiles
* [ ] Crianças
* [ ] Responsáveis
* [ ] Disciplinas
* [ ] Tópicos
* [ ] Habilidades
* [ ] Questões
* [ ] Desafios
* [ ] Tentativas
* [ ] Progresso

## Fase 3 — Game Core

* [ ] XP
* [ ] Níveis
* [ ] Moedas
* [ ] Estrelas
* [ ] Recompensas
* [ ] Avatar
* [ ] Inventário
* [ ] Conquistas
* [ ] Missões
* [ ] Mundos
* [ ] Fases

## Fase 4 — Conteúdo

* [ ] Matemática
* [ ] Português
* [ ] Biologia
* [ ] Física
* [ ] Química
* [ ] Banco de questões
* [ ] Banco de desafios
* [ ] Progressão por habilidade

## Fase 5 — Inteligência Artificial

* [ ] Avaliação inicial
* [ ] Diagnóstico
* [ ] Perfil de aprendizagem
* [ ] Análise de erros
* [ ] Recomendação
* [ ] Dificuldade adaptativa
* [ ] Seleção automática de desafios
* [ ] Tutor IA

## Fase 6 — Área dos responsáveis

* [ ] Dashboard
* [ ] Cadastro de crianças
* [ ] Relatórios
* [ ] Metas
* [ ] Agenda
* [ ] Sessões de estudo
* [ ] Notificações
* [ ] Contatos autorizados

## Fase 7 — Integrações

* [ ] Google OAuth
* [ ] Google Calendar
* [ ] Sincronização de eventos
* [ ] Notificações
* [ ] Políticas de foco Android
* [ ] Integrações externas

## Fase 8 — Game 2.0

* [ ] Mapas
* [ ] Mundos avançados
* [ ] Bosses
* [ ] Pets
* [ ] Loja
* [ ] Eventos
* [ ] Ranking
* [ ] Temporadas
* [ ] Desafios especiais
* [ ] Guildas

---

# 36. Roadmap futuro

Possíveis evoluções:

* professores;
* escolas;
* turmas;
* painel pedagógico;
* criação de conteúdo por professores;
* relatórios educacionais;
* desafios entre alunos;
* ranking por turma;
* eventos;
* temporadas;
* sistema de guildas;
* multiplayer educacional;
* suporte a tablets;
* versão iOS;
* integração com plataformas educacionais;
* recomendações pedagógicas avançadas.

---

# 37. Princípios do projeto

## Educação em primeiro lugar

A gamificação deve incentivar o aprendizado e não substituir o conteúdo pedagógico.

## Personalização

Cada aluno deverá receber uma experiência compatível com seu nível e evolução.

## Progressão saudável

O sistema deverá incentivar consistência sem criar pressão excessiva sobre a criança.

## Segurança

Dados de crianças e responsáveis deverão receber tratamento prioritário.

## Privacidade

A plataforma deverá coletar somente os dados necessários para seu funcionamento.

## Escalabilidade

A arquitetura deverá permitir a inclusão de novas disciplinas, conteúdos, funcionalidades e plataformas.

## Experiência de jogo

A interface deverá ser moderna, divertida e intuitiva, sem perder a clareza necessária para uma aplicação educacional.

---

# 38. Estratégia de implementação do Supabase

A implementação deverá seguir esta ordem:

```text
1. Supabase Project
       ↓
2. Extensions
       ↓
3. Profiles / Children
       ↓
4. Subjects / Topics / Skills
       ↓
5. Worlds / Challenges / Questions
       ↓
6. Attempts / Progress
       ↓
7. Assessments / Learning
       ↓
8. Gamification
       ↓
9. Avatar / Achievements
       ↓
10. Study Schedule
       ↓
11. Android Policies
       ↓
12. Calendar
       ↓
13. Notifications
       ↓
14. AI
       ↓
15. RLS / Security
       ↓
16. Seed Data
```

A criação das tabelas deverá ser feita por migrations versionadas.

---

# 39. Ambiente de desenvolvimento

Variáveis de ambiente esperadas para a aplicação Web:

```env
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
```

Chaves administrativas do Supabase não deverão ser expostas no frontend.

Quando necessárias, deverão permanecer exclusivamente no ambiente seguro do backend ou Edge Functions.

---

# 40. Estado atual do projeto

O projeto encontra-se em fase de planejamento e estruturação inicial.

A prioridade técnica atual é estabelecer uma fundação consistente para:

1. banco de dados;
2. autenticação;
3. RLS;
4. modelo educacional;
5. gamificação;
6. progresso;
7. avaliação diagnóstica;
8. IA;
9. área dos responsáveis;
10. integrações.

A implementação deverá ocorrer incrementalmente, evitando criar funcionalidades de interface antes que o modelo de dados e as regras de negócio correspondentes estejam definidos.

---

# 41. Objetivo da primeira versão funcional

A primeira versão funcional deverá priorizar o seguinte fluxo:

```text
Responsável
    ↓
Cadastro / Login
    ↓
Cadastro da criança
    ↓
Avaliação inicial
    ↓
Perfil de aprendizagem
    ↓
Escolha de disciplina
    ↓
Desafio
    ↓
Resposta
    ↓
Resultado
    ↓
XP / moedas / estrelas
    ↓
Atualização do progresso
    ↓
Próxima recomendação
```

Após esse fluxo estar estável, deverão ser adicionados progressivamente:

```text
Gamificação avançada
        ↓
Avatar
        ↓
Missões
        ↓
Conquistas
        ↓
Área dos responsáveis
        ↓
Agenda
        ↓
Google Calendar
        ↓
Android Focus
        ↓
Tutor IA
        ↓
Game 2.0
```

---

# 42. Critérios de qualidade

Antes de considerar uma funcionalidade concluída, deverão ser verificados:

* persistência correta no PostgreSQL;
* autenticação;
* autorização;
* RLS;
* tratamento de erros;
* validação dos dados;
* funcionamento no Web;
* comportamento no Android quando aplicável;
* consistência entre frontend e banco;
* segurança das APIs;
* logs adequados;
* comportamento em caso de ausência de dados;
* testes de permissões.

---

# 43. Licença

Definir a licença do projeto conforme o modelo de distribuição escolhido.

---

# EduQuest

## Aprender. Jogar. Evoluir.

O EduQuest busca transformar desafios educacionais em uma jornada de aprendizagem na qual cada atividade representa uma oportunidade de evolução.

A arquitetura foi projetada para permitir que educação, gamificação, inteligência artificial, acompanhamento familiar e recursos móveis evoluam de forma integrada, segura e escalável.
