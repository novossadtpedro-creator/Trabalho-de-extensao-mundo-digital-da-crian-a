# Mundo Digital da Criança 2.0

Aplicação web responsiva para responsáveis e crianças organizarem rotina, aprendizagem e acordos digitais em família. A interface se inspira na composição da referência enviada, mas usa a identidade coral pedida no briefing.

## O que já funciona

- Cadastro, login, logout e recuperação de senha pelo Supabase Auth quando configurado.
- Modo local explícito para experimentar o aplicativo sem credenciais. Os dados ficam somente no `localStorage` do navegador.
- Perfis infantis com apelido, avatar e idade opcional.
- Rotinas por dia e horário, edição, exclusão e conclusão com histórico.
- Quiz educativo com pontuação e histórico.
- Acordos familiares, lista informativa de apps, pedidos de autorização e decisão pelo responsável.
- Registro manual de tempo de tela, limite acordado e relatórios semanais/mensais.
- Estrelinhas, marcos de aprendizagem, notificações, exportação dos dados locais e layout responsivo.
- Esquema PostgreSQL com relacionamentos e políticas RLS em `supabase/schema.sql`.

Não há dados de demonstração preenchidos: cadastre seus próprios registros para ver o painel e os relatórios ganharem conteúdo.

## Pré-requisitos

- Node.js LTS e npm.
- Para autenticação e sincronização: projeto Supabase próprio.

## Executar localmente

1. Abra um terminal nesta pasta.
2. Instale as dependências:

   ```powershell
   npm install
   ```

3. Inicie o servidor:

   ```powershell
   npm run dev
   ```

4. Abra o endereço local exibido pelo Vite.

Sem credenciais, a tela permite abrir o **modo local**. Esse modo não implementa autenticação: não use dados reais ou sensíveis de crianças nele.

## Configurar Supabase

1. Crie um projeto Supabase e configure a URL de redirecionamento de autenticação para a URL local e para os domínios de implantação.
2. No SQL Editor do seu projeto, execute `supabase/schema.sql`.
3. Copie `.env.example` para `.env.local` e informe a URL do projeto e a chave pública (publishable/anon). **Nunca** use uma chave `service_role` no navegador.
4. Reinicie o Vite depois de editar as variáveis.
5. Configure a confirmação de e-mail e o envio de recuperação de senha no Supabase antes de publicar.

O cadastro cria uma família e um perfil de responsável por meio de um trigger. O SQL ativa RLS e limita registros à família autenticada. Revise as políticas no seu próprio projeto Supabase antes de inserir quaisquer dados reais.

## Limites importantes e privacidade

- A área infantil é uma interface no mesmo espaço autenticado, não uma conta/sessão independente para a criança.
- A lista de aplicativos e os limites são **combinados informativos**; não bloqueiam apps.
- O tempo de tela é digitado manualmente por um responsável. Não há monitoramento, localização ou integração nativa com dispositivos.
- O modo local grava conteúdo no navegador sem criptografia própria. Use somente conteúdo fictício ou não sensível nesse modo.
- Antes de uso real, a organização responsável deve revisar consentimento, retenção, exclusão, segurança, termos e demais obrigações da LGPD para dados infantis.

## Estrutura

```text
src/
  App.tsx          Fluxos e telas
  domain.ts        Tipos e persistência local
  main.tsx         Inicialização React
  styles.css       Interface responsiva
  supabase.ts      Auth e persistência Supabase
supabase/
  schema.sql       PostgreSQL, relacionamentos e RLS
public/
  reference-ui.png Referência visual fornecida
```

## Verificação

```powershell
npm run build
```
