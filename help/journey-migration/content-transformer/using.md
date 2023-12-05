---
title: Usar o transformador de conteúdo
description: Saiba como transformar sua estrutura de conteúdo em preparação para migrar para o AEM as a Cloud Service.
exl-id: 40516ff7-5686-42e6-bdd1-c9c6de432b09
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Usar o transformador de conteúdo {#using-ct}

## Considerações importantes sobre o uso do transformador de conteúdo {#imp-considerations-ct}

Siga a seção abaixo para entender as considerações importantes sobre o uso do transformador de conteúdo (CT):

* Para usar o transformador de conteúdo, primeiro você deve executar o Analisador de práticas recomendadas no ambiente do Adobe Experience Manager (AEM).
* Embora seja possível executar o transformador de conteúdo no ambiente de produção, é recomendável executar o transformador de conteúdo em um clone do ambiente de produção. Mais importante, você precisa garantir que o BPA e a CT sejam executados no mesmo ambiente.
* Você precisa ser um administrador no ambiente em que deseja executar o transformador de conteúdo.
* Qualquer operação que possa alterar o conteúdo de origem ( mover/remover/renomear ) criará por padrão um pacote de backup dos caminhos de origem em `/etc/packages/content-transformation` antes da transformação. Embora cada caixa de diálogo de operação tenha uma opção para desabilitar/habilitar a criação de pacote de backup, é estritamente recomendável ter sempre a opção habilitar criação de pacote selecionada.
* Cada página no Transformador de conteúdo é configurada para listar no máximo 50 descobertas, portanto, por vez, um máximo de 50 descobertas podem ser transformadas. Isso é feito para fornecer uma resposta de prontidão na interface do usuário.

## Disponibilidade {#availability-ct}

O transformador de conteúdo é fornecido com o [Ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) que pode ser baixado como um arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na instância AEM de origem.

>[!NOTE]
>O Transformador de conteúdo está disponível com a Ferramenta de transferência de conteúdo v2.0.20 ou superior.

## Abrir o transformador de conteúdo {#opening-ct}

1. Faça logon na instância de AEM de origem como administrador e acesse a página inicial: https://host:port/aem/start.html.
1. Navegue até Ferramentas > Operações > Migração de conteúdo

   ![imagem](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > Verifique se você executou o relatório BPA antes e verifique com o URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html

1. Clique no cartão com título **Relatório do Transformador de conteúdo para BPA**

   ![imagem](/help/journey-migration/content-transformer/assets/ct-2.png)

   Veja abaixo um exemplo de como a página de Visão geral do transformador de conteúdo será exibida se a criação do relatório do BPA tiver sido bem-sucedida e se encontrar problemas relacionados ao conteúdo.

   O tempo de expiração restante para o relatório do BPA é mostrado no painel lateral. É recomendável executar o transformador de Conteúdo com o relatório de BPA mais recente para evitar a perda de quaisquer resultados relacionados ao conteúdo.

   ![imagem](/help/journey-migration/content-transformer/assets/ct-3.png)

1. Você pode filtrar os problemas com base em `Pattern Code`, `Subtype`, `Importance`, e `Source`.

   ![imagem](/help/journey-migration/content-transformer/assets/ct-4.png)

1. Você pode selecionar todos os problemas ou problemas específicos e mover, remover ou renomear para resolvê-los. Caminhos personalizados também podem ser adicionados usando **Adicionar caminhos** no canto superior direito.

   >[!NOTE]
   > Ao usar a operação de mover, é recomendável mover todos os caminhos para apenas uma pasta (por exemplo, em `/etc/packages/content-transformation/paths`), de modo que, quando os pacotes de backup forem instalados para trazer a instância de volta ao estado original, a pasta (`/etc/packages/content-transformation/paths`) pode ser excluído usando a operação remover para reduzir o tamanho do repositório.

   ![imagem](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![imagem](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > Qualquer operação que possa alterar o conteúdo de origem (`move`/`remove`/`rename`) criará por padrão um pacote de backup dos caminhos de origem em `/etc/packages/content-transformation` antes da transformação. Embora cada caixa de diálogo de operação tenha uma opção para desabilitar/habilitar a criação de pacote de backup, é estritamente recomendável ter sempre a opção habilitar criação de pacote selecionada.

1. Um exemplo de pacote de backup criado para a operação de movimentação dos caminhos é mostrado abaixo. Clique em Instalar para trazer de volta os caminhos de origem. A instalação traz apenas os caminhos de origem de volta ao local original e não exclui os caminhos para onde foram movidos durante a transformação. Para excluir os caminhos no local movido, clique em **Adicionar caminhos** botão para adicionar o local (por exemplo, `/etc/packages/content-transformation/paths`), selecione o local e clique em **Remover**.

   >[!CAUTION]
   > Não excluir `/etc/packages/content-transformation` pois esse é o local onde residem os pacotes de backup. Somente quando tiver certeza de que não precisa mais desses pacotes, poderá excluir esse local para reduzir o tamanho do repositório.

   ![imagem](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![imagem](/help/journey-migration/content-transformer/assets/ct-8.png)
