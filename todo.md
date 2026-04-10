# Painel Líder Corretora - TODO

## Fase 1: Arquitetura de Dados
- [x] Definir schema do banco de dados (Drizzle ORM)
  - [x] Tabela `employees` (funcionários)
  - [x] Tabela `xp_logs` (histórico de XP imutável)
  - [x] Tabela `badges` (conquistas disponíveis)
  - [x] Tabela `employee_badges` (conquistas dos funcionários)
  - [x] Tabela `rewards` (prêmios da loja)
  - [x] Tabela `reward_redemptions` (resgates de recompensas)
  - [x] Tabela `duels` (duelos de XP)
  - [x] Tabela `duel_participants` (participantes dos duelos)
  - [x] Tabela `admin_users` (usuários administradores)

## Fase 2: Backend (tRPC Routers e Autenticação)
- [x] Implementar autenticação de admin com token JWT
- [x] Criar middleware de autenticação para rotas protegidas
- [x] Implementar router de funcionários (CRUD)
- [x] Implementar router de XP com logging imutável
- [x] Implementar router de conquistas (badges)
- [x] Implementar router de loja de recompensas
- [x] Implementar router de duelos de XP
- [x] Implementar notificações automáticas ao admin
- [x] Corrigir bug de salvamento de QR Codes (implementado com upload para S3)
- [x] Implementar upload de fotos/QR Codes para S3 (ImageUploadField + routers tRPC)

## Fase 3: Interface de Administração
- [x] Criar tela de login com autenticação
- [x] Criar dashboard principal do admin
- [x] Implementar gerenciamento de funcionários (CRUD com UI completa)
- [x] Implementar gerenciamento de badges (UI completa com criação e listagem)
- [x] Implementar gerenciamento de recompensas (CRUD com UI completa)
- [x] Implementar gerenciamento de duelos (UI completa com criação e listagem)
- [x] Implementar visualização de logs de XP (UI completa com filtros e export CSV)

## Fase 4: Sistema de Gamificação
- [x] Implementar sistema de conquistas (badges) com critérios automáticos
- [x] Implementar loja de recompensas com resgate de XP
- [x] Implementar duelos de XP com gráfico de progresso em tempo real
- [x] Criar histórico de resgates de recompensas

## Fase 5: Modo TV Dinâmico
- [x] Redesenhar Modo TV com slides em tela cheia
- [x] Implementar slide individual de funcionário
- [x] Implementar slide de ranking geral
- [x] Implementar slide de conquistas recentes
- [x] Implementar slide de aniversariantes
- [x] Implementar slide de duelos ativos
- [x] Adicionar animações e transições entre slides

## Fase 6: Correções de UI/UX
- [x] Ajustar layout dos cards para não cortar nomes (EmployeeCard com truncamento inteligente)
- [x] Implementar truncamento inteligente com tooltip (implementado em EmployeeCard)
- [x] Reduzir vinheta preta na parte inferior das fotos (vinheta reduzida em cards)
- [x] Melhorar visualização das imagens nos cards (melhorias aplicadas e testadas)

## Fase 7: Testes e Entrega
- [x] Testes unitários com Vitest (35 testes passando)
  - [x] 15 testes de XP e badges
  - [x] 10 testes de CRUD de funcionários
  - [x] 9 testes de recompensas
  - [x] 1 teste de logout
- [x] Testes unitários (35 testes com Vitest cobrindo XP, badges, funcionários, recompensas)
- [ ] Testes de integração (fluxos end-to-end de upload, XP, duelos - pendente)
- [x] Validação de segurança básica (autenticação admin, validação de tamanho, tratamento de erros)
- [x] Documentação final (README.md com setup, arquitetura, fluxos e guia de alterações)
- [x] Pronto para Deploy (estrutura completa, testes passando, sem erros de build)
