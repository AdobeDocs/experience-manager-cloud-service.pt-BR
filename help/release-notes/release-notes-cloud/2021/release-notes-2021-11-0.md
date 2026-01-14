---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0.
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 93%

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

A data de lançamento da versão atual do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.11.0) é 16 de dezembro de 2021.
A data de lançamento da versão seguinte (2022.1.0) é sexta-feira, 3 de fevereiro de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de dezembro de 2021](https://video.tv.adobe.com/v/339278) para um resumo dos recursos adicionados na versão 2021.11.0 (novembro de 2021).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* O Corte inteligente e a Amostra de imagens do Dynamic Media agora são potencializados pelos serviços mais recentes de IA da Adobe, que geram melhores cortes e amostras. Além disso, um aprimoramento foi iniciado para gerar conteúdo de corte diferente, para a mesma proporção, mas em diferentes resoluções. Além disso, as edições manuais são preservadas no reprocessamento, se não houver alteração na largura e na altura do Perfil de imagem.

### Novos recursos no canal de pré-lançamento do [!DNL Assets] {#assets-prerelease-features}

* [!DNL Dynamic Media] - Agora você pode usar a interface do Dynamic Media do AEM para definir as Configurações gerais e a Configuração de publicação, em vez de precisar passar pelo aplicativo de desktop do Dynamic Media Classic.

* O [!DNL Dynamic Media] agora é compatível com a ingestão, visualização, reprodução e publicação de vídeos MXF. As funcionalidades de Anotação e vídeo que pode ser comprado ainda não são suportados para vídeos MXF.

* Após configurar uma conexão entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora é possível executar as operações [atualizar, excluir, renomear e mover](/help/assets/use-assets-across-connected-assets-instances.md) nos ativos ou pastas do DAM remoto. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Externalizar dados do fluxo de trabalho do AEM para processamento seguro**: Você pode armazenar dados de fluxos de trabalho em andamento do AEM (dados de variáveis de fluxo de trabalho do AEM) que contêm elementos de Dados pessoais sensíveis (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Os elementos de dados e as variáveis de fluxo de trabalho não são armazenados no repositório do AEM e são buscados sob demanda de um repositório gerenciado pelo cliente durante o processamento do fluxo de trabalho.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que possibilitam a você:

   * Gerar documentos preenchendo arquivos de modelo (PDF e XDP) com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.

* **Fontes personalizadas para Documentos de Registro e documentos PDF criados com APIs de comunicações**: agora é possível usar fontes aprovadas pela marca em documentos PDF gerados pelo uso de APIs de comunicações para se alinhar aos requisitos organizacionais.

* **Forms Portal**: Você pode usar o [Forms Portal](/help/forms/configure-forms-portal.md) para listar seus formulários adaptáveis publicados em uma página do AEM Sites. Isso ajuda um visitante do site a descobrir todos os formulários disponíveis. Além disso, o visitante pode usar o portal de formulários para salvar e acessar o rascunho de um formulário adaptável e consultar a versão em PDF de um formulário adaptável enviado.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Componentes myAccount estendidos baseados nos componentes Peregrine extensíveis do Commerce

![Componentes myAccount estendidos](/help/assets/CIF/extended-myAccount-components.png)

* Os autores podem criar Commerce Product Recommendations ad-hoc usando tipos de recomendações adicionais

* Suporte a cartões-presente na vitrine do AEM

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.11.0.

### Data de lançamento {#release-date-cm-nov}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.11.0 é 4 de novembro de 2021.
A próxima versão está planejada para 9 de dezembro de 2021.

### Novidades {#what-is-new-cm-nov}

* Os usuários agora podem aproveitar os novos pipelines de front-end para implantar exclusivamente o código de front-end de forma acelerada. Consulte [Pipelines de front-end do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para saber mais.

  >[!IMPORTANT]
  >Você deve estar no AEM versão `2021.10.5933.20211012T154732Z` ou superior para usar novos pipelines de Front-End.

* A duração do pipeline de qualidade de código é significativamente reduzida ao executar a análise de código de uma maneira mais eficiente, sem a necessidade de criar uma imagem completa do AEM. Esta alteração será gradual durante as semanas que se seguem ao lançamento.

* A Git Commit ID agora será exibida nos detalhes de execução do pipeline, facilitando o rastreamento do código que foi criado.

* A Criação de programas agora está disponível por meio da API exposta publicamente.

* A Criação de ambiente agora está disponível por meio da API exposta publicamente.

* O cabeçalho de resposta `x-request-id` agora está visível na API Playground em [www.adobe.io](https://www.adobe.io/). Esse cabeçalho é útil ao enviar problemas de atendimento ao cliente para solução de problemas.

* Como usuário, vejo que o cartão do pipeline com zero pipelines me fornece a orientação apropriada.

* Uma nova Página de atividade agora está disponível, em que atividades como pipeline e execuções de código podem ser visualizadas junto a seus detalhes associados. Com o tempo, as atividades listadas nesta página se expandirão em escopo junto com os detalhes fornecidos.

* Uma nova página Pipelines, com um popover de status ao passar o mouse para facilitar a visualização do resumo dos detalhes, está disponível. As execuções de pipeline podem ser visualizadas junto com seus detalhes associados.

* A API Editar pipeline agora oferece suporte à alteração do ambiente usado nas fases de implantação.

* Uma otimização no processo de varredura do OakPal foi introduzida para pacotes grandes.

* O arquivo CSV de problemas de qualidade agora contém o carimbo de data e hora de cada problema de qualidade.

### Correções de erros {#bug-fixes-nov}

* Certas configurações de build não ortodoxas resultaram no armazenamento de arquivos desnecessários no cache de artefatos do Maven no pipeline, o que resultou em I/O de rede irrelevantes ao iniciar e parar o contêiner de compilação.

* A API do PATCH de pipeline falha se a fase de implantação não existir.

* A regra de qualidade `ClientlibProxyResourceCheck` gerava problemas de falso positivo quando havia bibliotecas de clientes com caminhos de base comuns.

* A mensagem de erro quando o número máximo de repositórios era atingido não especificava o motivo do erro.

* Em casos raros, os pipelines estavam falhando devido ao manuseio de novas tentativas inadequado de determinados códigos de resposta.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.22 é 1º de dezembro de 2021.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar a versão do ACS commons usada.
* Capacidade de detectar e relatar o número de usuários e subgrupos em um grupo.
* Capacidade de detectar e relatar valores de propriedade do nó no MongoDB que excedam 16MB.

### Correções de erros {#bug-fixes-bpa}

* A detecção de componentes de base foi refinada para reduzir falsos negativos.
* Para clientes do AEM Forms, as mensagens de BPA relacionadas a `EMAIL_PDF_SUBMIT_ACTION` não estarem disponíveis no AEM as a Cloud Service foram corrigidas.
