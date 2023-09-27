---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 0dab7428d8ae5ec4c11a88ff310fad649a365868
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 22%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13665 {#release-13665}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 13665, lançada publicamente em 27 de setembro de 2023. Esta versão de manutenção substitui a versão 13420.

A Ativação de recursos 2023.10.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13665}

* Várias melhorias nas APIs de fragmento de conteúdo.
* ASSETS-26713: Painel de ativos: novo painel da interface da experiência agora acessível na interface para toque.
* SITES-11206: fragmentos de conteúdo: API de pesquisa para fragmentos de conteúdo.
* SITES-11262: Fragmentos de conteúdo: botão para alternar para o novo Editor de fragmento de conteúdo.
* SITES-15447: Componentes principais: Lançamento da versão 2.23.4.

### Problemas corrigidos {#fixed-issues-13665}

* Várias atualizações relacionadas à tradução.
* CQ-4354428: Workflows: não é possível concluir uma tarefa na Caixa de entrada.
* SITES-9733: Fragmentos de conteúdo: as Referências do ativo no painel de referência do fragmento de conteúdo mostram 0 (zero) referências.
* SITES-14561: Fragmentos de conteúdo: HTML fixo e aprimorado para conversão de marcação.
* SITES-14882: Fragmentos de conteúdo: depois de editar o Fragmento de conteúdo e fechar a guia sem clicar no botão Salvar ou fechar, os valores são armazenados.
* SITES-15167: fragmentos de conteúdo: corrigir uma variação com uma carga inválida não retorna 400, mas 500.
* SITES-15514: Fragmentos de conteúdo: saída de Markdown malformada para tabela dentro do RTE.
* SITES-15661: Fragmentos de conteúdo: não use restrição exclusiva e reordene itens em campos de referências na API de fragmentos.
* SITES-15730: Telas: a funcionalidade Visualização de canal do Screens não funciona no painel.
* SITES-15995: Fragmentos de conteúdo: os tipos MIME de campos de texto longo do modelo e do fragmento são codificados.
* SITES-16074: Fragmentos de conteúdo: campos de tag que não são String[] não pode ser recuperado do JCR.
* SITES-16084: Fragmentos de conteúdo: CFHomeCardModelImpl com navegador de destino ausente.
* SITES-14773: Fragmentos de experiência: a referência de link não é atualizada dentro do fragmento de experiência.
* SITES-14899: Fragmentos de experiência: várias ofertas criadas para variações XF no Target.
* SITES-8590: GraphQL: problemas de codificação com variáveis em consultas persistentes.
* SITES-9224: GraphQL: exceção &quot;O gravador já foi fechado&quot; no GraphQLServlet.
* SITES-14800: GraphQL: exceção em consultas persistentes do GraphQL com variáveis.
* SITES-15586: GraphQL: problema com a filtragem de consultas persistentes com valores nulos.
* SITES-15622: GraphQL: problema com consultas persistentes com parâmetros numéricos e bool.
* SITES-15654: GraphQL: problema com uniões e propriedades com o mesmo nome.
* SITES-15267: Inicializações: a promoção não coleta páginas de inicialização modificadas antes do momento de modificar a configuração de inicialização.
* SITES-15406: Inicializações: não é possível adicionar uma página de inicialização.
* SITES-15427: Lançamentos: comportamento inconsistente do escopo &quot;Promover página atual e subpáginas&quot;.
* SITES-15429: inicializações: as páginas de criação são excluídas ao promover inicializações.
* SITES-15462: Inicializações: o processo de promoção automática publica páginas fora do escopo de promoção.
* SITES-15815: Inicializações: a página excluída do lançamento faz com que o lançamento não seja promovido com sucesso.
* SITES-15223: Editor de páginas: não é possível redimensionar componentes no emulador de tamanho de tablet.
* SITES-15463: Modelos de página: os modelos não podem ser publicados.

### Problemas conhecidos {#known-issues-13665}

Nenhum

### Tecnologias integradas {#embedded-tech-13665}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
