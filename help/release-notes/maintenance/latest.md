---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 13%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 16971 {#release-16971}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 16971, lançada publicamente em quinta-feira, 3 de julho de 2024. A versão de manutenção anterior era a versão 16799.

A Ativação de recursos 2024.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-16971}

* SITES-22948: Remova as referências comerciais no conteúdo básico para AEM CS.
* SITES-22141: [Fragmentos de conteúdo] SegmentNotFoundException de CFM ModelChangeRepositoryImpl após OnRC.
* SITES-21893: problema de corte de imagem na instância do autor.
* SITES-21788: [Fragmentos de conteúdo] Exibir OBSERVAÇÃO no CF e no editor de modelos CF quando uiSchema estiver habilitado para o modelo.
* SITES-21688: a implantação do MSM não atualiza o caminho do fragmento de experiência (XF) nas páginas de live copy.
* SITES-21659: Retorna o nome completo do usuário que está criando/modificando/replicando um recurso de Modelo.
* SITES-21609: endpoint OpenAPI para migrar fragmentos de conteúdo de um modelo para outro.
* SITES-21598: [API aberta] Criar CFM: retorna um erro se o Caminho de configuração fornecido não existir.
* SITES-21491: [API aberta] O ponto de extremidade de PATCH CF deve respeitar as relações de vida no nível do campo.
* SITES-21434: [API aberta] O ponto de acesso do CF GET deve respeitar as relações de vida no nível do campo.
* SITES-21415: Editor de CF - suporte a referências UUID.
* SITES-21326: [API aberta] Forneça informações sobre a presença de referências para um Fragmento de conteúdo.
* SITES-21310: [API aberta] Adicionar id do fragmento de conteúdo na resposta da API de traduções.
* SITES-20859: API aberta do CF - Retorna referências ao recuperar um fragmento por caminho.
* SITES-20687: [API aberta] Endpoint para recuperação de status de processamento em lote.
* SITES-20657: [API aberta] Fornece a opção para a palavra inteira do match ao substituir uma string usando `FindAndReplace` terminal.
* SITES-20587: [API aberta] Criar `COPY` endpoint para fragmentos de conteúdo.
* SITES-20584: [API aberta] Otimizar recuperação de referência.
* SITES-20308: [API aberta] Ative o processamento em lote na API.
* SITES-19976: [API aberta] Esquema de interface do usuário genérico para campos condicionais.
* SITES-19556: [Fragmentos de conteúdo] Atualize o uiSchema, se ele existir, quando o modelo for editado.
* SITES-18056: [API aberta] Ao publicar um fragmento de conteúdo para Visualização, inclua referências.
* SITES-16898: [Esquema] Endpoint OpenAPI para migrar fragmentos de conteúdo de um modelo para outro.
* SITES-16609: ponto de extremidade de inicializações de lista.
* SITES-16606: Criar endpoint de inicialização.
* SITES-21617: [Xwalk] Torne as propriedades/metadados da página editáveis dentro do UE.
* SITES-19614: [Xwalk] Paginação e rolagem infinita do editor de planilhas.
* SITES-22163: [Xwalk] Aprimoramento do suporte ao conteúdo veiculado no nível de publicação para o Edge Delivery Sites.
* SITES-22109: [Xwalk] Manuseio aprimorado de pós-processamento de marcação richtext.
* SITES-22035: [Xwalk] Manuseio de MSM e inicializações aprimorado.
* SITES-21839: [Xwalk] Melhoria no mapeamento de caminhos e na limpeza para conteúdo não distribuído pelo Edge Delivery.

### Problemas corrigidos {#fixed-issues-16971}

* CQ-4356898: [Tradução] Erro outOfMemory para CF que contém um número de links excepcionalmente grande.
* CQ-4357055: [Tradução] A tradução automática não funciona usando a API Rest.
* CQ-4353931: [Tradução] Adicione jcr:uuid na página/xf/asset de origem da tradução quando estiver ausente.
* CQ-4357591: [Tradução] Modifique o workflow &quot;Associate JCR:UUID&quot; para funcionar para Páginas/XF.
* FORMS-14844: o Adaptive Forms permite o envio de formulários apesar da falha na verificação do reCAPTCHA.
* FORMS-14984: O Forms com CAPTCHA ignora a validação se &quot;submitMetaData&quot; estiver ausente nos dados enviados.
* FORMS-14477: As opções &quot;Is After&quot; e &quot;Is Before&quot; no editor de regras funcionam incorretamente na validação do Seletor de datas.
* FORMS-14019: A funcionalidade &quot;Chamar serviço&quot; do editor de regras não está funcionando no Editor universal.
* FORMS-14336: quando nenhum campo de formulário é selecionado, o editor deve abrir com foco no elemento de formulário inteiro.
* FORMS-15061: O círculo do carregador persiste indefinidamente ao usar a opção de invocar serviço no editor de regras.
* SITES-22457: Promover um lançamento que não seja profundo não atualiza o conteúdo original.
* SITES-22748: [Fragmentos de conteúdo] Aprimorar o tratamento de erros para o trabalho de atualização do fragmento de conteúdo
* SITES-22349: [Fragmentos de conteúdo] ContentType para elementos cf vazios de várias linhas não pode ser alterado.
* SITES-22343: [Fragmentos de conteúdo] O tipo semântico &quot;enumeração&quot; foi interrompido.
* SITES-22194: depois de definir o redirecionamento, model.json não funciona mais.
* SITES-21953: [API aberta] O Etag é alterado com base na ordem do validationStatus.
* SITES-21894: [API aberta] Aprimorar a validação do caminho principal ao criar CFs.
* SITES-21887: [API aberta] ETag inválido retornado pelo ponto de extremidade de variações de POST.
* SITES-21657: [API aberta] Melhore a validação na propriedade Caminho de pesquisa do CF.
* SITES-21949: O cursor inválido das APIs de pesquisa retorna 500.
* SITES-20927: as APIs de pesquisa retornam 500 quando a consulta está ausente.
* SITES-20544: [API aberta] Altere a geração de nomes de pacote de publicação para evitar conflitos com o oak.
* SITES-19710: CVE-2022-47937 - Remova todos os usos de org.apache.sling.commons.json do Editor de páginas.
* SITES-11992: [Acessibilidade] O botão seletor de amostra de anotação não tem um nome acessível.
* SITES-10979: [Acessibilidade] O rótulo não é persistente.
* SITES-10962: [Acessibilidade] Botão: o botão não tem uma função.
* SITES-10905: [Acessibilidade] O estado do componente ativo não tem uma relação de contraste de 3 para 1.
* SITES-2974:  [Acessibilidade] - Rolagem horizontal com largura de 320 px.
* SITES-22026: Não é possível mover fragmentos de experiência entre pastas no AEM
* SITES-22106: problema de funcionalidade de alternância de idioma no novo editor de fragmento de conteúdo
* SITES-21980: tratamento inconsistente para tipos de referência baseados em UUID.
* SITES-7257: NPE em ThumbnailServlet.

### Problemas conhecidos {#known-issues-16971}

Nenhum.

### Aviso de mudança {#change-notice-16971}

* A partir de setembro de 2024, a AEM as a Cloud Service desativará a serialização de Resource Resolvers por meio da estrutura do Exportador de modelo do Sling. Consulte [a documentação](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obter mais detalhes.

### Recursos e APIs obsoletos {#deprecated-16971}

Para saber o que está obsoleto ou foi removido no AEM as a Cloud Service, consulte [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-16971}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak API 1.64.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.22-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.25.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
