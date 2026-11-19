# BiblioHub — publicar esta versão no Render

**Esta versão não usa React/Vite.** É um site HTML/CSS/JavaScript com API Node.js (`node:http`) e banco SQLite (`node:sqlite`). **Escolha Web Service**, não Static Site.

## 1. Coloque os arquivos no GitHub

Extraia o ZIP no computador. Envie **o conteúdo** (e não a pasta externa) ao repositório. Na página inicial devem aparecer `backend/`, `public/`, `package.json` e `render.yaml`.

Se preferir manter tudo dentro de uma pasta, o **Root Directory** do Render deve ser exatamente o caminho da pasta que contém o `package.json`.

## 2. Configure no Render

Render → New → Web Service → GitHub → selecione o repositório.

| Campo | Valor |
|---|---|
| Language | Node |
| Branch | main |
| Root Directory | vazio se `package.json` está na raiz |
| Build Command | `npm install` |
| Start Command | `npm start` |
| Instance | Free (se disponível) |

Configure em Environment Variables:
- `NODE_ENV` = `production`
- `DEMO_READER_ENABLED` = `true` (para usar a conta de demonstração)
- `ADMIN_EMAIL` = e-mail do administrador escolhido por você
- `ADMIN_PASSWORD` = senha secreta e exclusiva, com **no mínimo 12 caracteres**
- `NODE_VERSION` = `22.16.0` (opcional; garante `node:sqlite`)

**Não configure PORT manualmente.** O Render informa a porta ao servidor.

Depois clique em **Deploy Web Service**.

## 3. Teste

Acesse `https://SEU-SERVICO.onrender.com/api/health` e verifique se a resposta contém `"ok":true`.
Abra o endereço principal e teste a conta demo `aluno@bibliohub.edu.br` / `biblioteca123`, se `DEMO_READER_ENABLED=true`.

Para entrar como administrador, use `ADMIN_EMAIL` e `ADMIN_PASSWORD` que configurou no Render.

## Atenção: dados NÃO persistentes no serviço gratuito

O SQLite é salvo no disco local do serviço. Em instâncias gratuitas do Render, reinicializações e novos deployments podem apagar os cadastros, empréstimos e livros adicionados. Esta configuração serve para **apresentação e testes**, nunca para guardar dados reais de alunos. Para permanência, é necessário banco externo persistente ou disco persistente em plano compatível.

## Teste local / Codespaces

`npm start` abre a porta 5173 no ambiente Codespaces. `npm run check` verifica sintaxe. A versão local preserva as contas de exemplo anteriores quando `NODE_ENV` não for `production`.
