# EduQuest

Plataforma multiplataforma de aprendizagem gamificada que transforma o desenvolvimento de habilidades escolares em uma experiência interativa baseada em desafios, progressão, recompensas e personalização por Inteligência Artificial.

O EduQuest foi projetado para atender crianças, responsáveis e, futuramente, instituições de ensino, combinando **educação, gamificação, inteligência artificial, controle parental e acompanhamento de desempenho** em uma única plataforma.

---

## 1. Visão

O objetivo do EduQuest é tornar o aprendizado mais envolvente e personalizado.

A criança participa de desafios relacionados a:

* Matemática
* Português
* Ciências

  * Biologia
  * Física
  * Química

Ao completar atividades, o jogador recebe experiência, moedas, estrelas e conquistas que podem ser utilizadas para evoluir seu personagem e desbloquear elementos do jogo.

A plataforma utiliza Inteligência Artificial para analisar o desempenho do aluno e adaptar progressivamente a dificuldade e os conteúdos apresentados.

---

## 2. Principais funcionalidades

### Experiência da criança

* Sistema de níveis e experiência (XP)
* Desafios interativos
* Missões diárias
* Sistema de recompensas
* Moedas e estrelas
* Sistema de conquistas
* Sequência de estudos
* Avatares personalizáveis
* Loja de itens virtuais
* Evolução por disciplina
* Mapas e mundos temáticos
* Desafios especiais e Bosses
* Sistema de aprendizagem adaptativa

### Disciplinas

#### Matemática

* Operações
* Multiplicação
* Divisão
* Frações
* Geometria
* Problemas matemáticos
* Raciocínio lógico

#### Português

* Leitura
* Interpretação de texto
* Gramática
* Ortografia
* Formação de palavras
* Construção de frases

#### Ciências

* Biologia
* Física
* Química
* Ciências naturais

A estrutura foi projetada para permitir a inclusão de novas disciplinas e competências futuramente.

---

# 3. Avaliação inicial

Na primeira utilização, a criança realiza uma avaliação diagnóstica.

O sistema utiliza uma abordagem adaptativa para identificar:

* nível atual do aluno;
* conhecimentos consolidados;
* dificuldades;
* habilidades que precisam de reforço;
* nível recomendado de dificuldade.

Exemplo:

```text
AVALIAÇÃO INICIAL

Matemática       82%
Português        74%
Ciências         61%

Pontos fortes
- Operações básicas
- Leitura

Necessita reforço
- Frações
- Interpretação
- Ciências
```

Essas informações alimentam o perfil de aprendizagem utilizado pelo motor de personalização.

---

# 4. Inteligência Artificial

A IA é responsável por personalizar a experiência de aprendizagem.

O sistema poderá analisar:

* respostas;
* erros;
* tempo de resposta;
* quantidade de tentativas;
* dificuldade das questões;
* evolução histórica;
* frequência de estudos;
* desempenho por habilidade.

A partir dessas informações, o sistema poderá recomendar:

```text
Próximo conteúdo:
Frações

Dificuldade:
Intermediária

Formato:
Desafio interativo

Motivo:
O aluno apresentou dificuldade
em 4 dos últimos 7 exercícios.
```

## Componentes de IA

O projeto prevê inicialmente:

* Assessment Engine
* Skill Analyzer
* Learning Profile
* Recommendation Engine
* Challenge Generator
* Adaptive Difficulty
* AI Tutor

A IA deve atuar como suporte ao processo educacional e não como substituta de professores ou responsáveis.

---

# 5. Gamificação

A gamificação é um dos principais componentes do EduQuest.

## XP

Utilizado para evolução do nível do jogador.

## Moedas

Podem ser utilizadas para adquirir itens virtuais.

## Estrelas

Representam recompensas especiais e podem desbloquear itens diferenciados.

## Conquistas

Reconhecem marcos importantes.

Exemplos:

```text
Primeiro Desafio
100 Desafios
Mestre da Matemática
Explorador da Ciência
7 Dias de Estudos
30 Dias de Estudos
```

---

# 6. Sistema de Avatar

Cada criança possui um personagem personalizável.

Itens previstos:

* cabelo;
* rosto;
* olhos;
* roupas;
* calçados;
* acessórios;
* chapéus;
* mochilas;
* pets;
* skins;
* efeitos visuais.

Os itens poderão ser desbloqueados através da progressão no jogo.

A progressão educacional não deve depender de compras financeiras.

---

# 7. Sistema de mundos

O conteúdo educacional será organizado dentro de mundos temáticos.

Exemplo:

```text
MUNDO 01
Vila dos Números
        |
        +-- Números
        +-- Operações
        +-- Multiplicação
        +-- Divisão
        +-- Geometria
        +-- Boss Matemático
```

