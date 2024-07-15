---
title: Como podemos sincronizar o Adaptive Forms com modelos de formulário XFA?
description: Sincronização do Adaptive Forms com arquivos XFA/XDP.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# Sincronização do Adaptive Forms com modelos de formulário XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introdução {#introduction}

Você pode criar um Formulário adaptável com base em um modelo de formulário XFA (arquivo `*.XDP`). Essa reutilização permite que você preserve seu investimento em formulários XFA existentes. Para obter informações sobre como usar um modelo de formulário XFA para criar um Formulário adaptável, [Crie um Formulário adaptável com base em um modelo](creating-adaptive-form.md).

Você pode reutilizar campos do arquivo XDP no Formulário adaptável. Esses campos são chamados de campos vinculados. As propriedades dos campos vinculados (como scripts, rótulos e formato de exibição) são copiadas do arquivo XDP. Você também pode optar por substituir o valor de algumas dessas propriedades.

O [!DNL AEM Forms] fornece uma maneira de ajudá-lo a manter os campos do Forms adaptável sincronizados com quaisquer alterações feitas posteriormente nos campos correspondentes no arquivo XDP. Este artigo explica como você pode habilitar essa sincronização.

![Você pode arrastar campos de um formulário XFA para um Formulário adaptável](assets/drag-drop-xfa.gif.gif)

No ambiente de criação [!DNL AEM Forms], você pode arrastar campos de um formulário XFA (esquerda) para um formulário adaptável (direita)

## Pré-requisitos {#prerequisites}

Para usar as informações deste artigo, é recomendável estar familiarizado com as seguintes áreas:

* [Criação de um formulário adaptável](creating-adaptive-form.md)

* XFA (XML Forms Architecture, arquitetura XML do)

