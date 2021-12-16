---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 994ecec88f2724a75d9b11ba38c9c854a6983066
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---


# Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obter detalhes de atualizações de documentação não diretamente relacionadas a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2021.11.0) é 16 de dezembro de 2021.
A seguinte versão (2022.1.0) é em 27 de janeiro de 2022.

## Lançamento de vídeo {#release-video}

Dê uma olhada no [Visão geral da versão de dezembro de 2021](https://video.tv.adobe.com/v/339278) vídeo para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos em [!DNL Assets] {#assets-features}

* O Dynamic Media Image Smart Crop and Swatch agora é fornecido pelos serviços mais recentes da Sensei, que gera colheitas e amostras aprimoradas. Além disso, um aprimoramento foi iniciado para gerar conteúdo de corte diferente, para a mesma proporção, mas em diferentes resoluções. Além disso, qualquer edição manual será preservada durante o reprocessamento, se não houver alteração na largura e na altura do Perfil de imagem.

### Novos recursos na [!DNL Assets] canal de pré-lançamento {#assets-prerelease-features}

* [!DNL Dynamic Media] - Agora você pode usar AEM interface do Dynamic Media para configurar as Configurações gerais e a Configuração de publicação, em vez de precisar passar pelo aplicativo de desktop do Dynamic Media Classic.

* [!DNL Dynamic Media] O agora é compatível com assimilação, visualização, reprodução e publicação de vídeos MXF. A anotação e o vídeo que pode ser comprado para vídeos MXF ainda não são suportados.

* Após configurar uma conexão entre implantações remotas de DAM e Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora é possível executar as operações de atualização, exclusão, renomeação e movimentação nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites .

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Forms Portal**: Você pode usar [Forms Portal](/help/forms/configure-forms-portal.md) para listar seus formulários adaptáveis publicados em uma página do AEM Sites. Ajuda um visitante do site a descobrir todos os formulários disponíveis. Além disso, o visitante pode usar o portal de formulários para salvar e acessar rascunho de um formulário adaptável e consultar a versão PDF de um formulário adaptável enviado.

* **Externalizar AEM dados do fluxo de trabalho para processamento seguro**: Você pode armazenar dados de fluxos de trabalho em andamento AEM (dados AEM variáveis de fluxo de trabalho) que contêm elementos Sensíveis de dados pessoais (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Os elementos de dados e as variáveis de fluxo de trabalho não são armazenados AEM repositório e são buscados sob demanda de um repositório gerenciado pelo cliente durante o processamento do fluxo de trabalho.

### Novos recursos disponíveis em [!DNL Forms] canal de pré-lançamento {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) ajuda a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que permitem:

   * Gere documentos preenchendo arquivos de modelo (PDF e XDP) com dados XML.
   * Gere formulários de saída em vários formatos, incluindo fluxos de PDF não interativos.

* **Fontes personalizadas para documentos de Documento de registro e PDF criados com APIs de comunicações**: Agora é possível usar fontes aprovadas pela marca em documentos PDF gerados usando APIs de comunicações para alinhar-se aos requisitos organizacionais.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes MyAccount estendidos baseados nos componentes Peregrine extensíveis do Commerce

![Componentes de MyAccount estendidos](/help/assets/CIF/extended-myAccount-components.png)

* Os autores podem criar o ad-hoc Commerce Product Recommendations usando tipos de recomendações adicionais

* Suporte a cartões-presente na Loja AEM

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.11.0.

### Data de lançamento {#release-date-cm-nov}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.11.0 é 4 de novembro de 2021.
A próxima versão está planejada para 9 de dezembro de 2021.

### Novidades {#what-is-new-cm-nov}

* Os usuários agora podem aproveitar os novos pipelines do Front-End para implantar exclusivamente o código front-end de forma acelerada. Consulte [Pipelines de Front-End do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para saber mais.

   >[!IMPORTANT]
   >Você deve estar AEM versão `2021.10.5933.20211012T154732Z` para utilizar novos pipelines Front-End.

* A duração do pipeline de qualidade de código é significativamente reduzida ao executar a análise de código de uma maneira mais eficiente, sem a necessidade de criar uma imagem AEM inteira. Esta alteração será gradual durante as semanas que se seguem à libertação.

* A ID de confirmação de Git agora será exibida nos detalhes de execução do pipeline, facilitando o rastreamento do código que foi criado.

* A Criação de programas agora está disponível por meio da API exposta publicamente.

* A Criação de ambiente agora está disponível por meio da API exposta publicamente.

* O `x-request-id` o cabeçalho de resposta agora está visível no Reprodução da API em [www.adobe.io](https://www.adobe.io/). Esse cabeçalho é útil ao enviar problemas de atendimento ao cliente para solução de problemas.

* Como usuário, vejo que o pipeline card com zero pipelines me fornece a orientação apropriada.

* Uma nova Página de atividade agora está disponível, onde atividades como pipeline e execuções de código podem ser visualizadas junto com seus detalhes associados. Com o tempo, as atividades listadas nesta página se expanderão no escopo junto com os detalhes fornecidos.

* Uma nova página Pipelines com uma oferta de status on-hover para facilitar a visualização do resumo dos detalhes está disponível. As execuções de pipeline podem ser visualizadas junto com seus detalhes associados.

* A API Editar pipeline agora oferece suporte à alteração do ambiente usado nas fases de implantação.

* Uma otimização no processo de varredura do OakPal foi introduzida para pacotes grandes.

* O arquivo CSV do problema de qualidade agora contém o carimbo de data e hora de cada problema de qualidade.

### Correções de erros {#bug-fixes-nov}

* Certas configurações de build não ortodoxas resultaram no armazenamento de arquivos desnecessários no cache de artefatos Maven do pipeline que resultaram em I/O de rede irrelevante ao iniciar e parar o contêiner de compilação.

* A API do PATCH de pipeline falha se a fase de implantação não existir.

* O `ClientlibProxyResourceCheck` a regra de qualidade gerava problemas de falso positivo quando havia bibliotecas de clientes com caminhos de base comuns.

* Mensagem de erro quando o número máximo de repositórios foi atingido não especificou o motivo do erro.

* Em casos raros, os pipelines estavam falhando devido ao tratamento inadequado de tentativas de determinados códigos de resposta.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.2 é 1 de dezembro de 2021.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar a versão do ACS commons usada.
* Capacidade de detectar e relatar o número de usuários e subgrupos em um grupo.
* Capacidade de detectar e relatar valores de propriedade de nó no MongoDB que excedem 16MB.

### Correções de erros {#bug-fixes-bpa}

* A detecção de componentes de base foi refinada para reduzir falsos negativos.
* Para clientes do AEM Forms, mensagens de BPA relacionadas a `EMAIL_PDF_SUBMIT_ACTION` não estar disponível AEM as a Cloud Service foi corrigido.
