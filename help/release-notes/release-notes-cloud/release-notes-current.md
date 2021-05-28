---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: dc66eca7b789cf3be1aeae3d63935362ab6f918a
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---


# Notas de versão atuais para [!DNL Adobe Experience Manager] como Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais para a versão atual (mais recente) de [!DNL Experience Manager] como um Cloud Service.

>[!NOTE]
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obter detalhes das atualizações de documentação não diretamente relacionadas a uma versão.

## Data de lançamento {#release-date}

A Data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2021.5.0 é 27 de maio de 2021.
A seguinte versão (2021.6.0) será lançada em 24 de junho de 2021.

## AEM como uma fundação de Cloud Service {#foundation}

### Novidades no AEM como um Cloud Service Foundation {#what-is-new-foundation}

* [Canal](/help/release-notes/prerelease.md) de pré-lançamento: Visualize os recursos futuros por um mês inteiro antes de eles entrarem em produção!

* [Substituição](/help/release-notes/deprecated-apis.md) da API: uma lista das APIs obsoletas mais recentes para o AEM as a Cloud Service está disponível.

* [AEM como um plug-in Maven do Cloud Service SDK Build Analyzer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html): Atualize seus projetos maven para a versão mais recente, que inclui uma verificação da API Java obsoleta e outras melhorias.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novidades em [!DNL Sites] {#what-is-new-sites}

* Em breve, você poderá verificar o conteúdo em um novo [Camada de visualização](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para simular a aparência da experiência final e a experiência como faria no nível de Publicação. Isso é ativado pelo assistente de Publicação gerenciada do AEM Sites , que agora permite escolher um destino de publicação entre Publicar ou Visualizar. As experiências na Visualização podem ser acessadas por um URL dedicado. Após a validação em Visualizar, o conteúdo pode ser publicado de Autor para Publicar como de costume. Habilitar o Serviço de visualização no AEM como ambientes Cloud Service será implementado gradualmente nas próximas semanas.

## [!DNL Adobe Experience Manager Assets] como  [!DNL Cloud Service] {#assets}

### Novos recursos disponíveis no canal de pré-lançamento {#what-is-new-assets-prerelease}

* Os esquemas de metadados podem ser aplicados diretamente às propriedades da pasta.

   ![Adicionar esquema de metadados das propriedades da pasta](/help/assets/assets/metadata-schema-folder-properties.png)

* A ferramenta Ingestor em massa de ativos permite adicionar metadados durante uma assimilação em massa.

* As melhorias na experiência do usuário exibem o número de ativos presentes em uma pasta. Para mais de 1000 ativos em uma pasta, [!DNL Assets] exibe 1000+.

   ![O número de ativos em uma pasta é exibido na interface](/help/assets/assets/browse-folder-number-of-assets.png)

### Erros corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* Fazer upload de arquivos muito grandes trava o [!DNL Experience Manager desktop app]. (CQ-4320942)
* As opções da barra de ferramentas são diferentes quando a mesma Coleção é selecionada de uma pasta e quando é selecionada de um resultado de pesquisa. (CQ-4321406)

#### Novidades em [!DNL Dynamic Media] {#what-is-new-dm}

* A taxa de pixels do dispositivo de imagem inteligente (DPR) e a otimização da largura de banda da rede permitem que você forneça imagens de melhor qualidade com eficiência, em dispositivos com telas de alta resolução e largura de banda de rede restrita. Consulte as [perguntas frequentes sobre a geração inteligente de imagens](/help/assets/dynamic-media/imaging-faq.md).

   >[!NOTE]
   >
   >A linha do tempo da versão para os aprimoramentos de Smart Imaging acima é:
   >
   >* América do Norte 24 de maio de 2021 em NA,
      >
      >
   * Europa, Oriente Médio e África 25 de junho de 2021,
      >
      >
   * Ásia-Pacífico em 19 de julho de 2021.


* Introdução do suporte para o formato de imagem da próxima geração AVIF na entrega [!DNL Dynamic Media] (modificador de URL fmt).

   >[!NOTE]
   >
   >A linha do tempo da versão do suporte a AVIF é:
   >
   >* América do Norte, 10 de maio de 2021,
      >
      >
   * Europa, Oriente Médio e África 24 de maio de 2021,
      >
      >
   * Ásia-Pacífico, 24 de junho de 2021.


## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.5.0.

### Data de lançamento {#release-date-cm-may}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.5.0 é 6 de maio de 2021.
A próxima versão está planejada para 10 de junho de 2021.

### Novidades {#what-is-new-may}

* A regra de qualidade PackageOverlaps agora detecta casos em que o mesmo pacote foi implantado várias vezes, ou seja, em vários locais incorporados, no mesmo conjunto de pacotes implantado.

* O endpoint do repositório na API pública agora inclui o URL do Git.

* O log de implantação baixado por um usuário do Cloud Manager será mais revelador e incluirá detalhes sobre falhas e cenários de sucesso.

* Falhas intermitentes encontradas ao enviar o código para o Adobe git foram resolvidas.

* O complemento Commerce agora pode ser aplicado a programas Sandbox durante o fluxo de trabalho Editar programa .

* A experiência Editar programa foi atualizada.

* A tabela Nomes de Domínio na página Detalhes do Ambiente exibirá até 250 nomes de Domínio por paginação.

* A guia Soluções nos fluxos de trabalho Adicionar programa e Editar programa exibirá a solução, mesmo que apenas uma solução esteja disponível para o programa.

* A mensagem de erro no log de etapas da criação quando a build não produziu nenhum pacote de conteúdo implantado não estava clara.

### Correções de erros {#bug-fixes-cm-may}

* Ocasionalmente, o usuário pode ver um status verde &quot;ativo&quot; ao lado de uma Lista de permissões de IP, mesmo quando essa configuração não foi implantada.

* Em vez de remover variáveis &quot;excluídas&quot;, a API de variáveis de pipelines somente as marcaria com o status **DELETED**.

* Alguns problemas de qualidade do tipo Código Smell estavam afetando incorretamente a Classificação de confiabilidade.

* Como domínios curingas não são compatíveis, a interface do usuário não permitirá que o usuário envie um domínio curinga.

* Quando uma execução de pipeline era iniciada entre meia-noite e 1h UTC, a versão de artefato gerada pelo Cloud Manager não tinha garantia de ser maior do que uma versão criada no dia anterior.

* Durante a configuração do programa de sandbox, depois que o projeto com código de amostra for criado com êxito, o Gerenciar Git será exibido como um link do cartão herói na página Visão geral .

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.4.0 é 11 de maio de 2021.

### Novidades {#what-is-new-ctt-may}

* Essa versão da ferramenta Transferência de conteúdo cria representações de texto para ativos que estão sendo migrados para o Cloud Service. As representações de texto são necessárias para suportar a pesquisa de texto completo em ativos assimilados.
* O número máximo de conjuntos de migração da ferramenta Transferência de conteúdo que um usuário pode criar foi aumentado de 4 para 10.

### Correções de erros {#bug-fixes-ctt-may}

* Várias correções de erros relacionadas ao recurso de atualização automática na interface do usuário da ferramenta Transferência de conteúdo .
* A ferramenta Transferência de conteúdo com `wipe=true` resultou em um índice de contador incorreto no destino. Isso foi corrigido.

## Complemento do Commerce {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Suporte à paginação para conteúdo associado nas propriedades do console do produto

### Correções de erros {#bug-fixes-commerce}

* Miniaturas de ativos não exibidas na guia Ativo das propriedades do produto

* A navegação estrutural redefine os dados de visualização no console do produto
