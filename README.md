# Agendamento de Exames Ocupacionais — DETRAN-RR

Página estática (single-file) para agendamento de exames ocupacionais.
Backend 100% no Supabase — não há build. É só publicar o `index.html`.

## Publicar no Render (subdomínio novo: agendamento.protecaorr.net)

1. **Criar repositório no GitHub** (conta `Haroldo7777`), ex.: `agendamento-exames`,
   e enviar esta pasta (veja comandos no fim).

2. **Render → New → Static Site**
   - Connect repository: `Haroldo7777/agendamento-exames`
   - Branch: `main`
   - Build Command: *(deixar vazio)*
   - Publish Directory: `.`
   - Create Static Site. Em ~1 min sai no ar num endereço `*.onrender.com`.

3. **Custom Domain** (dentro do serviço → Settings → Custom Domains)
   - Add Custom Domain: `agendamento.protecaorr.net`
   - O Render mostra um alvo de **CNAME** (algo como `agendamento-exames.onrender.com`).

4. **DNS** (no painel onde está o domínio `protecaorr.net`)
   - Criar registro: **CNAME** | Host/Nome: `agendamento` | Valor: o alvo `*.onrender.com` que o Render indicou.
   - Salvar. Propaga em minutos; o Render emite o certificado HTTPS automático.

Pronto: `https://agendamento.protecaorr.net`.

## Enviar para o GitHub (a partir desta pasta)

```bash
gh auth login          # se ainda não estiver logado
gh repo create Haroldo7777/agendamento-exames --public --source=. --remote=origin --push
```

Ou manualmente, se o repo já existir:

```bash
git add -A
git commit -m "Publica agendamento de exames ocupacionais"
git branch -M main
git remote add origin https://github.com/Haroldo7777/agendamento-exames.git
git push -u origin main
```

## Observação de segurança
O login do gestor (`Área do Gestor`) é validado só no navegador — e-mail/senha
estão embutidos no `index.html` (base64), então qualquer pessoa que abrir o
código-fonte consegue lê-los. A chave do Supabase é a `anon` (pública, ok).
Se o painel do gestor precisar ser realmente restrito, mova a autenticação para
o Supabase Auth + RLS. Posso fazer isso depois, se quiser.

## Publicar o Auditor eSocial (esocial.protecaorr.net)

A página provisória do Auditor está em `esocial/index.html`. Para colocá-la no ar
como um **segundo site estático** a partir deste mesmo repositório:

1. **Render → New → Static Site**
   - Connect repository: `Haroldo7777/agendamento-exames`
   - Branch: `main`
   - Build Command: *(deixar vazio)*
   - **Publish Directory: `esocial`**
   - Create Static Site.

2. **Custom Domain** (Settings → Custom Domains do novo serviço)
   - Add Custom Domain: `esocial.protecaorr.net`
   - O Render mostra o alvo de **CNAME** (algo como `auditor-esocial.onrender.com`).

3. **DNS** (painel do domínio `protecaorr.net`)
   - **CNAME** | Host/Nome: `esocial` | Valor: o alvo `*.onrender.com` indicado.
   - Propaga em minutos; HTTPS automático.

Quando o sistema real do Auditor (Fase 1 do `PLANO_FASE_1_AUDITOR.md`) tiver
repositório próprio, basta repontar esse serviço do Render para o novo repo —
o domínio `esocial.protecaorr.net` continua o mesmo.
