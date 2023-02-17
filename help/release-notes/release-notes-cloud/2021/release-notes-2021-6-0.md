---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0.
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 7b21a8af886c8e1f209e3b7cc5d94de5c58be1ac
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 34%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2021.6.0 é 28 de junho de 2021.
A seguinte versão (2021.7.0) será lançada em 29 de julho de 2021.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de junho de 2021](https://video.tv.adobe.com/v/334296) vídeo para obter um resumo dos recursos adicionados.

## XML Documentation para o AEM as a Cloud Service {#xml-documentation}

### Novidades {#what-is-new-xml-documentation}

* XML Documentation para AEM as a Cloud Service agora está disponível.
* Isso permitirá que os clientes atuais do AEM Cloud Service adquiram o complemento XML Documentation para importar, criar, gerenciar e fornecer conteúdo técnico em vários canais, incluindo sites de AEM

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.6.0 e 2021.5.0.

### Data de lançamento {#release-date-june-cm}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.6.0 é 10 de junho de 2021.
A próxima versão está planejada para 15 de julho de 2021.

### Novidades {#what-is-new-junecm}

* O Serviço de visualização será implantado continuamente em todos os programas. Os clientes serão notificados no produto quando o programa estiver ativado para o Serviço de visualização. Consulte [Acesso ao serviço de visualização](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obter mais detalhes.

* As Dependências do Maven baixadas durante a etapa de compilação agora serão armazenadas em cache entre as execuções de pipeline. Esse recurso será ativado para os clientes nas próximas semanas.

* O nome do programa agora pode ser editado por meio da caixa de diálogo Editar programa.

* O nome da ramificação padrão usado durante a criação do projeto e no comando de push padrão por meio do gerenciamento de fluxos de trabalho do Git foi alterado para `main`.

* A experiência de edição do programa na interface do usuário foi atualizada.

* A regra de qualidade `ImmutableMutableMixCheck` foi atualizada para classificar os nós `/oak:index` como sendo imutáveis.

* As regras de qualidade `CQBP-84` e `CQBP-84--dependencies` foram consolidadas em uma única regra. Como parte dessa consolidação, a verificação de dependências identifica com mais precisão os problemas em dependências de terceiros que estão sendo implantadas no tempo de execução do AEM.

* Para evitar confusão, as linhas de segmento Publicar AEM e Publicar Dispatcher na página Detalhes do ambiente foram consolidadas.

   ![](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* Uma nova regra de qualidade do código foi adicionada para validar a estrutura dos índices `damAssetLucene`. Consulte [Índices Oak Lucese Asset DAM personalizados](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) para obter mais detalhes.

* A página Detalhes do ambiente agora exibe vários nomes de domínio para os serviços de publicação e visualização (conforme aplicável). Consulte [Detalhes do ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.

### Correções de erros {#bug-fixes-junecm}

* As definições de nó JCR contendo uma nova linha após o nome do elemento raiz não eram analisadas corretamente.

* A API dos repositórios de lista não filtrava repositórios excluídos.

* Uma mensagem de erro incorreta era exibida quando um valor inválido era fornecido para a etapa de agendamento.

* Ocasionalmente, o usuário poderia ver um status verde *ativo* ao lado de uma Lista de permissões de IP, mesmo quando essa configuração não tinha sido implantada.

* Algumas sequências de edição de programas poderiam resultar na incapacidade de criar ou editar o pipeline de produção.

* Algumas sequências de edição de programas poderiam resultar na exibição de uma mensagem enganosa na página **Visão geral** para executar novamente a configuração do programa.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#ga-features-assets}

* A funcionalidade de Automação de conteúdo permite [!DNL Experience Manager Assets] utilize o [!DNL Adobe Creative Cloud] APIs para automatizar a produção de ativos em escala. Melhora a velocidade do conteúdo diminuindo drasticamente o tempo gasto e as iterações necessárias para criar variações do mesmo ativo. A funcionalidade não requer nenhum código e funciona no DAM.
* [!DNL Adobe Asset Link] v3.0 para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] e [!DNL Adobe Asset Link] v2.0 para [!DNL Adobe XD] for liberado. Ele fornece:

   * Suporte para [!DNL Assets Essentials].
   * Capacidade de se conectar automaticamente ao [!DNL Experience Manager] como [!DNL Cloud Service] ou [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Novos recursos disponíveis na [!DNL Assets] canal de pré-lançamento {#beta-features-assets}

* As configurações de exibição são aprimoradas para permitir que os usuários escolham uma exibição padrão e um parâmetro de classificação padrão.
* A funcionalidade de download do Linkshare usa downloads assíncronos que aumentam a velocidade de download.
* Os usuários podem pesquisar e filtrar as pastas com base em predicados de propriedade.
* [!DNL Experience Manager Assets] incorpora o Visualizador de PDF equipado com [!DNL Adobe Document Cloud] para visualizar os documentos suportados. Esse recurso permite que os usuários visualizem o PDF e outros arquivos de várias páginas sem nenhum processamento complexo. Isso melhora a paridade de recursos com [!DNL Experience Manager] 6.5.

### Erros corrigidos em [!DNL Assets] {#bugs-fixed-assets}

* Ao adicionar um proprietário a uma subpasta, [!DNL Assets] também adiciona o mesmo usuário como um proprietário da pasta pai. (CQ-4323737)
* Ao adicionar ativos a Coleções, se um usuário aplicar um filtro na pesquisa Coleções, ele não poderá exibir as Coleções na exibição Lista . (CQ-4323181)
* Ao pesquisar arquivos e pastas, se o usuário aplicar um filtro e selecionar [!UICONTROL Arquivos e pastas], somente os arquivos são exibidos, mas não a pasta. (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Sites] {#ga-features-sites}

* Publicar na camada de visualização agora é exibido como status da página na interface do usuário de administração do Sites
* Publicar na camada de visualização agora exibe o URL de visualização no final da ação e persiste o URL nas propriedades da página para referência posterior

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* Adição da capacidade de filtrar colunas personalizadas AEM Caixa de entrada.
* Adição da capacidade de usar o editor de temas e a camada de estilo do editor de formulário adaptável para criar estilo no componente captcha.
* Melhoria na velocidade e precisão para detectar automaticamente seções lógicas nos PDF forms de origem e convertê-las em painéis de formulário adaptáveis correspondentes.
* Adição da ação de mover para mover um arquivo PDF ou XDP de uma pasta para outra.

### Recurso beta de [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: As APIs de comunicação ajudam a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   * Gere documentos de formulário finais preenchendo arquivos de modelo com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   * Gere PDF de impressão a partir de um PDF de formulário XFA e Formulário Adobe Acrobat (AcroForm).

* **Externalizador de dados de variáveis**: Você pode salvar dados de variáveis de Fluxo de trabalho AEM em um sistema de armazenamento externo gerenciado por sua organização.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

### Erros corrigidos em [!DNL Forms] {#forms-bugs-fixed}

* Quando um campo é validado antes de enviar dados para o serviço de backend por meio do FDM (Form Data Model), as validações são bem-sucedidas, mas o serviço do Modelo de dados de formulário não consegue invocar a validação posterior.
* Às vezes, ao enviar um formulário contendo um campo de carregamento HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 bytes é recebido na outra extremidade. Esse é um problema conhecido no Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

Esta seção descreve as Notas de versão do AEM Screens as a Cloud Service.

### Data de lançamento {#release-date-june-screens}

A data de lançamento da AEM Screens as a Cloud Service é 24 de junho de 2021.

### Novidades {#what-is-new-screens-june}

>[!NOTE]
>Consulte [AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) Guia para o conhecimento fundamental necessário para instalar, configurar e executar com êxito o Screens as a Cloud Service e vincular a documentação técnica de conceitos detalhados.

* O gerenciamento do registro de dispositivos em massa significa que o provisionamento de grandes quantidades de dispositivos de player é mais rápido e eficiente.

* Opções de pesquisa e filtro aprimoradas para cada visualização de inventário de Dispositivo, Exibição e Canal.

* O instantâneo de integridade do dispositivo economiza tempo, fornecendo um status crítico.

* A página Detalhes do objeto oferece um resumo das informações mais relevantes para cada objeto do projeto.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Novos tipos de dados de referência de produto e categoria da CIF para Fragmentos de conteúdo (Incl. suporte à interface do usuário do seletor de categoria/produto)
* Novo Componente principal do fragmento de conteúdo de comércio
* Pesquisa de comércio de texto completo compatível com AEM backend
* Os Componentes principais do Commerce são compatíveis com a coleta de dados do Adobe Commerce Sensei Recs
* URLs compatíveis com SEO aprimorados para páginas de categoria
* Suporte para cabeçalhos HTTP personalizados por site/configuração

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.5.4 é 28 de junho de 2021.

### Novidades {#what-is-new-ctt-latest}

* Suporte para um [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) etapa adicionada para usar com CTT. A etapa de pré-cópia pode ser usada para acelerar significativamente as fases de extração e assimilação da atividade de transferência de conteúdo quando a instância de origem AEM está configurada para usar um armazenamento de dados Amazon S3 ou Azure Blob Storage.

* A grade de proteção foi adicionada à CTT para impedir que os usuários interrompam uma assimilação e possivelmente corrompam dados depois de atingir o ponto crítico durante a fase de assimilação.

* Os logs de extração foram mais descritivos para ajudar na solução de problemas.

* Adicionadas mais mensagens descritivas sobre o status de assimilação na interface do usuário.

### Correções de erros {#bug-fixes-ctt-latest}

* Ao parar uma assimilação na instância do autor, a interface do usuário substituiu uma assimilação concluída anteriormente na instância de publicação para `STOPPED` from `FINISHED`. Isso foi corrigido.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.16 é 30 de junho de 2021.

### Novidades {#what-is-new-bpa-latest}

* Capacidade de detectar e relatar os nós filhos ausentes nas pastas em `/content/dam`.

* Capacidade de detectar e relatar a versão do Analisador de práticas recomendadas usada.

### Correções de erros {#bug-fixes-bpa-latest}

* Corrigido um erro de registro relacionado à Estrutura de Repositório (URS) Não Suportada.
