# Deploy

O site é servido por nginx em `45.234.69.132`, no docroot `/var/www/leaomartins`.
O domínio aponta direto para esse IP (sem CDN na frente).

## Acesso

Autenticação por chave, sem senha. O alias `leao-vps` está em `~/.ssh/config`:

```
Host leao-vps
    HostName 45.234.69.132
    User link
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

## Publicar

```bash
scp index.html og-image.png apple-touch-icon.png robots.txt sitemap.xml \
    leao-vps:/var/www/leaomartins/
ssh leao-vps 'cd /var/www/leaomartins && chmod 644 *.html *.png *.txt *.xml'
```

> **O `chmod` não é opcional.** Os arquivos deste repo estão com modo `600` no macOS.
> O nginx roda como `www-data` e devolve **403** em arquivo que não consegue ler.
>
> **Não use `rsync -a` daqui.** O rsync que vem no macOS é a versão 2.6.9, não aceita
> `--chmod`, e o `-a` preserva justamente o `600` que causa o 403. Pior: ele falha
> em silêncio o suficiente para parecer que publicou. Use `scp` + `chmod`.

Depois de publicar, confira que o conteúdo novo está mesmo no ar — comparar o md5 local
com o do servidor pega o caso em que o envio não aconteceu:

```bash
md5 -q index.html
ssh leao-vps 'md5sum /var/www/leaomartins/index.html'
```

## nginx

`nginx-leaomartins.com.br.conf` é cópia fiel de
`/etc/nginx/sites-available/leaomartins.com.br`. Ao alterar, sempre:

```bash
sudo cp /etc/nginx/sites-available/leaomartins.com.br ~/vhost-leaomartins-$(date +%F-%H%M%S).bak
sudo cp novo.conf /etc/nginx/sites-available/leaomartins.com.br
sudo nginx -t          # valida os 13 sites do servidor, não só este
sudo systemctl reload nginx
```

Use `reload`, nunca `restart`: o servidor hospeda 13 sites em produção e o `reload`
troca a configuração sem derrubar conexão.

### O que a configuração faz

- **301 de HTTP para HTTPS** e **301 de `www` para o domínio sem `www`**, para o mesmo
  conteúdo não existir em três endereços.
- `/.well-known/acme-challenge/` **fica de fora do redirect**. O certbot deste domínio usa
  o autenticador `nginx` (veja `/etc/letsencrypt/renewal/leaomartins.com.br.conf`); se a
  renovação esbarrar no 301, o certificado não renova e o site cai de HTTPS em 90 dias.
- `gzip_types` no server block. O `gzip on` global já existe no `nginx.conf`, mas o
  `gzip_types` padrão cobre só `text/html`. Com isso a página caiu de 44 KB para 13 KB.
- Imagens e fontes com `expires 30d`; `index.html` com `Cache-Control: no-cache`, porque
  o deploy troca o arquivo no lugar.
- `X-Content-Type-Options`, `X-Frame-Options` e `Referrer-Policy`.

> Os cabeçalhos de segurança aparecem repetidos em cada `location`. Não é descuido: no
> nginx, um `location` que tem o seu próprio `add_header` **descarta todos os `add_header`
> herdados do server block**. Removendo as repetições, as rotas de asset e de index.html
> ficam sem cabeçalho de segurança.

### Decisões deliberadas

**HTTP/2 não foi ligado.** No nginx 1.18 o parâmetro `http2` do `listen` vale para o
socket inteiro (`:443`), não para o server block. Ligar aqui mudaria o protocolo dos
outros 12 sites do servidor de uma vez — não cabe numa alteração do site pessoal.
Vale fazer, mas como mudança combinada e verificada para todos.

**HSTS não foi ligado.** `Strict-Transport-Security` é bom para SEO e segurança, mas é
de difícil reversão: o navegador passa a recusar HTTP para o domínio durante todo o
`max-age`, mesmo que o certificado expire. Se for ligar, comece com `max-age=300`,
confirme que nada quebrou e só então aumente.

## Backups no servidor

- `~/leaomartins-backup-<timestamp>.tar.gz` — docroot anterior (site de março + logo).
- `~/vhost-leaomartins-<timestamp>.bak` — vhost anterior ao 301.

Para reverter o site: `tar -xzf ~/leaomartins-backup-<ts>.tar.gz -C /var/www`
