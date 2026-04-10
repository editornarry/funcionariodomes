# Painel Líder Corretora - Sistema de Gamificação e Engajamento

Um sistema completo de gamificação para gestão de funcionários com XP, badges, recompensas, duelos e modo TV dinâmico.

## 🚀 Funcionalidades Principais

### 1. **Sistema de XP e Ranking**
- Adicionar/subtrair XP de funcionários com logging imutável
- Histórico completo de alterações com data, hora e responsável
- Visualização de logs com filtros e export CSV
- Cálculo automático de XP por avaliações de clientes (1-5 estrelas)

### 2. **Badges (Conquistas)**
- Concessão automática de medalhas baseada em critérios:
  - Primeira avaliação 5 estrelas
  - Meta mensal alcançada
  - Recorde de XP
  - Assiduidade perfeita
- Gerenciamento de badges no dashboard
- Histórico de conquistas por funcionário

### 3. **Loja de Recompensas**
- Catálogo de prêmios com custo em XP
- Resgate de recompensas pelos funcionários
- Histórico de resgates com status (pending/approved/completed)
- Notificações automáticas ao admin

### 4. **Duelos de XP**
- Competições entre funcionários ou setores
- Prazo configurável
- Gráfico de progresso em tempo real
- Bônus de XP para vencedor
- Visualização de duelos ativos/finalizados

### 5. **Modo TV Dinâmico**
- Slides em tela cheia para exibição em TV da sala de clientes
- 5 tipos de slides:
  - Slide individual de funcionário (foto, XP, cargo, QR Code)
  - Ranking geral
  - Conquistas recentes
  - Aniversariantes
  - Duelos ativos
- Animações e transições suaves
- Intervalo configurável entre slides

### 6. **Upload de Fotos e QR Codes**
- Upload de fotos de perfil para S3
- Upload de QR Codes de avaliação para S3
- Validação de tamanho (máx 5MB)
- Chaves únicas com timestamp para evitar sobrescrita
- Preview antes do upload

### 7. **Dashboard de Administração**
- 6 abas funcionais:
  - Gerenciamento de funcionários (CRUD)
  - Gerenciamento de badges
  - Gerenciamento de recompensas
  - Gerenciamento de duelos
  - Visualização de logs de XP
- Autenticação com admin procedure
- Interface intuitiva e responsiva

## 📋 Arquitetura Técnica

### Backend (tRPC + Express)
- **40+ endpoints** para todas as operações
- **Autenticação admin** com JWT
- **Logging imutável** de todas as alterações
- **Notificações automáticas** ao admin
- **Upload para S3** com validação robusta

### Banco de Dados (Drizzle ORM + MySQL)
- **11 tabelas** bem estruturadas:
  - `employees`: Dados dos funcionários
  - `xp_logs`: Histórico imutável de XP
  - `badge_definitions`: Definições de conquistas
  - `employee_badges`: Conquistas dos funcionários
  - `rewards`: Catálogo de prêmios
  - `reward_redemptions`: Resgates de recompensas
  - `duels`: Competições de XP
  - `duel_participants`: Participantes dos duelos
  - `survey_responses`: Respostas de avaliação
  - `admin_notifications`: Log de notificações
  - `users`: Usuários do sistema

### Frontend (React + Tailwind + shadcn/ui)
- **Componentes reutilizáveis** para máxima flexibilidade
- **ImageUploadField**: Upload com preview e validação
- **EmployeeCard**: Card com truncamento inteligente
- **TVMode**: Slides dinâmicos em tela cheia
- **Responsivo**: Design adaptável para todas as telas

## 🧪 Testes

### Testes Unitários (35 testes passando)
```bash
pnpm test
```

Cobertura:
- ✅ 15 testes de XP e badges
- ✅ 10 testes de CRUD de funcionários
- ✅ 9 testes de recompensas
- ✅ 1 teste de logout

## 🔧 Setup Local

### Pré-requisitos
- Node.js 22+
- pnpm 10+
- MySQL/TiDB database

### Instalação
```bash
# Instalar dependências
pnpm install

# Gerar migrations do banco de dados
pnpm drizzle-kit generate

# Aplicar migrations (via UI do Manus)
# Usar webdev_execute_sql para aplicar o SQL gerado

# Iniciar servidor de desenvolvimento
pnpm dev
```

### Variáveis de Ambiente
Configuradas automaticamente pelo Manus:
- `DATABASE_URL`: Conexão MySQL
- `JWT_SECRET`: Chave para JWT
- `VITE_APP_ID`: ID da aplicação OAuth
- `OAUTH_SERVER_URL`: URL do servidor OAuth
- `BUILT_IN_FORGE_API_URL`: URL da API Manus
- `BUILT_IN_FORGE_API_KEY`: Chave da API Manus

## 📝 Fluxos Principais

