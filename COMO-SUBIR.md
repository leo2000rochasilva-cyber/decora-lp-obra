# Como subir a LP Decora (URL de validação antes do domínio)

Esta pasta tem tudo que o site precisa:
- `index.html` — a landing page
- `Institucional.mp4` — o vídeo da fábrica (precisa ficar na mesma pasta do index.html)

É um site **estático**. Escolha um dos caminhos abaixo. Recomendo o A pra ter URL na hora.

---

## Opção A — Netlify Drop (mais rápido, ~30 segundos, grátis)

1. Acesse **https://app.netlify.com/drop**
2. Faça login (pode usar a conta do Google/GitHub).
3. **Arraste a pasta `decora-lp-deploy` inteira** para a área de "Drag and drop".
4. Pronto: sai uma URL aleatória tipo `https://nome-aleatorio-123.netlify.app`.
5. Para trocar o nome: *Site configuration → Change site name*.
6. Quando quiser o domínio: *Domain management → Add a domain* (e aponta o DNS do seu domínio).

---

## Opção B — GitHub + Easypanel (seu stack)

**1. Subir no GitHub**
- Crie um repositório novo (ex.: `decora-lp`).
- Suba os 2 arquivos na **raiz** do repo: `index.html` e `Institucional.mp4`.
  (Pode arrastar os arquivos direto na interface do GitHub: *Add file → Upload files*.)

**2. Deploy no Easypanel**
- New → **App** (ou *Service*).
- Source: **GitHub** → selecione o repo `decora-lp` e a branch `main`.
- Tipo de build: **Static** (Nginx). Se pedir:
  - Build command: *(deixe vazio)*
  - Output / publish directory: `.` (a raiz, onde está o index.html)
- Salve e faça o Deploy. O Easypanel gera um subdomínio aleatório
  (ex.: `decora-lp.SEUSERVIDOR.easypanel.host`).
- Depois: aba **Domains** → adiciona seu domínio + ativa o SSL (Let's Encrypt).

> Se o Easypanel exigir um Dockerfile pra servir estático, me avisa que eu te entrego
> um `Dockerfile` com nginx pronto (copia os arquivos para `/usr/share/nginx/html`).

---

## Opção C — GitHub Pages (grátis, sem Easypanel)

1. Suba `index.html` + `Institucional.mp4` num repo (ex.: `decora-lp`).
2. No repo: *Settings → Pages → Source: Deploy from a branch → main / root → Save*.
3. Em ~1 min sai a URL `https://SEU-USUARIO.github.io/decora-lp/`.
4. Domínio depois: *Pages → Custom domain*.

---

## Observações

- O formulário hoje só mostra "recebemos" — **ainda não salva o lead**. Antes de rodar
  anúncio de verdade, a gente liga ele (Supabase/Formspree). Me chama pra isso.
- A página está com as imagens embutidas (~4 MB). Carrega ok, mas dá pra deixar
  bem mais rápida externalizando as imagens — opcional, pra quando escalar tráfego.