```text
MUNDO 02
Reino das Palavras
        |
        +-- Leitura
        +-- Ortografia
        +-- Gramática
        +-- Interpretação
        +-- Boss da Língua
```

```text
MUNDO 03
Laboratório
        |
        +-- Biologia
        +-- Física
        +-- Química
        +-- Ciências Naturais
        +-- Cientista Supremo
```

A estrutura permite adicionar novos mundos e conteúdos sem alterar a arquitetura principal.

---

# 8. Área dos responsáveis

A plataforma possuirá uma área administrativa destinada aos responsáveis.

Funcionalidades previstas:

* cadastro de crianças;
* acompanhamento de desempenho;
* acompanhamento de tempo de estudo;
* histórico de atividades;
* evolução por disciplina;
* definição de metas;
* criação de agenda;
* configuração de sessões de estudo;
* notificações;
* gerenciamento de permissões;
* contatos autorizados;
* políticas de uso do dispositivo;
* integração com Google Calendar.

Exemplo de indicadores:

```text
TEMPO DE ESTUDO
42 minutos

DESEMPENHO
87%

SEQUÊNCIA
12 dias

MATEMÁTICA
82%

PORTUGUÊS
74%

CIÊNCIAS
61%
```

---

# 9. Agenda de estudos

Os responsáveis poderão configurar uma rotina de estudos.

Exemplo:

```text
Segunda
18:00 - 18:40
Matemática

Terça
18:00 - 18:40
Português

Quarta
18:00 - 18:40
Ciências

Quinta
18:00 - 18:40
Matemática

Sexta
18:00 - 19:00
Revisão
```

As sessões serão armazenadas no Supabase e utilizadas pelo aplicativo Android para iniciar as experiências de estudo.

---

# 10. Google Calendar

O responsável poderá conectar sua conta Google e sincronizar automaticamente os horários de estudo definidos na plataforma.

Fluxo:

```text
Responsável
     |
     v
Painel EduQuest
     |
     v
Google OAuth
     |
     v
Google Calendar
     |
     v
Evento de estudo
```

Exemplo:

```text
EduQuest - Matemática

18:00 - 18:40

Aluno: João
Disciplina: Matemática
```

A integração deverá utilizar as APIs oficiais do Google e respeitar as permissões concedidas pelo usuário.

---

# 11. Controle de foco no Android

O aplicativo Android possuirá um módulo de foco destinado a ajudar a criança a manter sua rotina de estudos.

Durante uma sessão, o aplicativo poderá utilizar os mecanismos disponibilizados pelo Android para:

* iniciar sessões de estudo;
* apresentar notificações;
* monitorar o uso do dispositivo quando permitido;
* aplicar políticas de foco configuradas pelos responsáveis;
* priorizar aplicativos autorizados;
* orientar a criança de volta para a atividade.

Exemplo:

```text
SESSÃO DE ESTUDO

18:00 - 18:40

Matemática

Tempo restante:
32 minutos

[ CONTINUAR MISSÃO ]
```

O projeto deverá respeitar as APIs, permissões e políticas de segurança do Android. Recursos de bloqueio, sobreposição ou gerenciamento de aplicativos dependerão das capacidades oficialmente disponíveis para a versão do sistema e do modelo de distribuição do aplicativo.

---

# 12. Contatos autorizados

O responsável poderá definir contatos prioritários.

Exemplo:

```text
CONTATOS AUTORIZADOS

Responsável 01     ✓
Responsável 02     ✓
Professor          ✓
```

Durante uma sessão de estudo, o sistema poderá aplicar políticas diferenciadas aos aplicativos de comunicação, respeitando as limitações e permissões disponíveis no Android.

Chamadas e funcionalidades de emergência devem permanecer acessíveis conforme as regras do sistema operacional.

---

# 13. Arquitetura

A arquitetura inicial será composta por:

```text
                    EDUQUEST
                       |
          +------------+------------+
          |                         |
          v                         v
      WEB APP                  ANDROID APP
          |                         |
          +------------+------------+
                       |
                       v
                   SUPABASE
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
     Database         Auth          Storage
        |
        v
   Learning Data
        |
        v
    AI ENGINE
        |
   +----+----+----------------+
   |         |                |
   v         v                v
Assessment  Profile     Recommendations
   |
   v
Adaptive Challenges
```

---

# 14. Stack tecnológica

## Frontend Web

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

A escolha por Kotlin permite maior controle sobre recursos específicos do sistema Android.

## Backend

O backend será baseado principalmente nos recursos do Supabase:

* PostgreSQL
* Supabase Auth
* Supabase Storage
* Supabase Edge Functions
* Row Level Security
* Realtime

## Inteligência Artificial

Serviço independente para:

* avaliação adaptativa;
* análise de desempenho;
* recomendações;
* geração/seleção de desafios;
* tutor inteligente.

A implementação do serviço de IA poderá utilizar Python.