### 1. Adicionar Funcionário
1. Admin acessa Dashboard → Funcionários
2. Clica em "Novo Funcionário"
3. Preenche dados básicos
4. Após criar, pode fazer upload de foto e QR Code
5. Funcionário aparece no ranking e Modo TV

### 2. Adicionar XP
1. Admin acessa Dashboard → Funcionários
2. Seleciona funcionário
3. Clica em "Adicionar XP"
4. Insere valor e motivo
5. XP é adicionado e log é registrado
6. Badges são verificadas automaticamente

### 3. Criar Duelo
1. Admin acessa Dashboard → Duelos
2. Clica em "Novo Duelo"
3. Seleciona participantes/setores
4. Define prazo
5. Duelo aparece no Modo TV
6. Vencedor recebe bônus de XP

### 4. Visualizar Modo TV
1. Usuário acessa `/tv`
2. Slides mudam automaticamente a cada intervalo
3. Exibe funcionários, ranking, badges, aniversariantes, duelos
4. Ideal para exibir em tela na sala de clientes

## 🛡️ Segurança

### Autenticação
- Admin procedure valida role do usuário
- Todas as rotas de alteração requerem autenticação
- JWT para sessão segura

### Validação
- Tamanho máximo de arquivo: 5MB
- Validação de tipo de arquivo
- Sanitização de entrada
- Tratamento de erros específico

### Logging
- Todas as alterações de XP são registradas
- Histórico imutável com data, hora e responsável
- Rastreabilidade completa

## 📊 Componentes Reutilizáveis

### ImageUploadField
```tsx
<ImageUploadField
  label="Foto de Perfil"
  onImageSelect={(file) => handleUpload(file)}
  isLoading={isUploading}
/>
```

### EmployeeCard
```tsx
<EmployeeCard
  id={employee.id}
  name={employee.name}
  role={employee.role}
  sector={employee.sector}
  photoUrl={employee.photoUrl}
  currentXp={employee.currentXp}
/>
```

## 🚀 Deploy

### Via Manus UI
1. Clique em "Publish" no Management UI
2. Escolha domínio customizado (opcional)
3. Aguarde build e deploy
4. Acesse URL fornecida

### Checklist antes de publicar
- ✅ Todos os testes passando (`pnpm test`)
- ✅ Sem erros de TypeScript (`pnpm check`)
- ✅ Variáveis de ambiente configuradas
- ✅ Banco de dados migrado
- ✅ Checkpoint salvo

## 📚 Estrutura de Arquivos

```
lider-corretora-panel/
├── client/
│   ├── src/
│   │   ├── pages/          # Páginas (Home, Admin, TV, etc)
│   │   ├── components/     # Componentes reutilizáveis
│   │   ├── lib/            # Utilitários (tRPC client)
│   │   └── contexts/       # React contexts
│   └── public/             # Arquivos estáticos
├── server/
│   ├── routers.ts          # Endpoints tRPC
│   ├── db.ts               # Query helpers
│   ├── storage.ts          # S3 helpers
│   └── _core/              # Framework internals
├── drizzle/
│   └── schema.ts           # Definição do banco
└── todo.md                 # Rastreamento de tarefas
```

## 🔄 Fluxo de Alterações Futuras

### Adicionar Novo Campo a Funcionário
1. Editar `drizzle/schema.ts` (adicionar coluna)
2. Executar `pnpm drizzle-kit generate`
3. Aplicar SQL via `webdev_execute_sql`
4. Atualizar `server/db.ts` (query helpers)
5. Atualizar `server/routers.ts` (endpoints)
6. Atualizar UI em `client/src/pages/EmployeesManagement.tsx`
7. Adicionar testes em `server/employees.test.ts`

### Adicionar Nova Rota tRPC
1. Editar `server/routers.ts`
2. Adicionar novo router ou procedure
3. Usar `adminProcedure` para rotas protegidas
4. Adicionar testes em arquivo correspondente
5. Chamar via `trpc.*.useQuery/useMutation` no frontend

### Upload de Novo Tipo de Arquivo
1. Adicionar novo router em `server/routers.ts` (similar a `uploadPhoto`)
2. Adicionar validação de tamanho/tipo
3. Usar `storagePut` para S3
4. Adicionar componente UI (similar a `ImageUploadField`)
5. Testar com arquivo real

## ⚠️ Limitações Conhecidas

- Portal de funcionários não implementado (apenas admin)
- Notificações apenas via API (sem email/SMS)
- Sem suporte a múltiplas empresas
- Sem API pública para integrações externas

## 🤝 Suporte

Para dúvidas ou problemas:
1. Verifique logs em `.manus-logs/`
2. Consulte testes em `server/*.test.ts`
3. Revise documentação inline no código
4. Contate suporte do Manus

---

**Versão**: 1.0.0  
**Última atualização**: 2026-04-10  
**Status**: Pronto para produção
