# Monitor · Vulcanização — publicar no GitHub e gerar o APK

## O que tem nesta pasta

| Arquivo | Para que serve |
|---|---|
| `index.html` | O app (o mesmo `monitor.html`, com o nome que o site precisa) |
| `manifest.webmanifest` | Nome, ícone e cores do app instalado |
| `sw.js` | Faz o app abrir e funcionar sem internet |
| `icons/` | Ícones do app |
| `screenshots/` | Imagens que aparecem na instalação e na Play Store |
| `.nojekyll` | Arquivo vazio. **Precisa ir junto**: sem ele o GitHub não publica a pasta `.well-known` (passo 5) |

---

## 1. Criar o repositório

1. Entre em **github.com** (crie a conta, se ainda não tiver).
2. Clique em **+** › **New repository**.
3. Em **Repository name**, escreva exatamente: `SEUUSUARIO.github.io`
   (troque SEUUSUARIO pelo seu nome de usuário do GitHub).
   Usar esse nome deixa o site na raiz do endereço, e isso é necessário para o APK abrir sem a barra do navegador.
4. Deixe **Public** marcado e clique em **Create repository**.

## 2. Enviar os arquivos

1. No repositório, clique em **uploading an existing file** (ou **Add file › Upload files**).
2. Arraste **o conteúdo desta pasta** (não a pasta em si, e não o .zip): `index.html`, `manifest.webmanifest`, `sw.js`, `.nojekyll` e as pastas `icons` e `screenshots`.
3. Clique em **Commit changes**.

> No Windows, se o `.nojekyll` não aparecer: Explorador de Arquivos › Exibir › marcar "Itens ocultos".

## 3. Ligar o site

1. No repositório: **Settings › Pages**.
2. Em **Source**, escolha **Deploy from a branch**; em **Branch**, escolha **main** e **/(root)**. Clique em **Save**.
3. Espere 1 a 3 minutos. O site fica em: `https://SEUUSUARIO.github.io`

**Teste no celular:** abra o endereço no Chrome. Já dá para instalar pelo menu **⋮ › Instalar app**, ou pela aba **Dados › Instalar como app**.

## 4. Gerar o APK no PWABuilder

1. Entre em **pwabuilder.com**, cole `https://SEUUSUARIO.github.io` e clique em **Start**.
2. Clique em **Package for stores** › **Android** › **Generate Package**.
   - **Package ID**: pode deixar o sugerido (ex.: `io.github.seuusuario.twa`). Não mude depois.
   - O resto pode ficar no padrão.
3. Baixe o `.zip`. Dentro dele vêm:
   - `.apk` → para instalar direto nos celulares
   - `.aab` → só se for publicar na Play Store
   - `signing.keystore` e `signing-key-info.txt` → **GUARDE EM LUGAR SEGURO.** Sem eles não dá para lançar atualização do APK depois.
   - `assetlinks.json` → usado no passo 5

## 5. Tirar a barra do navegador do APK

Sem este passo o APK funciona, mas mostra uma barra de endereço no topo.

1. No repositório: **Add file › Create new file**.
2. No nome do arquivo, digite: `.well-known/assetlinks.json` (a barra cria a pasta).
3. Cole todo o conteúdo do `assetlinks.json` que veio do PWABuilder e clique em **Commit changes**.
4. Espere 1 a 3 minutos e confira: `https://SEUUSUARIO.github.io/.well-known/assetlinks.json` precisa abrir mostrando o texto.

## 6. Instalar o APK nos celulares

1. Mande o `.apk` para o celular (WhatsApp, cabo, Drive…).
2. Toque no arquivo. O Android vai pedir para **permitir instalar apps desta fonte**: permita e instale.
3. Na primeira vez que usar o QR, autorize a câmera.

---

## Antes de trocar para o app instalado: leve os dados

O app instalado guarda os dados separado do navegador. Em cada celular:

1. No Monitor que já usa hoje: **Dados › Backup (.json)**.
2. No app novo: **Dados › Restaurar backup** e escolha o arquivo.

## Como atualizar o app depois

- Mudou só o app (correções, telas)? Suba o `index.html` novo no GitHub por cima do antigo (**Add file › Upload files**). Todo mundo recebe a versão nova ao abrir o app com internet. **Não precisa gerar outro APK.**
- Só precisa de APK novo se mudar o nome, o ícone ou as cores do app. Nesse caso use o PWABuilder de novo, com a mesma `signing.keystore`.

## Importante: o site é público

No GitHub gratuito o site fica aberto na internet. Quem tiver o endereço vê o app e o **cadastro de moldes** (artigos, tamanhos e cores) que vai dentro do `index.html`.
Os **registros das máquinas não vão para o site**: ficam só nos celulares.