Para usar os ativos fornecidos para o exemplo no artigo, baixe o pacote de exemplo conforme explicado na próxima seção, [Pacote de exemplo](synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## Pacote de exemplo {#sample-package}

O artigo usa um exemplo para demonstrar como sincronizar o Formulário adaptável com um modelo de formulário XFA atualizado. Os ativos usados no exemplo estão disponíveis em um pacote, que pode ser baixado da seção [Downloads](synchronizing-adaptive-forms-xfa.md#p-downloads-p) deste artigo.

Depois de carregar o pacote, você pode exibir esses ativos na interface do usuário do [!DNL AEM Forms].

Instalar o pacote usando o gerenciador de pacotes: `https://<server>:<port>/crx/packmgr/index.jsp`

O pacote contém os seguintes ativos:

1. `sample-form.xdp`: o modelo de formulário XFA usado como exemplo

1. `sample-xfa-af`: o formulário adaptável baseado no arquivo sample-form.xdp. No entanto, esse Formulário adaptável não inclui campos. Na próxima etapa, adicionaremos conteúdo a este Formulário adaptável.

### Adicionar conteúdo ao formulário adaptável {#add-content-to-adaptive-form-br}

1. Navegue até https://&lt;server>:&lt;port>/aem/forms.html. Insira suas credenciais, se solicitado.
1. Abra o sample-af-xfa para edição no modo de autor.
1. No navegador Conteúdo da barra lateral, escolha a guia Objetos do modelo de dados. Arraste NumericField1 e TextField1 para o Formulário adaptável.
1. Altere o Título de NumericField1 de **Campo Numérico** para **Campo Numérico AF.**

>[!NOTE]
>
>Nas etapas anteriores, substituímos uma propriedade de um campo no arquivo XDP. Portanto, essa propriedade não será sincronizada se a propriedade correspondente no arquivo XDP for modificada posteriormente.

## Detecção de alterações no arquivo XDP {#detecting-changes-in-xdp-file}

Sempre que houver qualquer alteração em um arquivo XDP ou fragmento, a interface do usuário do [!DNL AEM Forms] sinalizará todos os Forms adaptáveis baseados no arquivo XDP ou no fragmento.

Depois de atualizar um arquivo XDP, é necessário carregá-lo novamente na interface do usuário do [!DNL AEM Forms] para que as alterações sejam sinalizadas.

Como exemplo, atualizemos o arquivo `sample-form.xdp` usando estas etapas:

1. Navegue até `https://<server>:<port>/projects.html.` Insira suas credenciais, se solicitado.
1. Clique na guia Forms à esquerda.
1. Baixe o arquivo `sample-form.xdp` no computador local. O arquivo XDP é baixado como um arquivo `.zip`, que pode ser extraído usando qualquer utilitário de descompactação de arquivo.

1. Abra o arquivo `sample-form.xdp` e altere o título do campo TextField1 de **Campo de Texto** para **Meu Campo de Texto**.

1. Carregue o arquivo `sample-form.xdp` de volta para a interface do usuário [!DNL AEM Forms].

Se um arquivo XDP for atualizado, você verá um ícone no editor ao editar o Forms adaptável com base no arquivo XDP. Esse ícone indica que o formulário adaptável está fora de sincronia com o arquivo XDP. Na imagem a seguir, veja o ícone ao lado na barra lateral.

![Ícone para mostrar que o Formulário Adaptável está fora de sincronia com o arquivo XDP](assets/sync-af-xfa.png)

## Sincronização do Adaptive Forms com o arquivo XDP mais recente {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Quando um Formulário adaptável que está fora de sincronia com o arquivo XDP for aberto para criação na próxima vez, a seguinte mensagem será exibida: **O Modelo de esquema/formulário para o Formulário adaptável foi atualizado. `Click Here` para trocar sua base pela nova versão.**

Clicar na mensagem sincroniza os campos no Formulário adaptável com os campos correspondentes no arquivo XDP.

Para o exemplo usado neste artigo, abra `sample-xfa-af` no modo de criação. A mensagem é exibida na parte inferior do Formulário adaptável.

![Mensagem solicitando que você sincronize o Formulário Adaptável com o arquivo XDP](assets/sync-af-xfa-1.png)

### Atualização das propriedades {#updating-the-properties}

Todas as propriedades que foram copiadas do arquivo XDP para o Formulário adaptável são atualizadas, exceto as propriedades que foram explicitamente substituídas no Formulário adaptável (da caixa de diálogo Componente) pelo Autor. A lista de propriedades que foram atualizadas está disponível nos logs do servidor.

Para atualizar as propriedades no exemplo de Formulário adaptável, clique no link (rotulado `"Click Here"`) na mensagem. O título de TextField1 é alterado de **Campo de Texto** para **Meu Campo de Texto**.

![propriedade-atualização](assets/update-property.png)

>[!NOTE]
>
>O campo numérico de AF do rótulo não foi alterado porque você substituiu esta propriedade na caixa de diálogo de propriedades do componente, conforme descrito em [Adicionar conteúdo ao Forms Adaptável](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### Adição de novos campos do arquivo XDP ao Formulário adaptável   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Todos os campos adicionados posteriormente ao arquivo XDP original aparecem na guia Hierarquia do formulário e você pode arrastar esses novos campos para o formulário adaptável.

Não é necessário clicar no link da mensagem de erro para atualizar os campos na guia Hierarquia do formulário.

### Campos excluídos no arquivo XDP {#deleted-fields-in-xdp-file}

Se um campo que foi copiado anteriormente para um formulário adaptável for excluído de um arquivo XDP, uma mensagem de erro será exibida no modo de criação informando que o campo não existe no arquivo XDP. Nesses casos, exclua manualmente o campo do Formulário adaptável ou limpe a propriedade `bindRef` na caixa de diálogo do componente.

As etapas a seguir ilustram esse fluxo de uso para os ativos no exemplo usado neste artigo:

1. Atualize o arquivo `sample-form.xdp` e exclua NumericField1.
1. Carregar o arquivo `sample-form.xdp` na interface do usuário [!DNL AEM Forms]
1. Abra o Formulário Adaptável do `sample-xfa-af` para criação. A seguinte mensagem de erro é exibida: O Modelo de esquema/formulário para o Formulário adaptável foi atualizado. `Click Here` para trocar sua base pela nova versão.

1. Clique no link (rotulado como &quot;`Click Here`&quot;) na mensagem. Uma mensagem de erro é exibida observando que o campo não existe mais no arquivo XDP.

![Erro exibido ao excluir um elemento do arquivo XDP](assets/no-element-xdp.png)

O campo que foi excluído também é marcado com um ícone para indicar um erro no campo.

![Ícone de erro no campo](assets/error-field.png)

>[!NOTE]
>
>Os campos no Formulário adaptável que têm uma associação incorreta (um valor `bindRef` inválido na caixa de diálogo de edição) também são considerados campos excluídos. Se o autor não corrigir esses erros e publicar o Formulário adaptável, o campo será tratado como um campo de Formulário adaptável desvinculado normal e será incluído na seção desvinculada do arquivo XML de saída.

## Downloads {#downloads}

Pacote de conteúdo para o exemplo neste artigo

[Obter arquivo](assets/sample-xfa-af-sync-1.0.zip)
