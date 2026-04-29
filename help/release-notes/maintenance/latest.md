---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fb50ebd0aecda2cf59e5a75136884f26488b4b90
workflow-type: tm+mt
source-wordcount: '2310'
ht-degree: 4%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 25520 {#25520}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 25520, lançada publicamente em 23 de abril de 2026. A versão de manutenção anterior era 25194.

A ativação de recursos do 2026.4.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.


### Aprimoramentos {#enhancements-25520}

* FORMS-24388: adição de um ambiente de desenvolvimento local para o Editor de comunicação interativa (IC) que permite aos desenvolvedores criar e testar configurações sem depender de servidores compartilhados. Esse aprimoramento ajuda os clientes corporativos a interagir mais rapidamente, reduzir as dependências do ambiente e melhorar a produtividade geral do desenvolvimento.
* FORMS-24014: Aprimoramento do Editor de regras para componentes de anexo de arquivo para suportar a combinação de condições usando a lógica &quot;AND&quot;; por exemplo, permitindo regras como &quot;Se o anexo de arquivo for alterado e o painel for válido, faça isso&quot;. Anteriormente, não era possível usar condições adicionais com anexos de arquivo; essa atualização permite definições de regras mais complexas para dar suporte a workflows avançados.
* FORMS-23571: aprimoramento da visualização simplificada de gramática existente para regras de evento de acionador adicionando suporte para eventos prontos para uso (OOTB), além de eventos personalizados. Anteriormente, os usuários só podiam usar a gramática simplificada para eventos personalizados e tinham que alternar entre as regras &quot;QUANDO&quot; e &quot;EVENTO ACIONADO&quot; para configurar eventos OOTB e personalizados separadamente. Com essa atualização, tanto a OOTB quanto os eventos personalizados podem ser usados na mesma gramática simplificada, simplificando a configuração de regras e reduzindo a necessidade de alternar contextos.
* FORMS-24462: Adição de suporte para o componente Assinatura escritas em componentes do React Vanilla para Headless Adaptive Forms (AF). Esse aprimoramento permite que os usuários capturem assinaturas manuscritas diretamente em formulários do React, dando suporte a fluxos de trabalho de assinatura digital e cronogramas de publicação planejados para clientes corporativos.
* FORMS-24343: Adição de tratamento otimizado para `custom:setProperty` no modelo de formulário JSON (JavaScript Object Notation), permitindo um processamento mais rápido de atualizações de propriedade dinâmicas. Esse aprimoramento melhora o desempenho para aplicativos complexos de Forms adaptável (AF) que dependem de alterações frequentes no tempo de execução, resultando em interações mais suaves do usuário e em tempos de carga reduzidos.
* FORMS-24358: adição de suporte para o uso da propriedade `items` na estrutura do modelo JSON (JavaScript Object Notation) em vez de `:items` e `:itemsOrder`. Esse aprimoramento permite que os desenvolvedores trabalhem com um modelo de dados mais limpo e intuitivo, que se alinha melhor às convenções JSON comuns e simplifica a integração com sistemas externos.
* FORMS-24087: adição de suporte para definição de regras e eventos diretamente em contêineres de fragmento no Adaptive Forms (AF). Esse aprimoramento permite que os autores apliquem lógica condicional e interações no nível do contêiner, melhorando a reutilização e reduzindo a necessidade de duplicar regras em campos de fragmento individuais.
* FORMS-24440: adição de uma nova ação &quot;Remover campo&quot; na lista suspensa THEN do Editor de regras para o editor de Comunicação interativa que permite que os usuários removam completamente um componente selecionado do formulário quando uma condição de regra é atendida. Este aprimoramento dá suporte a fluxos de trabalho que exigem formulários de reestruturação dinâmica em vez de apenas ocultar campos, enquanto ainda acionam o script `forms_ready` apropriado para comportamento consistente.
* FORMS-23898: adição de suporte para definição de variáveis usando a notação `@` no Editor de IC (Comunicação interativa), permitindo que os usuários configurem tabelas dinâmicas de forma mais intuitiva. Esse aprimoramento simplifica a configuração do conteúdo de tabela orientado por variáveis e melhora a clareza ao gerenciar dados dinâmicos na experiência de criação.
* FORMS-23702: adição da autenticação baseada em certificado para conexões da Lista do SharePoint (SPList) que permite acesso mais seguro e orientado por certificado aos dados do SharePoint. Esse aprimoramento ajuda os clientes empresariais a atender a requisitos mais rigorosos de segurança e conformidade, reduzindo a dependência da autenticação baseada em senha.
* FORMS-23800: adição de suporte para substituição de chaves secretas reCAPTCHA em configurações sling, permitindo que os clientes corporativos se alinhem a seus próprios requisitos de segurança e conformidade. Esse aprimoramento permite o gerenciamento de chaves secretas específicas do ambiente para que os administradores possam integrar com segurança o reCAPTCHA sem alterações de código.
* SITES-39116: o endpoint do GET do fragmento de conteúdo agora inclui informações de esquema de metadados.
* SITES-41449: novo endpoint dedicado do GET para recuperar metadados do fragmento de conteúdo.
* SITES-39434: os fragmentos e as pastas de conteúdo agora podem ser vinculados a esquemas de metadados para gerenciamento de metadados estruturados.
* SITES-39567: os metadados do fragmento de conteúdo agora são validados e armazenados de acordo com o esquema de metadados vinculado.
* SITES-40006: os fragmentos de conteúdo agora podem ser pesquisados e filtrados usando valores de campo de metadados.
* SITES-41391: a API de recuperação de um único fragmento de conteúdo agora inclui informações de status de check-in/check-out
* SITES-42214: Melhoria na confiabilidade e no desempenho das operações de movimentação de fragmentos de conteúdo
* SITES-41351: aprimoramento do formato de exibição de metadados nos fragmentos de conteúdo para melhorar a legibilidade.
* SITES-42458: Os metadados padrão agora podem ser adicionados sem validação de esquema estrita para maior flexibilidade.
* SITES-35508: Edge Delivery com Universal Editor: adicionar suporte para imagens no RTE.
* SITES-37078: Edge Delivery com Universal Editor: remova as instrumentações do Universal Editor quando as páginas forem somente leitura.
* SITES-40206: Edge Delivery com Universal Editor: adicionar validação de nome ao assistente de criação de página.
* SITES-40255: Edge Delivery com Universal Editor: impede a publicação de planilhas como `/config.json`.
* SITES-40757: Edge Delivery com Universal Editor: garantir a exclusividade das configurações do Edge Delivery no assistente de criação de sites.
* SITES-41134: Edge Delivery com Universal Editor: falha ao publicar a configuração baseada em arquivo.

### Problemas corrigidos {#fixed-issues-25520}

* FORMS-24811: os usuários tiveram problemas ao gerenciar regras de lógica de formulário. Ao tentar modificar regras criadas anteriormente, o editor de regras não permitia alterações, forçando os usuários a recriar regras do zero e atrasando a manutenção do formulário.
* FORMS-24720: os usuários tiveram problemas ao configurar variáveis recém-criadas no Adaptive Forms (AF). Ao adicionar regras a variáveis vinculadas ou não vinculadas a dados, as regras não eram salvas conforme esperado, forçando os usuários a recriar sua lógica e retardando os fluxos de trabalho de criação de formulários.
* FORMS-24195: os usuários experimentaram um comportamento inconsistente ao redefinir campos suspensos no Adaptive Forms (AF). Quando uma lista suspensa tinha um espaço reservado configurado e o formulário ou componente era redefinido, o campo ficava em branco em vez de retornar ao valor do espaço reservado, causando confusão sobre as seleções necessárias.
* FORMS-24718: os usuários tiveram problemas de navegação no editor de Comunicação interativa (IC) ao selecionar o botão Página inicial. Em vez de retornar à interface principal do Adobe Experience Manager (AEM), o botão não redirecionava como esperado, interrompendo o fluxo de trabalho dos usuários ao alternar entre a edição do IC e a tela inicial do AEM.
* FORMS-24810: os usuários tiveram falhas intermitentes ao carregar a Interface do usuário adaptável (AUI) para formulários na primeira tentativa. Em algumas sessões, a página inicial não era renderizada corretamente, forçando os usuários a atualizar ou tentar novamente antes de começarem a preencher os formulários.
* FORMS-24520: os usuários experimentaram números de página ausentes na visualização de impressão da interface do usuário do agente (UI) para formulários usando a Interface do usuário adaptável (AUI). Quando os agentes abriam a pré-visualização de impressão, o campo de número de página às vezes parecia vazio, dificultando a referência a páginas específicas ao revisar ou compartilhar cópias impressas.
* FORMS-24532: Os usuários tiveram falhas ao usar o preenchimento do modelo de dados de formulário (FDM) com as configurações de lista do SharePoint `/teams`. Organizações governamentais que dependiam dessas listas viram os formulários serem carregados sem os dados pré-preenchidos esperados, interrompendo os fluxos de trabalho de coleta de dados e aumentando o esforço de entrada manual.
* FORMS-24516: faltam dados de assinatura de rabisco nos usuários do Documento de registro (DoR) após uma atualização do SDK no AEM Forms as a Cloud Service. Quando os formulários eram assinados usando a opção de rabisco, o DoR gerado não exibia a assinatura capturada, causando confusão e registros incompletos para clientes corporativos.
* FORMS-18631: Os usuários tiveram problemas de acessibilidade com layouts de grade no desktop, tablet com web design responsivo (RWD) e visualizações móveis RWD. Ao usar o Chrome no Windows 11 com o leitor de tela NVDA (NonVisual Desktop Access), as grades não tinham as funções e os atributos apropriados, dificultando a interpretação e a navegação corretas do conteúdo pelas tecnologias assistivas.
* FORMS-24798: os usuários experimentaram um comportamento inconsistente ao usar condições do `else` nas regras do Adaptive Forms (AF) na Interface do Usuário (UI) do AEM Forms. Quando a condição de regra primária não foi atendida, as ações `else` associadas não foram executadas, fazendo com que a lógica do formulário e a visibilidade do campo se comportassem de forma diferente da configurada pelos autores.
* FORMS-24334: os usuários tiveram falhas de preenchimento prévio e problemas de mesclagem da Notação de objeto do JavaScript (JSON) ao trabalhar com um Formulário adaptável (AF) incorporado no Adobe Experience Manager (AEM) Forms as a Cloud Service. Ao carregar formulários migrados, os dados pré-preenchidos esperados não eram exibidos e o conteúdo JSON mesclado estava incompleto ou incorreto. Isso bloqueou a migração do AEM 6.5 no local para o AEM Forms as a Cloud Service em ambientes afetados.
* FORMS-24441: os usuários tiveram problemas com a configuração do modelo do Documento de registro (DoR) no Adobe Experience Manager (AEM) Forms as a Cloud Service. Quando salvavam um modelo DoR personalizado no ambiente de desenvolvimento rápido, o modelo revertia para a versão padrão, impedindo-os de manter o layout e as configurações desejados.
* FORMS-24393: Os usuários sentiram confusão quando modelos mais antigos continuaram a aparecer como &quot;Sem título&quot; em vez de mostrar nomes significativos. Isso dificultava a distinção e a reutilização de modelos existentes durante o trabalho diário de criação.
* FORMS-24163: os usuários tiveram problemas ao visualizar formulários da Versão 2 que continham fragmentos. No modo de visualização, o conteúdo do formulário não era renderizado conforme esperado, impedindo que os usuários validassem o layout e o comportamento antes da publicação.
* FORMS-24328: Os usuários experienciaram envios de formulários não concluídos ao usar o reCAPTCHA v2 invisível com a opção &quot;Validar CAPTCHA em uma ação do usuário&quot;. Os clientes corporativos viram que os formulários em ambientes afetados não eram enviados conforme esperado, interrompendo o contato e os fluxos de trabalho de solicitação de proposta.
* SITES-42118: Ignorar regras de substituição para `/graphql/execute.json`.
* SITES-40095: corrija a lista de referência local no editor de metadados.
* SITES-42191: Corrigir o GraphQL JSON omite referências de imagem incorporadas quando os nomes de arquivo do DAM contêm espaços/caracteres não ASCII.
* SITES-22336: cadeia de caracteres &quot;Modelos de fragmento de conteúdo&quot; não localizada em Assets > Criar > Fragmento de conteúdo.
* SITES-19796: a sequência de caracteres não localizada &quot;Nome inválido fornecido&quot; é exibida ao adicionar um caractere inválido ao criar o fragmento de conteúdo no Assets.
* SITES-42531: a dica de ferramenta é deslocalizada ao bloquear &quot;Fragmento de conteúdo&quot; na página &quot;Assets&quot;.
* SITES-42532: sequência de caracteres &quot;Posteriormente&quot; deslocalizada na publicação do CF no AEM no Assets.
* SITES-39250: os caracteres localizados são exibidos incorretamente no link em Assets > Editor de fragmentos de conteúdo.
* SITES-41117: cadeia de caracteres &quot;O valor selecionado precisa ser um Tipo de Modelo válido dentro de `{}` ou um modelo global&quot; deslocalizada no Editor de Modelos de Fragmentos de Conteúdo.
* SITES-41431: verbosidade reduzida do feedback do leitor de tela para o botão de bloqueio para fornecer anúncios mais claros e concisos.
* SITES-40819: o foco do teclado foi corrigido para não retornar ao elemento de acionamento após uma interação, garantindo uma ordem de foco previsível.
* SITES-40751: adição de rótulos visíveis no foco do teclado para itens da barra de ferramentas para que os usuários de teclado possam identificar claramente as ações.
* SITES-25524: correção do uso de aria-pressionado em botões de dispositivo para que as tecnologias assistivas recebessem informações de estado precisas.
* SITES-25321: cores de texto atualizadas para atender aos requisitos mínimos de contraste e melhorar a legibilidade para usuários com pouca visão.
* SITES-25304: impedia que a barra de ferramentas demográfica recolhida recebesse o foco incorretamente, mantendo uma sequência de foco lógica.
* SITES-25292: esclarecimentos sobre os anúncios do leitor de tela para o botão de rotação do dispositivo descreverem melhor sua finalidade e estado.
* SITES-25290: adição de um estado de pressionamento visível para o botão de alternância da área de trabalho para tornar seu status de seleção óbvio para os usuários.
* SITES-25287: contexto de medição de régua aprimorado ao editar o layout, fornecendo aos usuários de leitores de tela informações de medição compreensíveis.
* SITES-25284: corrigido o truncamento do rótulo do botão &quot;iPhone 8 Plus&quot; no estado desmarcado para que o nome completo do dispositivo seja anunciado e visível.
* SITES-25251: Feedback apresentado para usuários de leitores de tela quando a lista &quot;Inserir novo componente&quot; é filtrada, indicando que os resultados foram alterados.
* SITES-25221: Aumento do tamanho do destino de toque do botão Editar no painel lateral do ativo para atender às diretrizes de tamanho mínimo do destino.
* SITES-25220: adição de aviso/indicação de que o botão Editar no painel esquerdo do Assets abre uma nova guia, melhorando a previsibilidade para usuários de tecnologia assistiva.
* SITES-24993: atualização do título do cabeçalho da Tela do editor para usar uma função de cabeçalho apropriada, melhorando a estrutura do documento para leitores de tela.
* SITES-24954: correção da ordem de foco do botão do emulador para que ele seguisse uma sequência de navegação natural e lógica.
* SITES-41586: correção para copiar e colar o componente de Fragmento de conteúdo no editor perdendo uma referência ao fragmento de conteúdo.
* SITES-42195: correção `CommerceLinksTransformerFactory` que não respeita os mapeamentos sling na instância de publicação.
* SITES-41238: correção de um erro no ThumbnailServlet que causava a inundação de log.
* SITES-41041: Corrigir componentes do CIF não renderizados na Pré-visualização/Comparação de versão.
* SITES-40756: Corrigir formato de data não localizado em Visão geral da Live Copy > Status do relacionamento.
* SITES-40219: correção do CatalogPageNotFoundFilter que não é chamado para páginas de produto ou categoria específicas.
* SITES-40218: Corrigir SpecificPageFilterFactory sem registro de tipo de recurso de página v3.
* SITES-40347: quebra a herança do título ao criar uma live copy com um novo conjunto de títulos.
* SITES-41544: os cálculos de ETag do fragmento de conteúdo agora excluem metadados.
* SITES-42734: corrigido o problema em que o endpoint de metadados do GET retornava campos vazios ao usar o esquema padrão.
* SITES-37955: Edge Delivery com Universal Editor: verifique se os pré-requisitos de publicação estão verificados de forma consistente.
* SITES-40877: Edge Delivery com Universal Editor: corrija falhas de publicação de páginas que contêm caracteres especiais não ascii.
* SITES-42092: Edge Delivery com Universal Editor: corrija o cancelamento de publicação profundo para caminhos que terminam em `-s`.
* SITES-24650: o iframe não tem um título.

### Problemas conhecidos {#known-issues-25520}

* SITES-43715: Edge Delivery com Universal Editor: a falha na validação de permissão adiciona latência às cargas de trabalho de publicação.

### Recursos e APIs obsoletos {#deprecated-25520}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-25520}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 24 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-25520}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.90.0 | [API do Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
