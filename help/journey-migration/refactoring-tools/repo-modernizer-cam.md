---
title: Modernizador de repositório (CAM)
description: Saiba como reestruturar pacotes de projetos existentes e torná-los compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.
feature: Migration
role: Admin
source-git-commit: 317ee65786d48d7b92d95c7c6b8782f617d6e346
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 2%

---


# Modernizador de repositório (CAM) {#repo-modernizer-cam}

O Repository Modernizer é um utilitário desenvolvido para reestruturar pacotes de projetos existentes separando o conteúdo e o código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager as a Cloud Service traz muitos novos recursos e possibilidades para seus Projetos AEM. No entanto, algumas alterações são necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um alto nível, o AEM requer uma separação de **conteúdo** e **código** em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Consulte [Estrutura de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) para obter mais detalhes sobre a nova estrutura de projeto do AEM para o Cloud Service.

O Repository Modernizer cria uma estrutura de projeto compatível do AEM Cloud Service ao criar a seguinte estrutura de implantação:

- O pacote `ui.apps` é implantado em `/apps` e contém todo o código

- O pacote `ui.content` é implantado em áreas graváveis em tempo de execução (por exemplo, `/content`, `/conf`, `/home` ou qualquer coisa que não seja `/apps`) e contém todo o conteúdo e configuração.

- O pacote `all` é um pacote de contêiner que contém os subpacotes `ui.apps` e `ui.content`.