---

# 15. Estrutura do projeto

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
│   │   └── types/
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
│   └── seed/
│
├── docs/
│   ├── architecture/
│   ├── database/
│   ├── api/
│   ├── ai/
│   └── product/
│
└── README.md
```

---

# 16. Banco de dados

A estrutura inicial do Supabase deverá contemplar entidades como:

```text
profiles
children
parent_child

subjects
topics
skills

challenges
questions
challenge_attempts

assessments
assessment_questions
learning_profiles
learning_recommendations

study_sessions
study_schedule

avatars
avatar_items
child_avatar_items

rewards
achievements
child_achievements

coins_transactions
stars_transactions

authorized_contacts
app_policies

calendar_integrations
notifications
```

O banco deverá utilizar **Row Level Security (RLS)** para garantir que responsáveis tenham acesso somente aos dados autorizados de suas respectivas crianças.

---

# 17. Segurança e privacidade

Como o EduQuest possui público infantil, segurança e privacidade são requisitos fundamentais.

O projeto deverá considerar:

* LGPD;
* consentimento dos responsáveis;
* proteção de dados de crianças e adolescentes;
* minimização de dados coletados;
* Row Level Security;
* autenticação segura;
* controle de acesso;
* criptografia;
* auditoria;
* controle de sessões;
* proteção das APIs;
* segurança das integrações externas.

A plataforma não deve coletar dados desnecessários para sua finalidade educacional.

---

# 18. Roadmap

## Fase 1 — Fundação

* [ ] Criar repositório
* [ ] Configurar Supabase
* [ ] Criar banco inicial
* [ ] Configurar autenticação
* [ ] Criar projeto Web
* [ ] Criar projeto Android
* [ ] Estruturar documentação
* [ ] Definir identidade visual

## Fase 2 — Game Core

* [ ] Sistema de XP
* [ ] Níveis
* [ ] Moedas
* [ ] Estrelas
* [ ] Recompensas
* [ ] Avatar
* [ ] Inventário
* [ ] Conquistas
* [ ] Missões

## Fase 3 — Conteúdo

* [ ] Matemática
* [ ] Português
* [ ] Biologia
* [ ] Física
* [ ] Química
* [ ] Banco de questões
* [ ] Sistema de desafios
* [ ] Progressão por habilidade

## Fase 4 — IA

* [ ] Avaliação inicial
* [ ] Diagnóstico
* [ ] Perfil de aprendizagem
* [ ] Análise de erros
* [ ] Recomendação
* [ ] Dificuldade adaptativa
* [ ] Tutor IA

## Fase 5 — Área dos responsáveis

* [ ] Dashboard
* [ ] Cadastro de crianças
* [ ] Relatórios
* [ ] Metas
* [ ] Agenda
* [ ] Notificações
* [ ] Contatos autorizados

## Fase 6 — Integrações

* [ ] Google OAuth
* [ ] Google Calendar
* [ ] Sincronização de eventos
* [ ] Políticas de foco Android

## Fase 7 — Game 2.0

* [ ] Mapas
* [ ] Mundos
* [ ] Bosses
* [ ] Pets
* [ ] Loja
* [ ] Eventos
* [ ] Ranking
* [ ] Temporadas
* [ ] Desafios especiais

---

# 19. Princípios do projeto

O desenvolvimento do EduQuest seguirá alguns princípios:

### Educação em primeiro lugar

A gamificação deve incentivar o aprendizado e não substituir o conteúdo pedagógico.

### Personalização

Cada aluno deve receber uma experiência compatível com seu nível e evolução.

### Progressão saudável

O sistema deve incentivar consistência sem criar pressão excessiva sobre a criança.

### Segurança

Dados infantis e informações dos responsáveis devem receber tratamento prioritário.

### Privacidade

Coletar somente os dados necessários para funcionamento da plataforma.

### Escalabilidade

A arquitetura deve permitir a inclusão de novas disciplinas, conteúdos, funcionalidades e plataformas.

### Experiência de jogo

A interface deve ser divertida, moderna e intuitiva, sem perder a clareza necessária para uma aplicação educacional.

---

# 20. Roadmap futuro

Possíveis evoluções:

* suporte a professores;
* escolas;
* turmas;
* painel pedagógico;
* criação de conteúdo por professores;
* relatórios educacionais;
* desafios entre amigos;
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

# 21. Status

**Projeto em fase de planejamento e desenvolvimento inicial.**

A implementação será realizada de forma incremental, priorizando primeiro o núcleo educacional, gamificação, avaliação adaptativa e infraestrutura.

---

# 22. Licença

Definir licença do projeto conforme o modelo de distribuição escolhido.

---

## EduQuest

**Aprender. Jogar. Evoluir.**

Uma experiência de aprendizagem construída para transformar desafios escolares em conquistas.
