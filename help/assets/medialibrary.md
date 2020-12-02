---
title: AEM Assets vs. AEM MediaLibrary
description: Perguntas frequentes sobre a AEM Assets e a. AEM Biblioteca de mídia, incluindo diferenças entre os dois.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 3%

---


# Perguntas frequentes sobre a AEM Assets versus AEM MediaLibrary {#aem-assets-vs-aem-medialibrary}

O Adobe Experience Manager (AEM) Assets é parte integrante da plataforma AEM. Essa integração suave é considerada uma grande vantagem da AEM e garante consistência na gestão de conteúdo e alta produtividade para os autores de conteúdo.

## O que é o AEM Assets? {#what-is-aem-assets}

O AEM Assets é um aplicativo da plataforma AEM que permite que nossos clientes gerenciem seus ativos digitais (imagens, vídeos, documentos e clipes de áudio) em um repositório baseado na Web. A AEM Assets inclui suporte a metadados, execuções, o Digital Asset Management Finder e administração por meio da interface do usuário.

## O que é a Biblioteca de mídia AEM? {#what-is-the-aem-media-library}

A Biblioteca de mídia AEM é uma parte designada do repositório de conteúdo AEM WCM, onde as imagens e outros recursos compartilhados são armazenados. A Biblioteca de mídia usa os recursos de Gerenciamento de ativos digitais AEM WCM.

## O que eu recebo da AEM Assets que não faz parte AEM WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Os recursos exclusivos que estão disponíveis somente para clientes da AEM Assets são:

1. a capacidade de extrair e editar metadados diferentes de título, tags e descrição.
1. o AEM Assets Admin, disponível na tela de boas-vindas, clicando no segundo botão ao lado do siteadmin.
1. Todas as etapas do fluxo de trabalho relacionadas ao Gerenciamento de ativos digitais, nomeadamente AEM Assets Ingestion, AEM Assets Deletion, AEM Assets Sub-Asset-Handling, extração de metadados AEM Assets.
1. bibliotecas incluindo o espaço do pacote &quot;dam&quot; im.

O uso desses recursos requer uma licença válida do AEM Assets.

## A AEM Assets está disponível como um pacote separado? {#is-aem-assets-available-as-a-separate-package}

Não. Para facilitar a instalação e a implantação, todos os aplicativos e complementos AEM são fornecidos em um único pacote com todas as funcionalidades incluídas. Isso não implica que você tenha permissão para usar todos os recursos do pacote.

## Quero editar metadados de ativos digitais. Preciso de AEM Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Se você estiver planejando editar metadados diferentes de título, descrição e tags, é necessário licenciar a AEM Assets.

## Quero usar o predicado de categoria no meu site. Preciso de AEM Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sim, o predicado de categoria, juntamente com todos os outros componentes usados no Geometrixx Press Center, fazem parte da AEM Assets e exigem uma licença da AEM Assets.

## Desejo redimensionar automaticamente as imagens após a importação. Preciso de AEM Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Sim. O redimensionamento de imagens e a transformação automática orientada por fluxo de trabalho, bem como a capacidade de gerenciar execuções, fazem parte do AEM Assets e exigem uma licença da AEM Assets.

## Desejo redimensionar imagens usando um componente de imagem personalizado. Preciso de AEM Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

O componente de imagem faz parte AEM WCM. A biblioteca de gráficos que está sendo usada pelo componente de imagem (mas também pela AEM Assets) faz parte da plataforma AEM e não exige uma licença da AEM Assets.

## Como posso impedir que meus usuários usem o AEM Assets se eu não licenciei o AEM Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Você pode remover todos os workflows, componentes, taxonomias, opções e o administrador da AEM Assets específicos da AEM Assets da AEM. Isso impede que os usuários usem acidentalmente recursos do AEM Assets que você não licenciou.

## Quero adicionar imagens a uma página e cortar e redimensionar essas imagens. Preciso de AEM Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Nesse caso de uso, não é necessário comprar o AEM Assets, nem mesmo o uso da Biblioteca de mídia é necessário para usar imagens em um site, já que o componente de imagem inteligente permite o upload de imagens diretamente na página.

## Uma lista detalhada dos recursos disponíveis no AEM Assets vs Media Library {#listoffeatures}

**Ativos AEM**

* Coleções e lightbox
* Propriedades e gerenciamento de metadados avançados
* Link do ativo do Adobe (conecte-se ao Creative Cloud para empresas)
* Aplicativo de desktop do AEM
* Processamento de perfis
* Integração do servidor InDesign
* Modelos de ativos e estrutura de produtores de catálogos
* Ativos vinculados ao Adobe Photoshop, Illustrator e InDesign
* Gerenciamento de ativos multilíngues
* Integração de PIM
* Rights Management
* Suporte Camera Raw
* Gerenciamento e configuração de aspectos de pesquisa
* Workflows DAM pré-criados (por exemplo, fotografar)
* Relatórios de ativos e Analytics: Insights de ativos
* Gerenciamento de ativos 3D
* Connected Assets
* Brand Portal
* Acesso a autoatendimento
* Procurar, Pesquisar e Baixar
* Coleções e compartilhamento de pasta
* Ferramentas administrativas
* Tags inteligentes
* Pesquisa visual
* Interface do usuário do administrador de ativos

**Biblioteca de mídia**

* Propriedades básicas de metadados
* Gerenciamento de tags
* Controle da versão
* Representações estáticas
* Projetos, Tarefas, Criação de fluxo de trabalho
* Fluxo de atividade (linha do tempo)
* Construtor de query (API)
* Integração de Marketing Cloud
* Personalização e extensão da interface do usuário
* Comentários e anotações