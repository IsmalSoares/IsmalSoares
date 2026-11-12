# Soares Design Estratégico — soaresdesign.com.br

Este arquivo é a memória do projeto para qualquer sessão futura do Claude Code que abrir esta pasta.
Leia isto antes de continuar o trabalho.

## O que é este projeto

O site soaresdesign.com.br **não nasceu como repositório de código**: foi autorado como páginas
Claude Artifact (claude.ai) e publicado manualmente na hospedagem (export → upload). Esta pasta
`site/` é uma cópia de trabalho local dessas páginas, criada para revisar e corrigir antes de
subir de novo na hospedagem.

Páginas-fonte originais no Claude (Artifacts, propriedade do usuário):
- Home (`index.html`, canonical `https://soaresdesign.com.br/`): https://claude.ai/artifact/M2ndEcBjndb91VfueAFujx
- Subpágina regional (`consultoria-de-marca-jundiai-campinas.html`): https://claude.ai/artifact/S3rC3Q3rWV9Mg4EkDpR4m9
- Guia de branding (`guia-de-branding.html`): https://claude.ai/artifact/BdoLoMwUV9usiYAWhr2vUa

**IMPORTANTE — fora de sincronia:** só o artifact da subpágina (S3rC3Q3rWV9Mg4EkDpR4m9) foi
republicado com as correções. O artifact da home (M2ndEcBjndb91VfueAFujx) ainda está na versão
antiga (title duplicado, galerias por clique, logos "em breve"). Os arquivos locais em `site/`
já têm tudo corrigido. Antes de considerar o trabalho "pronto", decidir: ou republicar os
artifacts do Claude a partir destes arquivos locais, ou tratar só os arquivos locais como fonte
de verdade a partir de agora.

## Problema original e causa raiz

Busca "Soares Design Estratégico" no Google mostrava dois resultados confusos (um "certo", um
"errado"). Causa raiz encontrada: `index.html` e `consultoria-de-marca-jundiai-campinas.html`
tinham `<title>` idêntico e 3 perguntas de FAQ (schema.org FAQPage) com texto 100% duplicado.

## O que já foi corrigido

1. **Título/meta duplicados**: `consultoria-de-marca-jundiai-campinas.html` agora tem
   `<title>`, `og:title` e `twitter:title` diferentes da home.
2. **FAQ duplicado**: removidas da subpágina as 3 perguntas idênticas à home; mantida só a
   pergunta exclusiva, com link "veja outras perguntas" apontando para `index.html#faq`.
3. **Imagens renomeadas e indexáveis**: todas as ~48 fotos de portfólio e os 7 logos tinham
   nomes genéricos numerados (`01.jpg`...) carregados por um script que só buscava arquivo por
   arquivo via JS (`probeImages`). Isso foi trocado por:
   - Nomes descritivos (`strahl-catalogo-tecnico.jpg`, `logo-ouviden.png`, etc.)
   - `alt` específico por imagem
   - Miniaturas reais e visíveis no HTML desde o carregamento (não mais escondidas atrás de um
     clique no botão "Portfólio") — o lightbox agora só amplia a imagem, não é mais quem
     "descobre" se ela existe.
   - Isso também resolveu sozinho 2 dos 3 textos provisórios do relatório original: "Logos em
     breve" e "Ainda não há imagens neste portfólio" não aparecem mais (há imagens reais).

## O que ainda falta (não resolvido)

- **Foto do retrato**: `Foto-Consultor.jpg` não existe. O placeholder "Retrato a inserir"
  continua na seção Sobre. Precisa de uma foto real do Ismael.
- **`/contato` retorna 404 no site ao vivo**: não existe mais página `/contato`, hoje é só a
  seção `#contato` da home. Correção não é recriar a página, é configurar um **redirect 301**
  de `/contato` para `/#contato` no painel da hospedagem — isso só o usuário consegue fazer,
  não é algo editável nestes arquivos.
- **Serviços e Agroindústria ainda são âncoras** (`#servicos`, `#agroindustria`) dentro da home,
  não páginas próprias — item 4 do relatório original de SEO ainda pendente, não confirmado se
  o usuário quer essa mudança.
- **Upload para hospedagem**: processo é manual (usuário exporta/sobe os arquivos). Depois de
  subir, usar o Search Console (Inspeção de URL) para pedir reindexação da home e da subpágina.
- **Remote Control**: tentativas de conectar a pasta local do usuário
  (`/Users/ismaelsoares/sites/Soares-design/site`) via `list_computer_folders` não retornaram
  nada (nem disponível, nem bloqueada) mesmo após o usuário confirmar que ativou nas
  configurações. Pode ser atraso de sincronização ou recurso ainda não disponível para a conta;
  não foi diagnosticado com certeza.

## Onde está o código

Branch `claude/soares-design-duplicates-utbtji` do repositório `IsmalSoares/IsmalSoares`
(github.com/IsmalSoares/IsmalSoares). Todo o histórico de commits tem mensagens descrevendo
cada mudança — ver `git log` para detalhes além deste resumo.
