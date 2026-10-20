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

## Identidade

A marca é tipográfica: o nome em Sora, e o acento do ê é um arco laranja, um
pedaço do anel do símbolo do Grupo Gênesis Brasil. Ela é texto e SVG inline,
então muda de tamanho e cor com a página. Três variáveis no topo da folha de
estilo controlam o arco (largura, altura e distância do e).

| Papel | Cor |
| --- | --- |
| Fundo escuro e texto no claro | `#0b0b0c` |
| Cartões sobre o escuro | `#141416` |
| Destaque (arco da marca, botão principal, ícones) | `#F57129`, `#ff8c4a` sobre o escuro |
| Fundo claro | `#f4f2ef` |

Tipografia: Sora nos títulos e Source Sans 3 no texto, via Google Fonts.
Ícones em SVG inline, no traço do Lucide.

## Estrutura

```
index.html
assets/
  styles.css      tokens, componentes e três pontos de quebra (1100, 980, 720)
  main.js         menu do celular, entrada suave das seções, formulário por e-mail
  img/            favicon (SVG e PNG) e fotos
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
aws s3 sync . s3://<bucket>/ --delete --exclude ".git/*" --exclude ".gitignore" --exclude "README.md" --exclude "LICENSE"
aws cloudfront create-invalidation --distribution-id <id> --paths "/*"
```

## Licença

O código (HTML, CSS e JavaScript) está sob a licença MIT. A marca Banco
Gênesis Brasil, os textos institucionais e as fotos pertencem ao Banco Gênesis
Brasil e não estão cobertos pela licença.
