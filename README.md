# Escritório Virtual de Marketing — Salário-Maternidade

Escritório 3D no navegador, com uma sala única onde ficam o gerente, a secretária e a equipe de marketing (pesquisa, copy, criativo, análise e social media). Você anda pela sala com as setas, conversa com os personagens e acompanha o trabalho numa Central de Tarefas ligada a uma Estante de arquivos.

Tudo o que aparece como concluído foi registrado de verdade no sistema. Não há tarefas, arquivos nem números de exemplo.

## Tecnologias

- HTML, CSS e JavaScript puros, sem etapa de compilação
- [Three.js r128](https://threejs.org/) carregado por CDN (cdnjs) para a sala 3D
- Google Fonts (Bricolage Grotesque, Figtree, JetBrains Mono), também por CDN
- IndexedDB do navegador para guardar tarefas, notificações e arquivos

## Estrutura

```
escritorio-marketing/
├── index.html      estrutura da página
├── css/style.css   visual (painéis, menus, estante, responsivo)
├── js/app.js       sala 3D, personagens, Central de Tarefas, Estante, Secretária
├── .nojekyll       faz o GitHub Pages servir os arquivos como estão
└── README.md
```

## Como executar localmente

1. Baixe ou clone o repositório.
2. Dê dois cliques em `index.html`. A página abre no navegador (Chrome, Edge ou Firefox).

É preciso estar conectado à internet, porque o Three.js e as fontes vêm por CDN.

Se preferir um servidor local, rode dentro da pasta `python -m http.server 8000` e abra `http://localhost:8000`.

## Como publicar no GitHub Pages

1. Envie os arquivos para a raiz do repositório `escritorio-marketing`, com `index.html` no nível principal.
2. No GitHub, abra **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**, depois a branch `main`, a pasta `/ (root)`, e clique em **Save**.
4. Em alguns minutos o site fica disponível em `https://SEU-USUARIO.github.io/escritorio-marketing/`.

Todos os caminhos são relativos (`./css/…`, `./js/…`). O projeto funciona no GitHub Pages sem nenhum servidor.

## Funcionalidades atuais

- **Sala 3D**: piso, paredes, janelas, relógio com a hora real, plantas, estantes, sofá e mesas com computadores.
- **Seu personagem**:
  - As setas movem o personagem (WASD também funciona), com animação de caminhada.
  - A câmera o acompanha. A tecla `C` alterna para a visão geral, e a roda do mouse dá zoom.
  - No celular aparece um direcional na tela.
- **Equipe**: gerente (Marcos), secretária (Helena), pesquisadora (Lívia), copywriter (Rafael), criativa (Bia), analista (Otávio) e social media (Carol). Cada um tem mesa e aparência próprias.
  - A animação de trabalho de cada um só aparece quando existe uma etapa real em andamento com aquela pessoa.
- **Interação**: chegue perto de um personagem e aperte `E`, ou clique nele.
  - Cada ficha mostra o que a pessoa está fazendo, o que está aguardando e o que ela já concluiu.
- **Central de Tarefas**:
  - Cada tarefa tem título, descrição, fluxo de etapas com responsáveis, data prevista e observações.
  - Os status possíveis são Não iniciada, Aguardando, Em andamento, Em revisão, Concluída, Problema e Pausada.
  - Há filtros por status, pelo responsável e pela opção "Minhas tarefas".
  - Cada tarefa guarda o histórico com data e hora, o progresso e a opção "Devolver para ajustes" na revisão.
- **Estante / Arquivo**:
  - Os arquivos ficam em gavetas por período: Hoje, Ontem, Esta semana, Semana passada, Este mês, Mês passado, Meses anteriores, Este ano, Ano passado e Todos.
  - Também ficam em pastas por tipo: Vídeos, Imagens, Textos, Anúncios, Posts, Roteiros, Documentos, Relatórios e Outros.
  - Todo arquivo fica ligado a uma tarefa. Você pode enviar um arquivo ou escrever um texto, que vira um `.txt`, e depois abrir, baixar e excluir.
- **Secretária Helena**: responde perguntas consultando os dados registrados, sem inventar.
  - Exemplos: "Como está a campanha?", "Quem está trabalhando?", "Quais arquivos foram produzidos hoje?".
  - Quando não há registro, ela diz isso.
- **Notificações**: só aparecem quando uma etapa ou tarefa é concluída, ou quando um arquivo é guardado.
- **Relatórios**: números calculados a partir dos dados.
  - Mostra tarefas por status, etapas concluídas por pessoa, tempo médio por etapa e arquivos por tipo e período.
  - Tem download de um relatório geral em `.txt` e a opção de guardar o relatório de uma tarefa na Estante.

## Limitações atuais

- **Sem IA nos funcionários:** cada etapa avança quando você clica em Iniciar ou Concluir.
- **Dados só no seu navegador (IndexedDB):**
  - Não aparecem em outro computador ou celular, nem para outras pessoas.
  - Limpar os dados do navegador apaga as tarefas e os arquivos.
- **Dados do Claude não vêm juntos:** as tarefas criadas na versão publicada dentro do Claude ficam lá. Esta cópia começa vazia.
- **Relatório de resultados com etapas fora de ordem:** no tipo de tarefa "Relatório de resultados", a Revisão aparece antes da Análise.
- **Sem integrações:** Meta Ads, Instagram, Facebook, TikTok e ferramentas de IA não estão conectados. Por isso não há números de anúncios.
- **Precisa de internet:** o Three.js e as fontes são carregados por CDN.

## Observação técnica

O arquivo `js/app.js` guarda os dados por meio de um objeto `Store`. Quando a página roda dentro do Claude, ele usa o armazenamento do Claude. Em qualquer outro lugar, como o GitHub Pages ou o computador local, ele usa o IndexedDB automaticamente, sem nenhuma configuração.

As ações do escritório (criar tarefa, iniciar e concluir etapa, guardar arquivo) também ficam disponíveis em `window.EscritorioVirtual` para futuras integrações.
