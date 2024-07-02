---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 90b4cf269fc8be36d90f398d1696fc40f89f5142
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 17%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 16799 {#release-16799}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 16799, lançada para o público em quarta-feira, 18 de junho de 2024. A versão de manutenção anterior era a versão 16544.

A Ativação de recursos 2024.6.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-16799}

* ASSETS-31977: operações aprimoradas de movimentação, cópia e exclusão de ativos.
* ASSETS-33618: recurso de transcrição automática e tradução para vídeos no Dynamic Media.
* ASSETS-35185: ação de aprovação para ContentHub e DM e adição de propriedades às propriedades damAssetLucene.
* ASSETS-35533: Adicionar propriedades DRM e CAI ao índice damAssetLucene.
* ASSETS-37280: manuseio de trabalho sequencial para tradução quando o subtítulo de origem (vtt) ainda está sendo processado.
* ASSETS-37559: evento de exclusão de ativo aprimorado.
* ASSETS-37723: Implementar o evento publicado de ativo.
* ASSETS-37724: Implementar o evento de ativo não publicado.
* ASSETS-38614: Compartilhar aprimoramentos da interface do usuário do link.
* ASSETS-39601: Aplicar regex de validação automaticamente ao nome da Live Copy do ativo.
* ASSETS-39454: atualização para visualizadores 2024.5.0 no Quickstart.
* CNTBF-184: Suporte a caminhos abaixo `/conf` em Fluxo de retorno de conteúdo.

### Problemas corrigidos {#fixed-issues-16799}

* ASSETS-37335: Editar O Painel De Pesquisa No Filtro Desmarca Todas As Caixas.
* ASSETS-38069: Problema de visualização do PDF AEM DAM na seleção de filtro da linha do tempo.
* ASSETS-38215: o botão de licença do Adobe Stock está esmaecido na assinatura do AEM as a Cloud Service para corporações.
* ASSETS-38578: Hiperlinks incorretos no relatório Compartilhamento de links do Assets.
* ASSETS-38678: as configurações de exibição estão quebradas em Detalhes da coleção.
* ASSETS-39071: a entrega otimizada para a Web pode gerar uma exceção se o mimetype da representação original for nulo.
* ASSETS-39316: a classificação por nome não funciona em Coleções.
* ASSETS-39377: a importação em massa do OneDrive pode falhar ao receber pressão de retorno da API remota.
* ASSETS-39428: Problemas de renderização na interface do usuário do Gerenciamento de direitos autorais.
* CQ-4357150: Guava no pacote cq-content-sync.
* GRANITE-52573: solicitações que contêm uma barra dupla `//` são rejeitados com o código de status 400.
* SCRNS-4194: Remova a dependência das APIs do Google Guava.
* SCRNS-4360: Botão Gerenciar publicação e Publish rápido ausente para usuários não administradores no Provedor de conteúdo para canais.
* SCRNS-4323: Ocultar/desativar inicializações de screens.html.

#### Forms

* FORMS-14844: o Adaptive Forms permite o envio de formulários apesar da falha na verificação do reCAPTCHA.
* FORMS-14984: O Forms com CAPTCHA ignora a validação se &quot;submitMetaData&quot; estiver ausente nos dados enviados.
* FORMS-14477: As opções &quot;Is After&quot; e &quot;Is Before&quot; no editor de regras funcionam incorretamente na validação do Seletor de datas.
* FORMS-14019: A funcionalidade &quot;Chamar serviço&quot; do editor de regras não está funcionando no Editor universal.
* FORMS-14336: quando nenhum campo de formulário é selecionado, o editor deve ser aberto com foco no elemento de formulário inteiro.
* FORMS-15061: O círculo do carregador persiste indefinidamente ao usar a opção de invocar serviço no editor de regras.

### Problemas conhecidos {#known-issues-16799}

>[!NOTE]
> A engenharia de AEM identificou uma regressão na funcionalidade Lançamentos que está afetando as versões atuais do AEM a partir de 16461. Devido a essa regressão, novas Inicializações (criadas após a aplicação de novas versões) que incluem páginas não profundas não serão promovidas corretamente devido a configurações ausentes.
> Caso seus ambientes sejam afetados, um script de shell para identificar e atualizar configurações ausentes estará disponível por meio do suporte ao cliente (referência interna SITES-22457).
> Uma correção de longo prazo será disponibilizada e garantirá que novos lançamentos sejam criados com todas as configurações certas. Até lá, uma versão de patch interna também estará disponível sob demanda.

#### Forms

1. Se um usuário baixar a versão do SDK do AEM Forms superior a `AEM Forms add-on v2024.05.04.00-240400`, o arquivo em lote falha ao iniciar o serviço Docker. Para resolver esse problema:
   1. Baixe o [pasta](/help/forms/assets/sdk_hotfix.zip).
   1. Extraia o conteúdo da pasta baixada e copie o `sdk.sh` e `sdk.bat` arquivos.
   1. Substituir o existente `sdk.sh` e `sdk.bat` no SDK do AEM Forms com os novos arquivos.

### Aviso de mudança {#change-notice-16799}

* Esta versão inclui as seguintes novas versões do índice de produtos:
   * **damAssetLucene-11**
   * **fragmentos-11**

  As versões personalizadas das versões de índice anteriores serão mescladas automaticamente com a nova versão do índice do produto. Aplique mais atualizações personalizadas à versão mesclada.

* A partir de setembro de 2024, a AEM as a Cloud Service desativará a serialização de Resource Resolvers por meio da estrutura do Exportador de modelo do Sling. Consulte [a documentação](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obter mais detalhes.

### Recursos e APIs obsoletos {#deprecated-16799}

Para saber o que está obsoleto ou foi removido no AEM as a Cloud Service, consulte [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-16799}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak API 1.64.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.22-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.25.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
