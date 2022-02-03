---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 3c6b25bdcc626946ae7bd4b98da65f4ccfd963f7
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 31%

---


# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] versão atual (2022.1.0) é 3 de fevereiro de 2022.
A seguinte versão (2022.2.0) é em 24 de fevereiro de 2022.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de janeiro de 2022](https://video.tv.adobe.com/v/340120) vídeo para obter um resumo dos recursos adicionados na versão 2022.1.0.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - Agora você pode usar a interface do Dynamic Media do AEM para definir as Configurações gerais e a Configuração de publicação, em vez de precisar passar pelo aplicativo de desktop do Dynamic Media Classic.

* O [!DNL Dynamic Media] agora é compatível com a assimilação, visualização, reprodução e publicação de vídeos MXF. As funcionalidades de Anotação e vídeo que pode ser comprado ainda não são suportados para vídeos MXF.

* Após configurar uma conexão entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora você pode executar o [atualizar, excluir, renomear e mover operações](/help/assets/use-assets-across-connected-assets-instances.md) nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites.

### Novos recursos no canal de pré-lançamento do [!DNL Assets] {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] oferece a flexibilidade para [configurar uma conta alias](../../assets/dynamic-media/dm-alias-account.md) na interface do usuário, garantindo assim a atualização imediata dos URLs do Dynamic Media e do código de inserção do visualizador. Isso afeta positivamente a SEO, para refletir as atualizações feitas no contexto de negócios, como rebranding.

* Agora você pode usar o [!DNL Experience Manager Assets] interface do usuário para:

   * Configure a detecção de ativos duplicados em um repositório.

   * Configure a adição de marcas d&#39;água digitais a imagens.

* Os administradores agora podem configurar o serviço de email para downloads grandes. Ela permite que os usuários habilitem notificações por email para downloads grandes da [!DNL Experience Manager Assets] interface. O usuário recebe uma notificação por email contendo o link de download da pasta zip arquivada após concluir o processo de download.


* O recurso Gerenciar publicação é aprimorado com uma interface do usuário aprimorada. Os usuários podem publicar ou cancelar a publicação de conteúdo de e para o destino selecionado, Adicionar conteúdo à lista de publicação no repositório DAM, Incluir configurações da pasta para publicar o conteúdo das pastas selecionadas e aplicar filtros, e agendar a publicação para uma data ou hora posterior.

### Correções de erros {#bug-fixes}

* Os ativos não processados sem representação original são enviados ao Asset compute para processamento ao migrar ativos do AEM local para os serviços em nuvem.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que possibilitam a você:

   * Gere documentos preenchendo arquivos de modelo com dados XML.
   * Gere formulários em vários formatos, incluindo fluxos de PDF não interativos.
   * Gere PDF de impressão a partir de PDF de formulário XFA.
   * Gere documentos PDF, PostScript, PCL e ZPL em massa ao mesclar vários conjuntos de dados com modelos de origem.

* **Fontes personalizadas para Documentos de Registro e documentos PDF criados com APIs de comunicações**: agora é possível usar fontes aprovadas pela marca em documentos PDF gerados pelo uso de APIs de comunicações para se alinhar aos requisitos organizacionais.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[API do Assembler](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: APIs do Assembler para combinar, reorganizar, aumentar e obter informações sobre documentos do PDF.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes da minha conta aprimorados
* O componente Recomendação de produto suporta tipos de página adicionais (página inicial, carrinho de compras, confirmação de pedido)
* **Lista de desejos**
   * Os visitantes conectados podem adicionar produtos a uma lista de desejos
   * O gerenciamento da lista de desejos e seus produtos é possível por meio da myAccount
   * O botão &quot;Adicionar à lista de desejos&quot; pode ser ativado/desativado em um nível de componente por meio de uma política (por exemplo, teaser de produto, detalhes do produto
   * Disponível como um componente principal e na loja AEM Venia

![Lista de desejos](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

Esta página descreve as notas de versão do Cloud Manager AEM as a Cloud Service 2022.01.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2022.01.0 é 20 de janeiro de 2022. A próxima versão está planejada para 10 de fevereiro de 2022.

### Novidades {#what-is-new-cm}

* O Cloud Manager [evite reconstruir a base de código quando detecta que a mesma confirmação de git é usada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) em várias execuções de pipeline de pilha completa.
* Agora, para acessar o log de ambiente AEM é necessário **Gerenciador de implantação** perfil do produto. Os usuários sem esse perfil verão um botão desativado na interface do usuário.
* A interface do usuário não permitirá a configuração de pipeline de front-end para um programa em que o Sites não está habilitado como uma solução.
* Após gerar uma senha git, a data de expiração será exibida.

### Correções de erros {#bug-fixes-cm}

* Exceções de ponteiro nulo encontradas por algumas implantações de pipeline front-end foram corrigidas.
* As variáveis de ambiente agora podem ser adicionadas, atualizadas e excluídas quando um ambiente estiver executando uma versão desatualizada do AEM.
* A etapa de criação de imagem não será mais marcada como ERRO para pipelines que usaram a etapa agendada em determinados casos raros.
* Para programas com apenas um repositório, a tela de execução do pipeline agora exibirá o nome do repositório.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.24 é 1 de fevereiro de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar o número de ativos com e sem Tags inteligentes.
* Capacidade de detectar e relatar a versão do Componente principal usado.
* Capacidade de detectar e gerar relatórios sobre o tipo de camada de origem (Autor ou Publicação) em que o BPA foi executado.

### Correções de erros {#bug-fixes-bpa}

* A lógica de dimensionamento de BPA ficou mais rápida e eficiente.
* Em alguns cenários, o BPA não incrementou a contagem analisada quando foi executado. Isso foi corrigido.
