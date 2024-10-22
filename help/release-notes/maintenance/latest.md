---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 19%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 18311 {#18311}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 18311, lançada publicamente em quarta-feira, 22 de outubro de 2024. A versão de manutenção anterior era a versão 18175.

A ativação de recursos 2024.10.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-18311}

* ASSETS-41820 : Melhorias de indexação para watchdog de processamento.
* ASSETS-43720 : Melhorias funcionais no watchdog de processamento.
* ASSETS-42554: Melhorias de desempenho para pastas grandes.
* SKYOPS-77603 : Gerenciamento de redirecionamentos por usuários empresariais.

### Problemas corrigidos {#fixed-issues-18311}

* ASSETS-37534 : alterações na pesquisa para não expor a propriedade usada para o destino de aprovação.
* ASSETS-38322 : Remover configuração do provedor de critérios de publicação Remover recurso de evento de publicação.
* ASSETS-40482 : problema de acessibilidade nos botões reproduzir/pausar e ativar mudo/ativar mudo no reprodutor de vídeo do Scene7.
* ASSETS-40593 : A página de erro ocorre depois de clicar no botão &quot;Propriedades&quot; em Assets > Arquivos.
* ASSETS-40598 : sincroniza cortes inteligentes quando um ativo não sincronizado é movido para uma pasta habilitada para sincronização.
* ASSETS-40743 : problemas com o acionamento da caixa de diálogo Substituir ativo quando determinados caracteres existem no nome de arquivo.
* ASSETS-40825 : Aspectos De Pesquisa Do Assets Desaparecem Após A Edição Do Formulário De Pesquisa.
* ASSETS-41007 : A exclusão do AEM às vezes deixa o Assets órfão no delivery.
* ASSETS-41172 : caracteres especiais de Modelos do Dynamic Media não permitidos no nome.
* ASSETS-41896 : a Assets mencionada no cq:propriedade discarded na pasta NÃO deve ser publicada no Brand Portal.
* ASSETS-42067: Modelos do Dynamic Media - O download fornece um erro.
* ASSETS-42070 : Modelos do Dynamic Media - Usuários não administradores devem ter acesso de criação/edição ao Modelo.
* ASSETS-42344 : Sincronização do Assets conectada desconectada - Reconectar e aviso para o cliente.
* ASSETS-42620: problema com a opção de visualização de versões de ativos - mostra a visualização em branco quando abrimos o ativo.
* ASSETS-42701: Problema de entrega e corte de imagens otimizadas para a Web.
* ASSETS-42966 : Barricadas assíncronas podem ser desbloqueadas com erro se vários trabalhos compartilharem o mesmo caminho.
* ASSETS-43072 : Modelos do Dynamic Media - A pesquisa de referências de modelo falha em uma referência inválida.
* ASSETS-43212 : problemas de internacionalização no editor de esquema de metadados.
* ASSETS-43202 : correções para selecionar anotações para imprimir a partir da linha do tempo.
* ASSETS-43502: Nome da predefinição de imagem existente AEM CS não exibido na página Editar.
* ASSETS-43538 : o trabalho de cópia assíncrona de ativos usa propriedades incorretas para o caminho de origem.
* ASSETS-43798 : Verifique o caminho de destino primeiro antes de copiar ativos.
* ASSETS-43945 : aumente o atraso de repetição para 20 min para fila de trabalhos de ativos assíncronos.
* ASSETS-44025 : o trabalho de exclusão assíncrona de ativos falha para quando ativos individuais são selecionados.
* SITES-26128: exceção de conversão de classe em CreateLiveCopyStep.
* SCRNS-4551 : [Pools do SG] O canal do Screens que contém o componente de vídeo mostra &quot;Erro geral de página&quot; na visualização e no player do navegador

### Problemas conhecidos {#known-issues-18311}

* FORMS-15818: A entrada do descritor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` não encontrou instruções nos logs do servidor. Estas são instruções de registro inofensivas.

### Recursos e APIs obsoletos {#deprecated-18311}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-18311}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda três vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-18311}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
