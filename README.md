# apps/links — página "link na bio"

Página estática (HTML + JSON, sem backend) que lista os 10 produtos com botão para a loja. É para onde apontam as bios do Instagram e do YouTube (o TikTok aponta para o Instagram até ter 1.000 seguidores).

## Como funciona
- `index.html` lê `links.json` e monta os cartões.
- O parâmetro `?c=` diz de qual rede a pessoa veio e escolhe o link de afiliado com o **sub_id** certo:
  - Instagram (bio): `https://SEU-DOMINIO/?c=ig`
  - YouTube (aba Links): `https://SEU-DOMINIO/?c=yt`
  - TikTok (quando liberar o link): `https://SEU-DOMINIO/?c=tt`
- Enquanto um produto não tem link de afiliado, o botão usa `fallback` (link normal da loja, sem comissão). **Troque pelos links de afiliado assim que a Shopee e o Mercado Livre aprovarem.**
- Aviso de #publi fixo no topo (exigência das redes e do CONAR). Quando entrar a Amazon, acrescentar a frase de associado no `aviso`.

## Ativar/ocultar produtos
Cada produto em `links.json` tem `"ativo": true|false`. Produto com `ativo: false` não aparece na página (usado para a Shopee até a aprovação do programa, 08/10/2026). Para reativar: mude para `true` e publique.

## Preencher os links
Em `links.json`, para cada produto, cole em `links.tt`, `links.ig` e `links.yt` o link gerado no portal do programa com o sub_id correspondente (`tt01`, `ig01`, `yt01` para o produto 01, e assim por diante). Mercado Livre: se o painel não oferecer sub_id, use o mesmo link nos três campos.

## Onde está no ar
Repositório público `resolvenacozinha/resolvenacozinha-links` (GitHub Pages, raiz da branch main):
`https://resolvenacozinha.github.io/resolvenacozinha-links/`. Publicar/atualizar: `python scripts/publicar_links.py` (ver docstring; `--set NN tt|ig|yt|ml URL` troca um link e publica). O clone de trabalho fica em `D:/Projects/resolvenacozinha-links` e usa só a credencial do `gh` (conta resolvenacozinha).

## Hospedar em outro lugar (alternativas)
Opção A — **GitHub Pages:** crie um repositório público só com esta pasta (ou use a pasta `apps/links` como fonte do Pages) → Settings → Pages → Deploy from branch. URL do tipo `usuario.github.io/resolvenacozinha`.
Opção B — **Cloudflare Pages:** conecte o repositório ou faça upload direto da pasta. Permite domínio próprio (`resolvenacozinha.com.br`) e tem analytics gratuito.
Opção C — enquanto não hospeda: Beacons/Linktree com um botão por produto (sem sub_id por rede).

## Testar localmente
```bash
python -m http.server 8090 --directory apps/links
```
Abra `http://localhost:8090/?c=ig`.

## Próximos passos (Fase 1)
Contador de cliques por vídeo (`/go/<slug>?v=cz-001`) com Cloudflare Pages Functions ou Umami, alimentando o funil views → cliques → vendas.
