# Subir a LP no Easypanel + subdomínio na GoDaddy

Subdomínio escolhido: **obra.decoraesquadrias.com.br**
(se quiser outro, ex.: `suprema`, é só trocar onde aparecer `obra`.)

Esta pasta já está pronta pra deploy: `index.html`, `assets/`, `Institucional.mp4`,
`Dockerfile` (nginx), `robots.txt`, `sitemap.xml`.

---

## Passo 1 — Subir os arquivos no GitHub

1. Crie um repositório novo (ex.: `decora-lp-obra`).
2. Suba **todo o conteúdo desta pasta** na raiz do repo
   (`index.html`, a pasta `assets/`, `Institucional.mp4`, `Dockerfile`, `robots.txt`, `sitemap.xml`).
   - Pela web do GitHub: *Add file → Upload files* → arrasta tudo → Commit.

## Passo 2 — Criar o serviço no Easypanel

1. No seu projeto do Easypanel: **+ Service → App**.
2. **Source:** GitHub → selecione o repo `decora-lp-obra`, branch `main`.
3. **Build:** o Easypanel vai detectar o **Dockerfile** automaticamente (nginx). Não precisa
   build command nem start command.
4. Clique em **Deploy**. Em ~1 min o serviço sobe (porta 80, servida pelo nginx).
5. Teste pelo domínio temporário que o Easypanel gera
   (`...easypanel.host`) só pra ver se carregou.

## Passo 3 — Apontar o subdomínio na GoDaddy

1. GoDaddy → **My Products → DNS** do domínio `decoraesquadrias.com.br` → **Manage DNS**.
2. **Add Record:**
   - **Type:** A
   - **Name (Host):** `obra`
   - **Value:** o **IP do seu servidor Easypanel** (o mesmo IP onde roda o app/CRM).
   - **TTL:** 1 hora (padrão).
3. Salve. (A propagação leva de minutos a ~1h.)

> Não mexa nos registros do `@` e `www` — eles são a sua loja. Você só **adiciona** o `obra`.

## Passo 4 — Ligar o domínio no Easypanel (SSL automático)

1. No serviço do Easypanel → aba **Domains** → **Add Domain**.
2. Digite `obra.decoraesquadrias.com.br`.
3. Marque **HTTPS / SSL** (Let's Encrypt) — o Easypanel emite o certificado sozinho assim
   que o DNS estiver apontando.
4. Pronto: a LP fica em **https://obra.decoraesquadrias.com.br**.

## Passo 5 — Ligar a home da loja → LP

Na home do `decoraesquadrias.com.br`, adicione o botão/banner de direcionamento apontando
para `https://obra.decoraesquadrias.com.br`. (A LP já volta pra loja pelo logo/menu.)

---

## Observações

- O **formulário já salva** no seu Supabase (`lp_leads`). Antes de rodar anúncio,
  limpamos os leads de teste e você adiciona a **aba no CRM** que lê a `lp_leads`.
- Se trocar o subdomínio, me avisa que eu atualizo o `canonical`, `og:url` e o `sitemap.xml`.
