---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.5.0.
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 32%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] O as a Cloud Service 2021.5.0 é 27 de maio de 2021.
A versão seguinte (2021.6.0) será lançada em 28 de junho de 2021.

## Fundação as a Cloud Service AEM {#foundation}

### Novidades da Fundação AEM as a Cloud Service {#what-is-new-foundation}

* [Canal de pré-lançamento](/help/release-notes/prerelease.md): visualize os recursos futuros por um mês inteiro antes de eles entrarem em produção.

* [Descontinuação de API](/help/release-notes/deprecated-apis.md): uma lista das APIs obsoletas mais recentes para o AEM as a Cloud Service está disponível.

* [Plug-in Maven Analisador de build do SDK as a Cloud Service do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR): atualize os projetos maven para a versão mais recente, o que inclui uma verificação de API Java descontinuada e outras melhorias.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* Em breve, você poderá verificar o conteúdo em um novo [Camada de visualização](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para simular a aparência e a experiência finais como você faria na camada de Publicação. Isso é ativado pelo assistente de Publicação gerenciada do AEM Sites, que agora permite escolher um destino de publicação entre Publicar ou Pré-visualizar. As experiências na Pré-visualização podem ser acessadas por meio de um URL dedicado. Após a validação em Pré-visualizar, o conteúdo pode ser publicado de Autor para Publicar como de costume. A habilitação do serviço de Pré-visualização em ambientes as a Cloud Service AEM será liberada gradualmente nas próximas semanas.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

* É possível baixar os ativos compartilhados usando a funcionalidade Compartilhamento de link. Esse download agora usa um serviço assíncrono que oferece downloads mais rápidos e ininterruptos, mesmo para downloads muito grandes. Consulte [baixar ativos](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Baixar caixa de entrada](/help/assets/assets/download-inbox.png)

### Novos recursos disponíveis no canal de pré-lançamento {#what-is-new-assets-prerelease}

* Os esquemas de metadados podem ser aplicados diretamente às propriedades da pasta.

   ![Adicionar esquema de metadados das propriedades da pasta](/help/assets/assets/metadata-schema-folder-properties.png)

* A ferramenta Entrada de ativos em massa permite adicionar metadados durante uma entrada em massa.

* As melhorias na experiência do usuário exibem o número de ativos presentes em uma pasta. Para mais de 1000 ativos em uma pasta, [!DNL Assets] exibe mais de 1000.

   ![O número de ativos em uma pasta é exibido na interface](/help/assets/assets/browse-folder-number-of-assets.png)

### Bugs corrigidos em [!DNL Assets] {#assets-bugs-fixed}

* O upload de arquivos muito grandes trava o [!DNL Experience Manager desktop app]. (CQ-4320942)
* As opções da barra de ferramentas são diferentes quando a mesma coleção é selecionada em uma pasta e quando é selecionada em um resultado de pesquisa. (CQ-4321406)

#### Novidades do Dynamic Media {#what-is-new-dm}

* A DPR (Relação de pixels do dispositivo) da imagem inteligente e a otimização da largura de banda da rede permitem que você forneça imagens com mais eficiência, em dispositivos com telas de alta resolução e largura de banda de rede restrita. Para obter mais informações, consulte [Perguntas frequentes sobre imagens inteligentes](/help/assets/dynamic-media/imaging-faq.md) e [Otimização de imagem com formatos de imagem de próxima geração WebP e AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* Introdução do suporte para o formato de imagem AVIF de próxima geração na entrega do Dynamic Media (modificador de URL fmt).

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **Ajuda contextual**: adição de ajuda contextual para o editor de formulários adaptáveis, editor de modelo e editor de tema para ajudar os autores a entender melhor vários recursos dos editores.
* **Mensagens de erro no navegador de propriedades**: Adição de mensagens de erro para cada propriedade no navegador Propriedades adaptáveis do Forms. Essas mensagens ajudam a entender os valores permitidos para um campo.

### Futuro recurso beta do [!DNL Forms] {#what-is-new-forms-prerelease}

Output as a Cloud Service: o serviço de saída ajuda a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo de lote síncrono e assíncrono. O serviço de saída permite criar aplicativos que permitem:

* Gerar documentos de formulário final preenchendo arquivos de modelo com dados XML.
* Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
* Gerar PDFs de impressão a partir de PDFs de formulário XFA.

Você pode enviar um email a formscsbeta@adobe.com para se cadastrar no programa beta.

### Bugs corrigidos em [!DNL Forms] {#forms-bugs-fixed}

* Em uma etapa Atribuir tarefa de fluxos de trabalho do AEM Forms, ao substituir o ícone padrão dos botões de ação por um ícone de coral, o fluxo de trabalho para de funcionar e registra uma exceção. O fluxo de trabalho é executado conforme esperado quando os ícones padrão são usados.
* Na camada de layout, ao alterar o número de colunas, abrir a camada de edição e arrastar alguns componentes em um painel, caixas azuis quadradas começam a aparecer na área de conteúdo do editor de formulários adaptáveis e o editor fica sem resposta.
* A mensagem de erro de uma opção do editor de regras relacionada ao fornecimento de URL de um ativo adaptável ou externo é muito longa e não é amigável.


## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.5.0.

### Data de lançamento {#release-date-cm-may}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.5.0 é 6 de maio de 2021.
A próxima versão está planejada para 03 de junho de 2021.

### Novidades {#what-is-new-may}

* A regra de qualidade PackageOverlaps agora detecta casos em que o mesmo pacote era implantado várias vezes, ou seja, em vários locais incorporados, no mesmo conjunto de pacotes implantados.

* O endpoint do repositório na API pública agora inclui a URL do Git.

* O log de implantação baixado por um usuário do Cloud Manager será mais revelador e incluirá detalhes sobre falhas e cenários de sucesso.

* As falhas intermitentes encontradas ao enviar o código para o Git da Adobe foram resolvidas.

* O complemento de comércio agora pode ser aplicado a programas de sandbox durante o fluxo de trabalho Editar programa.

* A experiência Editar programa foi atualizada.

* A tabela de Nomes de domínio na página Detalhes do ambiente exibirá até 250 nomes de Domínio por página.

* A guia Soluções nos workflows Adicionar programa e Editar programa exibirá a solução, mesmo se apenas uma solução estiver disponível para o Programa.

* A mensagem de erro no log de etapas de compilação quando a compilação não produzia nenhum pacote de conteúdo implantado não era clara.

### Correções de erros {#bug-fixes-cm-may}

* Ocasionalmente, o usuário pode ver um status verde “ativo” ao lado de uma Lista de permissões de IP, mesmo quando essa configuração não foi implantada.

* Em vez de remover variáveis “excluídas”, a API de variáveis de pipelines somente as marcava com o status **EXCLUÍDO**.

* Alguns problemas de qualidade do tipo Code Smell afetavam incorretamente a avaliação de confiabilidade.

* Como não há suporte a domínios curingas, a interface do usuário não permitirá que o usuário envie um domínio curinga.

* Quando uma execução de pipeline era iniciada entre meia-noite e 1h (UTC), não havia garantia de que a versão de artefato gerada pelo Cloud Manager seria maior do que uma versão criada no dia anterior.

* Durante a configuração do programa de sandbox, depois que o projeto com código de amostra fosse criado com sucesso, a opção Gerenciar Git apareceria como um link do cartão hore na página Visão geral.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A data de lançamento da ferramenta de transferência de conteúdo v1.4.6 é 27 de maio de 2021.

### Novidades {#what-is-new-ctt-latest}

* Uma nova instrução de registro foi adicionada ao registro de erros do início rápido se o usuário não tiver permissão de execução no executável Java.

* Quando um usuário exclui um conjunto de migração da interface da CTT, onde uma extração foi executada, a variável `tmp` a pasta associada a esse conjunto de migração será excluída para economizar espaço.

### Correções de erros {#bug-fixes-ctt-latest}

* Ao excluir um conjunto de migração, ocasionalmente uma mensagem de erro inútil era exibida na interface da CTT. Isso foi corrigido.

* Ao executar o mapeamento de usuários, se os usuários tivessem o mesmo endereço de email no destino e no host, mas nomes de usuário diferentes, a assimilação inteira falharia. Isso foi corrigido. Nesse cenário conflitante, o usuário/grupo é ignorado e registrado como um conflito no arquivo de log.

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.4.0 é 11 de maio de 2021.

### Novidades {#what-is-new-ctt-may}

* Essa versão da ferramenta Transferência de conteúdo cria representações de texto para ativos que estão sendo migrados para o Cloud Service. As representações de texto são necessárias para oferecer suporte à pesquisa de texto completo em ativos assimilados.
* O número máximo de conjuntos de migração da ferramenta Transferência de conteúdo que um usuário pode criar aumentou de 4 para 10.

### Correções de erros {#bug-fixes-ctt-may}

* Várias correções de erros relacionadas ao recurso de atualização automática na interface do usuário da ferramenta Transferência de conteúdo.
* Ferramenta Transferência de conteúdo com `wipe=true` resultou em índice de contador incorreto no destino. Isso foi corrigido.

## Complemento do Commerce {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Suporte à paginação para conteúdo associado nas propriedades do console do produto

### Correções de erros {#bug-fixes-commerce}

* As miniaturas de ativos não são exibidas na guia Ativo das propriedades do produto

* A navegação estrutural redefine os dados de visualização no console do produto
