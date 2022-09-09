---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0.
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 12%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2021.5.0 é 27 de maio de 2021.
A seguinte versão (2021.6.0) será lançada em 28 de junho de 2021.

## AEM fundação as a Cloud Service {#foundation}

### Novidades AEM fundação as a Cloud Service {#what-is-new-foundation}

* [Canal de pré-lançamento](/help/release-notes/prerelease.md): Visualize os recursos futuros por um mês inteiro antes de eles entrarem em produção!

* [Substituição da API](/help/release-notes/deprecated-apis.md): uma lista das APIs obsoletas mais recentes para AEM as a Cloud Service está disponível.

* [AEM Plug-in Maven do Analisador de Compilação do SDK as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR): Atualize seus projetos maven para a versão mais recente, que inclui uma verificação da API Java obsoleta e outras melhorias.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* Em breve você poderá verificar o conteúdo em um novo [Camada de visualização](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para simular a aparência da experiência final na camada Publicar . Isso é ativado pelo assistente de Publicação gerenciada do AEM Sites , que agora permite escolher um destino de publicação entre Publicar ou Visualizar. As experiências na Visualização podem ser acessadas por um URL dedicado. Após a validação em Visualizar, o conteúdo pode ser publicado de Autor para Publicar como de costume. Habilitar o Serviço de visualização em AEM ambientes as a Cloud Service será implementado gradualmente nas próximas semanas.

## [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* Você pode baixar os ativos compartilhados usando a funcionalidade Compartilhamento de links . Esse download agora usa um serviço assíncrono que oferece downloads mais rápidos e ininterruptos, mesmo para downloads muito grandes. Consulte [baixar ativos](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Baixar caixa de entrada](/help/assets/assets/download-inbox.png)

### Novos recursos disponíveis no canal de pré-lançamento {#what-is-new-assets-prerelease}

* Os esquemas de metadados podem ser aplicados diretamente às propriedades da pasta.

   ![Adicionar esquema de metadados das propriedades da pasta](/help/assets/assets/metadata-schema-folder-properties.png)

* A ferramenta Ingestor em massa de ativos permite adicionar metadados durante uma assimilação em massa.

* As melhorias na experiência do usuário exibem o número de ativos presentes em uma pasta. Para mais de 1000 ativos em uma pasta, [!DNL Assets] exibe 1000+.

   ![O número de ativos em uma pasta é exibido na interface](/help/assets/assets/browse-folder-number-of-assets.png)

### Erros corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* O upload de arquivos muito grandes interrompe o [!DNL Experience Manager desktop app]. (CQ-4320942)
* As opções da barra de ferramentas são diferentes quando a mesma Coleção é selecionada de uma pasta e quando é selecionada de um resultado de pesquisa. (CQ-4321406)

#### Novidades no Dynamic Media {#what-is-new-dm}

* O Smart Imaging DPR (Device Pixel Ratio) e a otimização da largura de banda da rede permitem fornecer imagens de melhor qualidade com eficiência, em dispositivos com telas de alta resolução e largura de banda de rede restrita. Para obter mais informações, consulte [Perguntas frequentes sobre imagens inteligentes](/help/assets/dynamic-media/imaging-faq.md) e [Otimização de imagem com formatos de imagem da próxima geração, WebP e AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* Introdução do suporte para AVIF na próxima geração do formato de imagem na entrega do Dynamic Media (modificador de URL fmt).

## [!DNL Adobe Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Ajuda contextual**: Adição de ajuda contextual para o editor de formulários adaptáveis, editor de modelos e editor de temas para ajudar os autores a entender melhor vários recursos dos editores.
* **Mensagens de erro no navegador Propriedades**: Adicionadas mensagens de erro para cada propriedade no navegador Adaptive Forms Properties. Essas mensagens ajudam a entender os valores permitidos para um campo.

### Futuro recurso beta de [!DNL Forms] {#what-is-new-forms-prerelease}

Saída como um serviço da nuvem: O serviço de saída ajuda a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos no modo de lote síncrono e assíncrono. O serviço de saída permite criar aplicativos que permitem:

* Gere documentos de formulário finais preenchendo arquivos de modelo com dados XML.
* Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
* Gerar PDFs de impressão a partir de PDFs de formulário XFA.

Você pode gravar em formscsbeta@adobe.com para se inscrever no programa beta.

### Erros corrigidos em [!DNL Forms] {#forms-bugs-fixed}

* Em uma etapa Atribuir tarefa dos fluxos de trabalho do AEM Forms, ao substituir o ícone padrão dos botões de ação por um ícone de coral, o fluxo de trabalho para de funcionar e registra uma exceção. O fluxo de trabalho é executado conforme esperado quando os ícones padrão são usados.
* Na camada de layout, ao alterar o número de colunas, abrir a camada de edição e arrastar alguns componentes em um painel, caixas azuis quadradas começam a aparecer na área de conteúdo do editor de formulários adaptáveis e o editor fica sem resposta.
* A mensagem de erro de uma opção do editor de regras relacionada ao fornecimento de URL de um ativo adaptável ou externo é muito longa e não é amigável para o usuário.


## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.5.0.

### Data de lançamento {#release-date-cm-may}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.5.0 é 6 de maio de 2021.
A próxima versão está planejada para 3 de junho de 2021.

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

* Em vez de remover variáveis &quot;excluídas&quot;, a API de variáveis de pipelines somente as marcaria com status **EXCLUÍDO**.

* Alguns problemas de qualidade do tipo Código Smell estavam afetando incorretamente a Classificação de confiabilidade.

* Como domínios curingas não são compatíveis, a interface do usuário não permitirá que o usuário envie um domínio curinga.

* Quando uma execução de pipeline era iniciada entre meia-noite e 1h UTC, a versão de artefato gerada pelo Cloud Manager não tinha garantia de ser maior do que uma versão criada no dia anterior.

* Durante a configuração do programa de sandbox, depois que o projeto com código de amostra for criado com êxito, o Gerenciar Git será exibido como um link do cartão herói na página Visão geral .

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.4.6 é 27 de maio de 2021.

### Novidades {#what-is-new-ctt-latest}

* Uma nova instrução de log foi adicionada ao log de erros do início rápido, se o usuário não tiver permissão de execução no executável Java.

* Quando um usuário exclui um conjunto de migração da interface do usuário da CTT, onde uma extração foi executada, a variável `tmp` a pasta associada a esse conjunto de migração será excluída para economizar espaço.

### Correções de erros {#bug-fixes-ctt-latest}

* Ao excluir um conjunto de migração, ocasionalmente, uma mensagem de erro inútil apareceria na interface do usuário da CTT. Isso foi corrigido.

* Durante a execução do Mapeamento de usuários, se os usuários tivessem o mesmo endereço de email no destino e no host, mas nomes de usuários diferentes, a assimilação inteira falharia. Isso foi corrigido. Nesse cenário conflitante, o usuário/grupo é ignorado e registrado como um conflito no arquivo de log.

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.4.0 é 11 de maio de 2021.

### Novidades {#what-is-new-ctt-may}

* Essa versão da ferramenta Transferência de conteúdo cria representações de texto para ativos que estão sendo migrados para o Cloud Service. As representações de texto são necessárias para suportar a pesquisa de texto completo em ativos assimilados.
* O número máximo de conjuntos de migração da ferramenta Transferência de conteúdo que um usuário pode criar foi aumentado de 4 para 10.

### Correções de erros {#bug-fixes-ctt-may}

* Várias correções de erros relacionadas ao recurso de atualização automática na interface do usuário da ferramenta Transferência de conteúdo .
* Ferramenta Transferência de conteúdo com `wipe=true` resultava em índice de contador incorreto no target. Isso foi corrigido.

## Suplemento comercial {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Suporte à paginação para conteúdo associado nas propriedades do console do produto

### Correções de erros {#bug-fixes-commerce}

* Miniaturas de ativos não exibidas na guia Ativo das propriedades do produto

* A navegação estrutural redefine os dados de visualização no console do produto
