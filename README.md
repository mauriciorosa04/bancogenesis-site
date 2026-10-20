# Banco Gênesis Brasil, site institucional

Site do Banco Gênesis Brasil, organização de Curitiba voltada ao
desenvolvimento sustentável sistêmico: crédito e fomento, fundos e garantias,
consultoria, projetos e conexão com o mercado financeiro.

Uma página só, estática, sem framework e sem build: um arquivo HTML, uma
folha de estilo e um script de 40 linhas. Abre em qualquer servidor de arquivos
e fica nítido em qualquer tela, porque tudo que não é foto é vetor ou fonte.

## O que tem

- **Abertura** com os dois caminhos do visitante: conhecer as soluções ou
  propor parceria.
- **Quem somos**, com os quatro pilares da instituição.
- **Soluções**, as seis frentes de atuação: crédito e fomento, conta digital e
  pagamentos, fundos e garantias, consultoria e capacitação, projetos e
  concessões, mercado financeiro e negócios.
- **Para quem**: os oito perfis atendidos, da pessoa física ao poder público.
- **Diferenciais**, **Investimento e parceria** e **Contato**, com formulário
  que monta a mensagem e abre o programa de e-mail do visitante.
- Páginas de Termos de Uso e Política de Privacidade, escritas para o que o
  site faz de verdade: não grava cookies nem dados, e o contato vai por e-mail.

## Identidade

A marca é o monograma BG (o B atrás, o G do Grupo Gênesis Brasil na frente)
com o nome em Sora. Os arquivos em vetor, com o texto convertido em curvas,
estão em `marca/final/`; o site usa `assets/img/marca-horizontal.svg` no topo
e no rodapé e o símbolo sozinho no favicon.

| Papel | Cor |
| --- | --- |
| Marinho, fundo escuro e texto no claro | `#0f1f3d` |
| Cartões sobre o marinho | `#1a2d52` |
| Dourado (G da marca, botão principal, ícones) | `#c9a24a`, `#e0bf6a` sobre o escuro, `#8a6a1e` sobre o claro |
| Areia, fundo claro | `#f4f2ef` |

Tipografia: Sora nos títulos e Source Sans 3 no texto, via Google Fonts.
Ícones em SVG inline, no traço do Lucide.

## Estrutura

```
index.html
termos-de-uso.html
politica-de-privacidade.html
assets/
  styles.css      tokens, componentes e três pontos de quebra (1100, 980, 720)
  main.js         menu do celular, entrada suave das seções, formulário por e-mail
  img/            marca em SVG, favicon (SVG e PNG) e fotos
marca/
  final/          a marca em vetor: horizontal, empilhada e símbolo, nas duas paletas
  *.svg, png/     o estudo que levou à marca (caminhos descartados incluídos)
```

## Rodar localmente

```bash
python3 -m http.server 5191
```

e abrir http://localhost:5191.

## Publicar

O site é servido por um bucket S3 privado atrás de uma distribuição CloudFront.
Qualquer hospedagem de arquivos estáticos serve igual: é só copiar os arquivos.

```bash
aws s3 sync . s3://<bucket>/ --delete --exclude ".git/*" --exclude ".gitignore" --exclude "README.md" --exclude "LICENSE" --exclude "marca/*"
aws s3 cp politica-de-privacidade.html s3://<bucket>/politica-de-privacidade --content-type "text/html; charset=utf-8"
aws s3 cp termos-de-uso.html s3://<bucket>/termos-de-uso --content-type "text/html; charset=utf-8"
aws cloudfront create-invalidation --distribution-id <id> --paths "/*"
```

As duas cópias sem extensão existem porque os links do site são
`/termos-de-uso` e `/politica-de-privacidade`. A pasta `marca/` fica fora da
hospedagem: é material de identidade, não página.

## Licença

O código (HTML, CSS e JavaScript) está sob a licença MIT. A marca Banco
Gênesis Brasil, os textos institucionais e as fotos pertencem ao Banco Gênesis
Brasil e não estão cobertos pela licença.
