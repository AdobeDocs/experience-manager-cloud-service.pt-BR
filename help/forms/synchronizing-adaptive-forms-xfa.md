---
title: Sincronização do Adaptive Forms com modelos de formulário XFA
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: Sincronização do Adaptive Forms com arquivos XFA/XDP.
seo-description: Synchronizing Adaptive Forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# Sincronização do Adaptive Forms com modelos de formulário XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introdução {#introduction}

É possível criar um formulário adaptável com base em um modelo de formulário XFA ( `*.XDP` arquivo ). Essa reutilização permite preservar seu investimento em formulários XFA existentes. Para obter informações sobre como usar um modelo de formulário XFA para criar um formulário adaptável, [Criar um formulário adaptável com base em um modelo](creating-adaptive-form.md).

Você pode reutilizar campos do arquivo XDP em seu formulário adaptável. Esses campos são chamados de campos vinculados. As propriedades dos campos vinculados (como scripts, rótulos e formato de exibição) são copiadas do arquivo XDP. Também é possível optar por substituir o valor de algumas dessas propriedades.

[!DNL AEM Forms] fornece uma maneira de ajudar a manter os campos do Adaptive Forms sincronizados com qualquer alteração feita posteriormente nos campos correspondentes no arquivo XDP. Este artigo explica como você pode habilitar essa sincronização.

![Você pode arrastar campos de um formulário XFA para um formulário adaptável](assets/drag-drop-xfa.gif.gif)

No [!DNL AEM Forms] ambiente de criação, é possível arrastar campos de um formulário XFA (à esquerda) para um formulário adaptável (à direita)

## Pré-requisitos {#prerequisites}

Para usar as informações neste artigo, recomenda-se uma familiaridade com as seguintes áreas:

* [Criação de um formulário adaptável](creating-adaptive-form.md)

* XFA (Arquitetura Forms XML)

