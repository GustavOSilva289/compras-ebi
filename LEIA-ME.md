# Compras EBI como aplicativo (PWA)

Pasta com tudo pronto: ícone, manifesto, service worker e a "casca" (index.html) que abre o seu sistema do Apps Script em tela cheia.

## Passo 1 — Liberar o Apps Script para abrir dentro da casca
No `doGet` do Code.gs, acrescente `.setXFrameOptionsMode(...)` e `.setFaviconUrl(...)` na mesma cadeia que você já usa:

    function doGet(e) {
      return HtmlService.createTemplateFromFile('Index').evaluate()
        .setTitle('Compras EBI')
        .addMetaTag('viewport', 'width=device-width, initial-scale=1')
        .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
        .setFaviconUrl('https://SEU-USUARIO.github.io/compras-ebi/icon-192.png');
    }

(Se o seu doGet já tem outras linhas, mantenha-as e só adicione essas duas.)

## Passo 2 — Nova versão da implantação
Implantar → Gerenciar implantações → editar (lápis) → Versão: **Nova versão** → Implantar.
Confira que o acesso está como "Qualquer pessoa" e copie o link que termina em `/exec`.

## Passo 3 — Colocar o link na casca
Abra `index.html` e troque `COLE_AQUI_O_LINK_DO_WEB_APP/exec` pelo link do passo 2.

## Passo 4 — Publicar a pasta (grátis, GitHub Pages)
1. Crie um repositório público, por exemplo `compras-ebi`.
2. Envie todos os arquivos desta pasta para a raiz do repositório.
3. Settings → Pages → Branch `main`, pasta `/ (root)` → Save.
4. Em 1–2 minutos o endereço fica `https://SEU-USUARIO.github.io/compras-ebi/`.

## Passo 5 — Instalar no celular
- **Android (Chrome):** abra o endereço → menu ⋮ → "Instalar app" (ou "Adicionar à tela inicial").
- **iPhone (Safari):** abra o endereço → Compartilhar → "Adicionar à Tela de Início".

O ícone azul da prancheta com check aparece na tela inicial com o nome "Compras EBI".

## Observações
- Login com conta Google não funciona dentro de iframe. Com o login atual (e-mail e senha do próprio sistema) funciona normalmente.
- Se mudar o ícone depois, aumente `VERSAO` no `sw.js` (ex.: `ebi-v2`) para os celulares atualizarem.
- `icon-maskable-512.png` é a versão sem cantos, usada pelo Android.
