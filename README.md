# Givanildo | Massagem Quântica

Aplicação web conectada ao projeto Supabase existente. O frontend respeita os nomes das tabelas, colunas, papéis, funções e políticas RLS que já estão configurados no banco. Nenhuma tabela foi recriada ou renomeada.

## Executar localmente
1. Copie `.env.example` para `.env.local`.
2. Preencha `VITE_SUPABASE_URL` e `VITE_SUPABASE_PUBLISHABLE_KEY` com os valores públicos do projeto.
3. Execute `npm install` e `npm run dev`.

## Estrutura Supabase usada
- Perfis e acesso: `profiles`, `clients`, `private.user_roles`, função `public.current_user_role()`.
- Catálogo: `services`, `products`.
- Agenda: `availability_rules`, `blocked_dates`, `appointments`, `appointment_history`.
- Dados privados: `anamnesis_forms`, `payments`, `notifications`.
- Configurações e auditoria: `clinic_public_settings`, `clinic_private_settings`, `audit_logs`.

## Segurança
- O navegador usa somente a chave publishable. Nunca adicionar `service_role` ao frontend.
- O painel administrativo exige papel `admin` e MFA AAL2, conforme as políticas existentes.
- Anamnese e dados pessoais são acessados pelas políticas RLS existentes.
- O projeto não contém migrações SQL e não altera o schema Supabase.

## Importante sobre agendamentos e integrações
O formulário grava solicitações com status `requested` e informa que o horário depende de confirmação manual. O banco atual não expõe uma função de disponibilidade que filtre conflitos nem possui trigger de prevenção de sobreposição; por isso a interface não promete confirmação automática ou disponibilidade garantida.
Pagamentos online e envio automático de e-mail/WhatsApp não estão integrados: precisam de provedor, credenciais e fluxo de webhook próprios.
