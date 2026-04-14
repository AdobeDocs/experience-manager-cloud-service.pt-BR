---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d2c26a122bd2a0a970af7578932d88e6f93487d5
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 6%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 25194 {#25194}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 25194, lançada publicamente em quinta-feira, 1 de abril de 2026. A versão de manutenção anterior era 24678.

A ativação de recursos do 2026.4.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

>[!NOTE]
>
>A versão 24893 foi tornada privada.

### Aprimoramentos {#enhancements-25194}

* ASSETS-65127: Metadados personalizados do evento: tratamento aprimorado de nomes de metadados.
* ASSETS-63313: crie links relacionados automaticamente para ativos e pais exportados com base em manifestos C2PA.
* ASSETS-10995: limite o número de ativos em um zip de download.
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

### Problemas corrigidos {#fixed-issues-25194}

* ASSETS-62882: Visualização do administrador: a dica de ferramenta info é interrompida quando vários nomes de arquivo inválidos são carregados.
* ASSETS-63642: O link de compartilhamento falha ao renderizar o ativo em alguns ambientes de desenvolvimento (SLA3).
* ASSETS-59267: NPE ao carregar metadados de aplicativo para carga do delivery.
* ASSETS-59227: Exportação de metadados: as propriedades não selecionadas não são mais incluídas devido à correspondência de regex.
* ASSETS-65187: visualização de CSV na nuvem quando os dados da coluna contêm vírgulas de escape.
* ASSETS-63441: Verifique se todos os usuários têm permissão para ler a configuração do Assets Omnisearch.
* SITES-40095: Editor de metadados: o fragmento de conteúdo local faz referência a mais de 10 entradas.
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

#### Guias do AEM {#guides-25194}

* GUIDES-38412 : Ao editar um arquivo do Schematron `(*.sch)` e usar o recurso localizar e substituir, o painel localizar e substituir aparece parcialmente fora da tela na parte inferior, impedindo o acesso aos campos e controles de entrada.
* GUIDES-37806: Quando o mesmo tópico é reutilizado em vários mapas com diferentes predefinições condicionais, a publicação do mapa mais recente no Salesforce substitui o conteúdo do tópico, resultando na exibição de dados incorretos para os usuários de mapas publicados anteriormente.
* GUIDES-39394: Quando uma imagem gerenciada inicialmente como um ativo específico de idioma com uma versão específica (por exemplo, em `/en/`) é movida para uma pasta global com uma versão atualizada e a exportação da linha de base é executada, a nova linha de base continua a fazer referência a versões desatualizadas específicas do idioma dessa imagem, resultando em uma falha na exportação da linha de base.
* GUIDES-39054: Ao criar uma linha de base dinâmica, o Editor às vezes fica sem responder devido a várias solicitações de API simultâneas, fazendo com que todas as outras operações travem.
* GUIDES-37781: Ao atribuir um usuário a uma tarefa de revisão, a lista suspensa lista todos os usuários em vez de apenas aqueles associados aos projetos selecionados, resultando em opções de usuário inválidas.
* GUIDES-39385: Ao abrir um Relatório para um mapa, há um atraso no carregamento do painel Filtros.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-25194}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-25194}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-25194}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 9 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-25194}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.90.0 | [API do Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