>[!NOTE]
>
> A estrutura do Projeto é baseada no _Arquétipo 48_ para pacotes e seus `pom.xml/filter.xml files`. Consulte [Arquétipo 48](https://github.com/adobe/aem-project-archetype) para obter mais detalhes.

O Modernizador de repositório agora também é compatível com os seguintes tipos de projeto:

- **MULTI_PROJECT**: representa um projeto de vários módulos sem POM pai, dispatcher e todos os módulos comuns.
- **SINGLE_PROJECT**: representa um único projeto.
- **NESTED_PROJECT**: representa um projeto de vários módulos com um POM pai, um Dispatcher e todos os módulos comuns.
- **MONOLITHIC_PROJECT**: representa um projeto principal com um ou mais subprojetos.

## Uso do Modernizador de repositório {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

- O Modernizador do repositório agora é chamado automaticamente pelo Serviço de refatoração na guia Trabalho de refatoração. Os clientes só precisam fazer upload do projeto e acionar o trabalho de refatoração, não é necessária nenhuma configuração adicional.

## Referência do código de erro

Se você encontrar um código de erro ao usar o Repository Modernizer, consulte a tabela abaixo para obter detalhes e ações recomendadas.

| Código de erro | Mensagem | Descrição | Ação do usuário necessária? |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| RM-100 | Erro ao converter o arquivo de configuração OSGi {0} no formato .cfg.json. Valide o arquivo de configuração existente antes de tentar novamente. | Esse erro ocorre quando há um problema durante a transformação de um arquivo de configuração OSGi para o formato .cfg.json. | Sim |
| RM-101 | Erro ao tentar copiar o conteúdo de: {0} | Esse erro ocorre quando há uma falha ao tentar copiar o conteúdo da origem especificada. | Não |
| RM-102 | Erro ao tentar mover o arquivo {0} de {1} para {2}. | Esse erro ocorre quando há um problema ao mover um arquivo de um local para outro. | Não |
| RM-103 | O caminho fornecido não pôde ser resolvido para um arquivo válido: {0} | Este erro ocorre quando o arquivo não é encontrado no local determinado. | Não |
| RM-104 | Erro ao iterar sobre o conteúdo de {0}. | Esse erro ocorre durante a travessia de arquivos ou diretórios, indicando um problema de acesso ou processamento de conteúdo. | Não |
| RM-105 | Erro ao tentar analisar o arquivo XML: {0}. Valide o arquivo XML antes de tentar novamente. | Esse erro ocorre quando há uma falha na análise do arquivo XML. | Sim |
| RM-106 | Erro ao gravar no arquivo XML: {0}. | Esse erro ocorre quando há um problema ao gravar no arquivo XML. | Não |
| RM-107 | Nenhum pacote de conteúdo encontrado no projeto existente: {0}. Valide se o projeto correto foi carregado. | Esse erro indica que nenhum pacote de conteúdo foi encontrado no projeto existente. | Sim |
| RM-108 | Arquivo POM não encontrado no caminho esperado: {0}. Espera-se que o arquivo POM do projeto ou módulo esteja localizado diretamente em seu diretório como um arquivo filho. | Esse erro ocorre quando o arquivo POM não é encontrado no local esperado. | Sim |
| RM-109 | Erro ao tentar analisar o arquivo pom.xml: {0}. Valide o arquivo pom antes de tentar novamente. | Esse erro ocorre quando há um problema ao analisar o arquivo pom.xml. | Sim |
| RM-110 | Erro ao gravar no arquivo pom.xml: {0}. | Esse erro ocorre quando há um problema ao gravar no arquivo pom. | Não |
| RM-111 | Erro ao gravar no arquivo de relatório. | Esse erro ocorre quando há uma falha durante o processo de gravação no arquivo de relatório. | Não |
| RM-112 | Não foi possível encontrar {0} no arquivo pom da estrutura do repositório em ({1}) | Esse erro ocorre quando a configuração esperada não é encontrada no modelo de arquétipo de projeto do AEM. | Não |
| RM-113 | Erro ao tentar copiar os modelos do Arquétipo de projeto do AEM para o destino. | Esse erro ocorre quando há um problema ao copiar os modelos do Arquétipo de projeto do AEM para o destino. | Não |
| RM-115 | Erro ao tentar se conectar ao Armazenamento de Blobs do Azure. | Esse erro ocorre quando há um problema de conexão com o Armazenamento de Blobs do Azure. | Não |
| RM-116 | Erro ao tentar carregar o arquivo: {0} para o Armazenamento Azure Blob. | Esse erro ocorre quando há um problema ao fazer upload de um arquivo para o Armazenamento de blobs do Azure. | Não |
| RM-117 | Erro ao tentar baixar o arquivo: {0} do Armazenamento de Blobs do Azure. | Esse erro ocorre quando há um problema ao baixar um arquivo do Armazenamento de blobs do Azure. | Não |
| RM-118 | Erro de E/S ao manipular : {0}. | Esse erro ocorre quando há um problema ao ler ou gravar em um arquivo de projeto. | Não |
| RM-119 | Erro de E/S ao tentar arquivar os resultados para upload no Azure. | Esse erro ocorre quando há um erro ao arquivar os resultados gerados pelo processo. | Não |
| RM-120 | Erro de E/S ao tentar desarquivar o zip do projeto fornecido. Verifique se o zip do projeto fornecido é válido. | Esse erro ocorre quando ocorre um erro ao desarquivar o projeto do cliente fornecido. | Sim |
| RM-121 | Erro ao gravar no arquivo de configuração. | Esse erro ocorre quando há uma falha durante o processo de gravação no arquivo de configuração. | Não |
| RM-122 | Tipo de solicitação incompatível: {0}. | Esse erro ocorre quando o sistema não oferece suporte ao tipo de solicitação. Verifique o tipo de solicitação e tente novamente. | Não |

## Noções básicas sobre as prioridades do relatório de resultados

Ao baixar o relatório de descobertas gerado pela ferramenta Repository Modernizer, cada descoberta recebe uma **prioridade**. Essas prioridades ajudam você a entender a urgência e o impacto de cada problema:

| Prioridade | Descrição |
| -------- | ----------------------------------------------------------------------------------------------- |
| CRÍTICO | Deve ser resolvido para a compilação bem-sucedida do projeto. |
| ALTA | Deve ser resolvido para garantir que a funcionalidade não seja quebrada no AEM. |
| NORMAL | Deve ser resolvido para garantir a sanidade e integridade geral da modernização. |
| BAIXA | Para verificação manual; essas descobertas são informativas e podem não exigir ação imediata. |

>[!NOTE]
> 
>É recomendável abordar as descobertas de prioridade mais alta primeiro para garantir um processo perfeito de modernização e implantação.
