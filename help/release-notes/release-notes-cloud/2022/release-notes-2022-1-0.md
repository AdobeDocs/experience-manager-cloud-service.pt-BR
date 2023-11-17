---
title: Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.1.0.
description: Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.1.0.
exl-id: 1c40ab67-8fd7-4f29-b8c9-dd98b6d5b490
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 93%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.1.0 {#release-notes}

A seção a seguir descreve as notas de versão de recurso da versão 2022.1.0 do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2022.1.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 3 de fevereiro de 2022.
A data de lançamento da versão seguinte (2022.3.0) é 31 de março de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de janeiro de 2022](https://video.tv.adobe.com/v/340120) que exibe um resumo dos recursos adicionados na versão 2022.1.0.

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* O botão **[Ativar pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** está disponível no painel **Site** do console Sites, para sites que usam a versão v2 do Componente principal de página. Esse botão configura o site para carregar os temas implantados com o pipeline de front-end por cima das bibliotecas de clientes existentes.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - Agora você pode usar a interface do Dynamic Media do AEM para definir as Configurações gerais e a Configuração de publicação, em vez de precisar passar pelo aplicativo de desktop do Dynamic Media Classic.

* O [!DNL Dynamic Media] agora é compatível com a assimilação, visualização, reprodução e publicação de vídeos MXF. As funcionalidades de Anotação e vídeo que pode ser comprado ainda não são suportados para vídeos MXF.

* Após configurar uma conexão entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora é possível executar as operações [atualizar, excluir, renomear e mover](/help/assets/use-assets-across-connected-assets-instances.md) nos ativos ou pastas do DAM remoto. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites.

### Novos recursos no canal de pré-lançamento do [!DNL Assets] {#assets-prerelease-features}

* Agora, o [!DNL AEM Dynamic Media] oferece a flexibilidade para [configurar um alias de conta](/help/assets/dynamic-media/dm-alias-account.md) na interface do usuário, garantindo assim a atualização imediata dos URLs do Dynamic Media e do código de inserção do visualizador. Isso afeta positivamente o SEO, para que reflita as atualizações feitas no contexto comercial, como o processo de rebranding.

* Agora você pode usar a interface de usuário do [!DNL Experience Manager Assets] para:

   * Configurar a detecção de ativos duplicados em um repositório.

   * Configurar a adição de marcas d&#39;água digitais a imagens.

* Os administradores agora podem configurar o serviço de email para downloads grandes. Ele permite que os usuários [ativem notificações por email para downloads grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) na interface do [!DNL Experience Manager Assets]. O usuário recebe uma notificação por email contendo o link de download do arquivo ZIP após concluir o processo de download.


* O recurso [Gerenciar publicação](/help/assets/manage-publication.md) está aprimorado, com uma interface de usuário melhorada. Os usuários podem publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, [adicionar conteúdo](/help/assets/manage-publication.md#add-content) à lista de publicação em todo o repositório DAM, [incluir configurações de pasta](/help/assets/manage-publication.md#include-folder-settings) para publicar o conteúdo das pastas selecionadas e aplicar filtros, e [agendar publicações](/help/assets/manage-publication.md#publish-assets-later) para uma data ou hora posterior.

### Correções de erros {#bug-fixes}

* Durante a migração de ativos do AEM local para os serviços em nuvem, os ativos não processados e sem representação original são enviados ao Asset Compute para processamento.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que possibilitam a você:

   * Gerar documentos preenchendo arquivos de modelo com dados XML.
   * Gerar formulários em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   * Gerar PDFs de impressão a partir de PDFs de formulário XFA.
   * Gerar documentos PDF, PostScript, PCL e ZPL em massa ao mesclar vários conjuntos de dados com modelos de origem.

* **Fontes personalizadas para Documentos de Registro e documentos PDF criados com APIs de comunicações**: agora é possível usar fontes aprovadas pela marca em documentos PDF gerados pelo uso de APIs de comunicações para se alinhar aos requisitos organizacionais.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[API do Assembler](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: APIs do Assembler para combinar, reorganizar, aumentar e obter informações sobre documentos PDF.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes myAccount aprimorados
* O componente Recomendação de produto oferece suporte a tipos de página adicionais (página inicial, carrinho de compras, confirmação de pedido)
* **Lista de desejos**
   * Os visitantes conectados podem adicionar produtos a uma lista de desejos
   * O gerenciamento da lista de desejos e de seus produtos é possível por meio da opção myAccount
   * O botão “Adicionar à lista de desejos” pode ser ativado/desativado no nível de componente por meio de uma política (por exemplo, teaser de produto, detalhes do produto)
   * Disponível como um Componente principal e na loja AEM Venia

![Lista de desejos](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2022.01.0 é 20 de janeiro de 2022. A próxima versão está planejada para 10 de fevereiro de 2022.

### Novidades {#what-is-new-cm}

* O Cloud Manager [evitará reconstruir a base de código quando detectar que a mesma Git Commit é usada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) em várias execuções de pipeline de pilha completa.
* Acessar o log de ambiente AEM agora requer o perfil de produto **Gerente de implantação**. Os usuários sem esse perfil veem um botão desativado na interface.
* A interface não permitirá a configuração de pipeline de front-end para um programa em que o Sites não está habilitado como uma solução.
* Ao gerar uma senha Git, a data de expiração é exibida.

### Correções de erros {#bug-fixes-cm}

* Foram corrigidas exceções de ponteiro nulo encontradas por algumas implantações de pipeline front-end.
* As variáveis de ambiente agora podem ser adicionadas, atualizadas e excluídas quando um ambiente estiver executando uma versão desatualizada do AEM.
* A etapa de criação de imagem não será mais marcada como ERRO para pipelines que usaram a etapa agendada em determinados casos raros.
* Para programas com apenas um repositório, a tela de execução do pipeline agora exibirá o nome do repositório.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.8.6 é 3 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Validação de conteúdo - os usuários podem determinar com garantia se todo o conteúdo que foi extraído pela ferramenta Transferência de conteúdo foi assimilado com sucesso na instância de destino. Para usar esse recurso, ative-o na `System Console` do ambiente AEM de origem. Consulte [Validação de transferências de conteúdo - Introdução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=pt-BR#getting-started) para obter mais detalhes.

### Correções de erros {#bug-fixes-ctt}

* Alguns usuários não foram mapeados porque o mapeamento de usuários diferenciava letras maiúsculas de letras minúsculas. Isso foi corrigido. O mapeamento de usuário não diferencia mais letras maiúsculas de letras minúsculas.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.24 é 1º de fevereiro de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e gerar relatórios sobre o número de ativos com e sem Tags inteligentes.
* Capacidade de detectar e gerar relatórios sobre a versão do Componente principal usada.
* Capacidade de detectar e gerar relatórios sobre o tipo de camada de origem (Autor ou Publicação) em que o BPA foi executado.

### Correções de erros {#bug-fixes-bpa}

* A lógica de dimensionamento de BPA ficou mais rápida e eficiente.
* Em alguns cenários, o BPA não incrementou a contagem analisada quando foi executado. Isso foi corrigido.
