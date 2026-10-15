# Presell — Cookie Popup (Jointvive)

Página estática servida por nginx em Docker, pronta para o Easypanel.

## Arquivos

- `index.html` — a página
- `Dockerfile` — imagem nginx:alpine que serve o `index.html`
- `nginx.conf` — qualquer caminho do domínio cai no `index.html`

## Deploy no Easypanel (VPS Hostinger)

1. **GitHub no Easypanel** (só na primeira vez): Easypanel → *Settings* → *GitHub* → cole um token do GitHub com acesso ao repositório.
2. **Criar o serviço**: abra (ou crie) um *Project* → **+ Service** → **App**.
3. **Source** → **GitHub**: escolha o *owner*, o repositório e a branch `main` → **Save**.
4. **Build** → selecione **Dockerfile** (caminho: `Dockerfile`) → **Save**.
5. Clique em **Deploy** e espere o build ficar verde.
6. **Domains** → **Add Domain**: coloque o domínio/subdomínio (ex.: `oferta.seudominio.com`), porta **80**, HTTPS ligado → **Save**.
7. **DNS** (painel da Hostinger ou onde o domínio estiver): crie um registro **A** apontando o domínio/subdomínio para o IP da VPS. O SSL sai sozinho em alguns minutos depois que o DNS propagar.
8. (Opcional) Ligue **Auto Deploy** no serviço: todo `git push` na `main` publica sozinho.

## Atualizar a página

Edite o `index.html`, faça commit e push. Com Auto Deploy ligado, o Easypanel republica; sem ele, clique em **Deploy** de novo.

## Testar localmente

```bash
python3 -m http.server 8765
```

Depois abra `http://localhost:8765/?utm_source=teste` e confira que os links ficam `...indexvs.php?utm_source=teste#aff=fvidalx`.