Para usar os ativos, forneça o exemplo no artigo, baixe o pacote de amostra conforme explicado na próxima seção, [Pacote de exemplo](synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## Pacote de exemplo {#sample-package}

O artigo usa um exemplo para demonstrar como sincronizar o formulário adaptável com um modelo de formulário XFA atualizado. Os ativos usados no exemplo estão disponíveis em um pacote, que pode ser baixado do [Downloads](synchronizing-adaptive-forms-xfa.md#p-downloads-p) neste artigo.

Após fazer upload do pacote, você pode exibir esses ativos na [!DNL AEM Forms] IU.

Instale o pacote usando o gerenciador de pacotes: `https://<server>:<port>/crx/packmgr/index.jsp`

O pacote contém os seguintes ativos:

1. `sample-form.xdp`: O modelo de formulário XFA usado como exemplo

1. `sample-xfa-af`: O formulário adaptável com base no arquivo sample-form.xdp . No entanto, esse formulário adaptável não inclui campos. Na próxima etapa, adicionaremos conteúdo a esse formulário adaptável.

### Adicionar conteúdo ao formulário adaptável {#add-content-to-adaptive-form-br}

1. Navegue até https://&lt;server>:&lt;port>/aem/forms.html. Insira suas credenciais, se solicitado.
1. Abra o sample-af-xfa para edição no modo de autor.
1. No navegador Conteúdo na barra lateral, escolha a guia Objetos do modelo de dados . Arraste NumericField1 e TextField1 para o Formulário adaptável.
1. Altere o Título de NumericField1 de **Campo numérico** para **Campo numérico AF.**

>[!NOTE]
>
>Nas etapas anteriores, substituímos uma propriedade de um campo no arquivo XDP. Portanto, essa propriedade não será sincronizada se a propriedade correspondente no arquivo XDP for modificada posteriormente.

## Detecção de alterações no arquivo XDP {#detecting-changes-in-xdp-file}

Sempre que houver qualquer alteração em um arquivo XDP ou em um fragmento, a variável [!DNL AEM Forms] A interface do usuário sinaliza todos os Forms adaptáveis baseados no arquivo XDP ou no fragmento.

Após atualizar um arquivo XDP, é necessário fazer upload dele novamente no [!DNL AEM Forms] Interface do usuário para as alterações serem sinalizadas.

Como exemplo, atualizemos o `sample-form.xdp` arquivo usando as seguintes etapas:

1. Navegar para `https://<server>:<port>/projects.html.` Insira suas credenciais, se solicitado.
1. Clique na guia Forms à esquerda.
1. Baixe o `sample-form.xdp` no computador local. O arquivo XDP é baixado como um `.zip` arquivo , que pode ser extraído usando qualquer utilitário de descompactação de arquivo.

1. Abra o `sample-form.xdp` e altere o título do campo TextField1 de **Campo de texto** para **Meu campo de texto**.

1. Faça upload do `sample-form.xdp` retorne ao [!DNL AEM Forms] IU.

Se um arquivo XDP for atualizado, você verá um ícone no editor, ao editar o Adaptive Forms com base no arquivo XDP. Esse ícone indica que o formulário adaptável está fora de sincronia com o arquivo XDP. Na imagem a seguir, veja o ícone ao lado da barra lateral.

![Ícone para exibir se o formulário adaptável está fora de sincronia com o arquivo XDP](assets/sync-af-xfa.png)

## Sincronização do Adaptive Forms com o arquivo XDP mais recente {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Quando um formulário adaptável fora de sincronia com o arquivo XDP for aberto para criação na próxima vez, a seguinte mensagem será exibida: **O esquema/modelo de formulário para o formulário adaptável foi atualizado. `Click Here` para recalcular com a nova versão.**

Clicar na mensagem sincroniza os campos no Formulário adaptável com os campos correspondentes no arquivo XDP.

Para o exemplo usado neste artigo, abra `sample-xfa-af` no modo de criação. A mensagem é exibida na parte inferior do formulário adaptável.

![Mensagem solicitando a sincronização do formulário adaptável com o arquivo XDP](assets/sync-af-xfa-1.png)

### Atualização das propriedades {#updating-the-properties}

Todas as propriedades que foram copiadas do arquivo XDP para o Formulário adaptável são atualizadas, exceto pelas propriedades que foram explicitamente substituídas no Formulário adaptável (na caixa de diálogo Componente) pelo autor. A lista de propriedades que foram atualizadas está disponível nos logs do servidor.

Para atualizar as propriedades no exemplo do formulário adaptável, clique no link (rotulado como `"Click Here"`) na mensagem. O título do TextField1 muda de **Campo de texto** para **Meu campo de texto**.

![update-property](assets/update-property.png)

>[!NOTE]
>
>O rótulo Campo numérico AF não foi alterado porque você substituiu essa propriedade da caixa de diálogo de propriedades do componente, conforme descrito em [Adicionar conteúdo ao Adaptive Forms](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### Adicionar novos campos do arquivo XDP ao formulário adaptável   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Todos os campos adicionados posteriormente ao arquivo XDP original serão exibidos na guia Hierarquia de formulário e você poderá arrastar esses novos campos para o Formulário adaptável.

Não é necessário clicar no link da mensagem de erro para atualizar os campos na guia Hierarquia de formulário.

### Campos excluídos no arquivo XDP {#deleted-fields-in-xdp-file}

Se um campo que foi copiado anteriormente para um formulário adaptável for excluído de um arquivo XDP, uma mensagem de erro será exibida no modo de criação declarando que o campo não existe no arquivo XDP. Nesses casos, exclua manualmente o campo do Formulário adaptável ou limpe o `bindRef` na caixa de diálogo do componente.

As etapas a seguir ilustram esse fluxo de uso para os ativos no exemplo usado neste artigo:

1. Atualize o `sample-form.xdp` e exclua NumericField1.
1. Faça upload do `sample-form.xdp` no [!DNL AEM Forms] interface
1. Abra o `sample-xfa-af` Formulário adaptável para criação. A seguinte mensagem de erro é exibida: O esquema/modelo de formulário para o formulário adaptável foi atualizado. `Click Here` para recalcular com a nova versão.

1. Clique no link (rotulado como &quot; `Click Here`&quot;) na mensagem. Uma mensagem de erro é exibida, observando que o campo não existe mais no arquivo XDP.

![Erro que você vê ao excluir um elemento no arquivo XDP](assets/no-element-xdp.png)

O campo que foi excluído também é marcado com um ícone para indicar um erro no campo.

![Ícone Error no campo](assets/error-field.png)

>[!NOTE]
>
>Os campos no Formulário adaptável que têm um vínculo incorreto (um `bindRef` na caixa de diálogo de edição) também são considerados campos excluídos. Se o autor não corrigir esses erros e publicar o Formulário adaptativo, o campo será tratado como um campo de Formulário adaptável normal não vinculado e será incluído na seção não vinculada do arquivo XML de saída.

## Downloads {#downloads}

Pacote de conteúdo para o exemplo deste artigo

[Obter arquivo](assets/sample-xfa-af-sync-1.0.zip)
