---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 53a2dd005de075c0f1e4bf83675995608e5f785d
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 7%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 20936 {#20936}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 20936, lançada publicamente em terça-feira, 19 de maio de 2025. A versão de manutenção anterior era 20626.

A ativação de recursos do 2025.5.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

>[!NOTE]
>
>A versão 20783 foi tornada privada em 19 de maio e foi substituída pela versão 20936.

### Aprimoramentos {#enhancements-20936}

* FORMS-19125: o editor de Formulário adaptável dos Componentes principais é aprimorado para oferecer suporte ao mapeamento automático de fragmentos de Formulário adaptável disponíveis quando uma seção correspondente da árvore de fonte de dados é colocada na tela de formulário. Isso traz um recurso essencial de produtividade do editor de base para os componentes principais.
* FORMS-17107: o AEM Forms agora oferece análise de função personalizada aprimorada do lado do cliente. Isso inclui suporte para recursos modernos do JavaScript (ECMAScript ES10+), como encadeamento opcional, e introduz a capacidade de usar importações estáticas em scripts de função personalizados. Isso permite que os desenvolvedores organizem melhor o código, utilizem módulos ESM e removam limitações anteriores encontradas com funções personalizadas no Adaptive Forms com base nos Componentes principais e no Edge Delivery Services, especialmente para usuários que anteriormente precisavam de soluções alternativas para esses recursos.
* SITES-27775: Pesquisa de referência otimizada durante a publicação.
* SITES-30885: processamento JSON otimizado em consultas persistentes.
* SITES-25433: Edge Delivery com editor universal: suporte à renderização de página inteira ao comparar versões antigas.
* SITES-27792: Edge Delivery com Universal Editor: adicionar modelo específico para configurações de serviço do Edge Delivery
* SITES-19754: Edge Delivery com Universal Editor: mensagem de erro convincente quando a configuração é interrompida.
* SITES-30328: Edge Delivery com editor universal: visualização do suporte ao Sidekick.
* SITES-23499: Edge Delivery com Universal Editor: permite que vários campos sejam usados para opções de bloco.
* SITES-29987: Adicione a capacidade de definir `previewUrlPattern` ao criar modelos de fragmento de conteúdo.
* SITES-29874: Adicionar suporte para referências LongTextField na API do fragmento de conteúdo.
* SITES-29601: adicione validação para fragmentos de conteúdo referenciados por campos LongText.
* SITES-24623: Tornar ETags retornadas pelo GET e pela API de fragmentos do SEARCH utilizáveis para patch.
* SITES-28557: Permitir parâmetro de URL `references` no Fragmento de Conteúdo do PATCH.
* SITES-5358: [OpenAPI] Copie Fragmentos de Conteúdo com filhos.
* SITES-29614: endpoint do fluxo de trabalho do GET.
* SITES-29615: lista o ponto de extremidade da API de solicitações em lote.
* SITES-25130: Atualizar componentes principais para 2.28.0
* SITES-10575: &quot;O carregador de filtro de bloomfilter do MSM Blueprint&quot; tenta carregar >100.000 linhas.
* SITES-26711: os links para campos de texto do RTE não são atualizados para apontar para a live copy na implantação do MSM.
* SITES-25976: os links dentro dos Fragmentos de experiência não se adaptam após a implantação do MSM.

### Problemas corrigidos {#fixed-issues-20936}

* ASSETS-50994: Tráfego de entrada bloqueado em AemRequestEventFilter.
* CQ-4358591: Projetos ausentes para alguns idiomas quando cópias de idioma são criadas do painel de referência de sites com a opção &quot;Criar projetos de tradução&quot;.
* CQ-4359108: o formato XLIFF 2.0 falha ao usar Importação/Exportação de tradução humana.
* CQ-4358722: a localização não está funcionando para códigos ISO herdados devido a diferentes códigos de localidade no Java 11 e Java 17.
* FORMS-19808: ao salvar um formulário grande que inclui fragmentos ativados com carregamento lento, os rascunhos não podem ser obtidos pelo usuário.
* FORMS-19887: um campo suspenso em um formulário XFA, inicialmente definido como acesso somente leitura, falha ao alterar para um status aberto/editável quando o formulário é renderizado no HTML5. O campo permanece como readOnly e impede a interação do usuário, diferentemente da renderização do PDF, em que funciona conforme esperado.
* FORMS-19651: no Editor de regras, uma regra não funciona corretamente quando um clique em um botão é usado em uma condição binária e o mesmo botão também é usado na instrução &quot;then&quot; dessa regra.
* FORMS-19628: no Documento de registro (DoR) gerado automaticamente para o Forms adaptável baseado em Componente principal, excluir o título de um painel aninhado do DoR também oculta incorretamente o título do painel raiz se o painel raiz tiver a opção &quot;Permitir rich text para título&quot; ativada.
* FORMS-18977: os PDFs gerados pelo serviço do Documento de registro (DoR) não têm o título do documento. Isso pode levar à não conformidade com os padrões de acessibilidade do PDF/UA e da WCAG 2.1, pois o título do documento é um atributo necessário para PDFs acessíveis.
* FORMS-18526: quando uma regra que contém vários campos em suas condições é copiada de um campo para outro, uma referência de campo fixo nessas condições retém incorretamente sua referência para o campo de origem original em vez de atualizar para o novo campo onde a regra é copiada.
* FORMS-19047: Depois que um Formulário adaptável é modificado e republicado no AEM Forms (especificamente 6.5.22.0), as traduções para certos elementos de formulário, particularmente caixas de texto, podem estar ausentes.
* FORMS-19234: o recurso de linha do tempo para PDFs no AEM Forms, que permite que os usuários visualizem detalhes sobre a criação e o controle de versão de um PDF, para de funcionar depois que qualquer PDF é carregada na seção &quot;Forms e documentos&quot;.
* FORMS-18196: A API HTTP de sincronização do `generatePrintedOutput` (ou `generatePdfOutput`) retorna incorretamente um código de resposta 200 (Sucesso) em vez do código de erro 400 (Solicitação inválida) esperado quando os dados opcionais do campo exigidos pelo modelo XDP são deixados vazios na solicitação.
* FORMS-19336: No editor do formulário adaptável dos Componentes principais (editor AF2), a funcionalidade de pesquisa na árvore do Data Source não funciona corretamente ou conforme esperado, impedindo que os usuários encontrem facilmente elementos de dados específicos.
* FORMS-17707: o conector do AEP (Adobe Experience Platform) não está funcionando corretamente quando configurado para se conectar a ambientes de &quot;preparo&quot; da plataforma AEP.
* FORMS-18526: ao copiar uma regra que tem condições baseadas em vários campos, um campo referenciado nas condições ou ações da regra (que não é o campo principal que aciona a regra) não é atualizado para fazer referência correta ao novo campo para o qual a regra está sendo copiada. Em vez disso, ele continua fazendo referência ao campo de origem original de onde a regra foi copiada.
* FORMS-18474: uma regra criada para definir o foco em um painel ou componente específico quando o valor de um campo específico é alterado (por exemplo, campo &quot;A&quot;) acionado incorretamente por uma alteração em qualquer campo do formulário. Por exemplo, se o campo &quot;B&quot; for modificado, o foco ainda será definido para o painel designado, mesmo que a regra tenha sido configurada apenas para alterações no campo &quot;A&quot;.
* GRANITE-58276: os ciclos de dependência OSGi impedem que a fábrica do mecanismo de script HTL funcione corretamente.
* OAK-11673: aumento do CPU Oak-segment-azure v12 causado por refreshLease.
* SITES-30752: Não use cabeçalhos `If-modified-since`/`last-modified` ao gerar resposta de consulta persistente.
* SITES-30353: DataFetchingExceptions do GraphQL para o campo &quot;src&quot; nos fragmentos de conteúdo do AEM.
* SITES-30333: leia metadados de ativos do jcr para evitar problemas de análise de xmp.
* SITES-30140: problema de janela dupla ao criar referência de fragmento de conteúdo.
* SITES-29748: Corrija as condições de renderização para mostrar as ações de gerenciamento de publicação/publicação rápida dentro do editor do CF.
* SITES-15452: elementos únicos do CF não devem ser verificados em relação a suas cópias no lançamento.
* SITES-30386: Edge Delivery com Universal Editor: a UE cors.js duplicada faz com que a UE duplique as seções ao adicionar conteúdo.
* SITES-29745: Corrigido um problema raro em que variações de referências não eram hidratadas.
* SITES-30585: não é possível definir &quot;previewUrlPattern&quot; ao criar modelos com referências.
* SITES-30327: a publicação de fragmentos de conteúdo sem permissões cria fluxos de trabalho separados para cada recurso de carga.
* SITES-29528: ETag não pode ser usado para armazenamento em cache na instância de publicação.
* SITES-30583: ferramenta Localizar e substituir alterando todos os caracteres para minúsculas.
* SITES-31157: O patch falha devido a ETag inconsistente.
* SITES-31327: [OpenAPI] A solicitação de obtenção de fragmento de conteúdo na instância do autor pode responder com 304.
* SITES-29691: NullPointerException ao tentar mover a página.
* SITES-30728: OnTime/OffTime não publica/desfaz a publicação conforme esperado quando configurado nas propriedades do ativo.
* SITES-29789: alteração de link de componente em páginas raiz copiadas no AEM.
* SITES-29191: Não é possível adicionar mais de 20 SKUs ao componente de lista de produtos.
* SITES-30372: O Recorte inteligente não funciona no componente principal Imagem (V2) do AEM.
* SITES-28693: o componente de Teaser renderiza o HTML corrompido quando o título está vazio.
* SITES-28668: não é possível promover a inicialização com LaunchPromotionParameters.
* SITES-31005: Aprimore a interface do trabalho de implantação para mostrar ao cliente o progresso.
* SITES-31020: melhore a interface do usuário para criar trabalhos de Live Copy para mostrar ao cliente o progresso.
* SITES-29816: erro &quot;Recurso não encontrado&quot; ao criar a Live Copy do fragmento de experiência.
* SITES-29363: o botão Redefinir live copy não está funcionando para a hierarquia de conteúdo da live copy aninhada.
* SITES-31467: Erros JS de `contexthub.authoring-hook.js` no editor de páginas.
* SKYOPS-106509: Adicione sinalizadores complementares de abertura para suportar o acesso reflexivo GSON no Java 21.

### Problemas conhecidos {#known-issues-20936}

* SITES-28030: a opção Iniciar destino não aparece ao selecionar a opção de direcionamento.

### Recursos e APIs obsoletos {#deprecated-20936}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-20936}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 19 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-20936}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.78.1-T20250429061757 | [API Oak API 1.78.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.26-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
