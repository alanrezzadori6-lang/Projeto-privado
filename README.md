# Site Institucional — Médico Perito Judicial e Assistente Técnico

Site estático de página única (HTML5 semântico + Tailwind CSS via CDN + JavaScript puro). Não precisa de build nem de servidor: pronto para GitHub Pages.

## Estrutura

```
index.html   # site completo (HTML, configuração do Tailwind, CSS e JS)
README.md    # este guia
```

Seções: Hero · Áreas de Atuação · Metodologia · Perfil Técnico · Contato (formulário + WhatsApp).

## 1. Personalizar os dados

Abra `index.html` e ajuste:

| O quê | Onde |
|---|---|
| WhatsApp, e-mail, telefone, mensagem inicial de triagem | objeto `CONFIG` no `<script>` no fim do arquivo |
| Nome, CRM | busque por `Álan Rezzadori`, `64436` |
| Credenciais acadêmicas | seção `id="perfil"` → bloco "Credenciais Acadêmicas" |
| Comarcas / regiões | seção `id="perfil"` → bloco "Comarcas e Regiões de Atendimento" |
| Título e descrição (SEO) | `<title>` e `<meta name="description">` no `<head>` |
| Cores | `tailwind.config` no `<head>` (`navy`, `steel`, `graphite`) |

Formato do WhatsApp em `CONFIG.whatsapp`: apenas dígitos, com DDI e DDD. Ex.: `5511987654321`.

## 2. Testar localmente

Basta abrir `index.html` no navegador (duplo clique). Opcional, com servidor local:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000
```

## 3. Publicar no GitHub Pages

1. **Criar o repositório** — em github.com → *New repository*. Para o endereço `https://SEU-USUARIO.github.io`, nomeie-o `SEU-USUARIO.github.io`; qualquer outro nome gera `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.
   > Em contas gratuitas, o GitHub Pages exige repositório **público**.
2. **Enviar os arquivos**
   - Pela web: *Add file → Upload files* → arraste `index.html` e `README.md` → *Commit changes*.
   - Pelo terminal:
     ```bash
     git init
     git add index.html README.md
     git commit -m "Site institucional"
     git branch -M main
     git remote add origin https://github.com/SEU-USUARIO/NOME-DO-REPO.git
     git push -u origin main
     ```
3. **Ativar o Pages** — no repositório: *Settings → Pages → Build and deployment*:
   - *Source*: **Deploy from a branch**
   - *Branch*: **main** / pasta **/(root)** → *Save*
4. **Aguardar 1–3 min** e acessar a URL exibida no topo da página *Settings → Pages*.
5. **Atualizações** — cada novo commit em `main` republica o site automaticamente.

### Domínio próprio (opcional)

1. *Settings → Pages → Custom domain* → informe `www.seudominio.com.br` → *Save* (o GitHub cria o arquivo `CNAME`).
2. No provedor de DNS (ex.: Registro.br):
   - `www` → registro **CNAME** apontando para `SEU-USUARIO.github.io`
   - Domínio raiz (opcional) → registros **A**: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. Após a propagação, marque **Enforce HTTPS**.

## 4. Formulário de contato

Sem backend (GitHub Pages é estático). O formulário valida os campos e oferece dois envios:

- **Enviar por e-mail** — abre o cliente de e-mail com assunto e corpo preenchidos (`mailto:`).
- **Enviar via WhatsApp** — abre conversa com os dados formatados.

Para receber envios diretamente na caixa de entrada sem depender do cliente de e-mail, use um serviço como [Formspree](https://formspree.io): crie um formulário, adicione `action="https://formspree.io/f/SEU_ID" method="POST"` ao `<form id="contatoForm">` e remova o `ev.preventDefault()` do script (ou envie via `fetch`).

## 5. Conformidade

- Publicidade médica: revise o conteúdo à luz da **Resolução CFM nº 2.336/2023** (sem promessas de resultado, com CRM visível; RQE apenas se houver especialidade registrada).
- LGPD: o formulário inclui consentimento explícito e alerta contra envio de dados sensíveis.
