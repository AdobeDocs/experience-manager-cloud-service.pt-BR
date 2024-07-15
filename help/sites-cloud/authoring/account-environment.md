---
title: Configurar o ambiente da sua conta
description: O Adobe Experience Manager (AEM) fornece a capacidade de configurar a sua conta e determinados aspectos do ambiente de Autor.
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 60%

---

# Configurar o ambiente da sua conta   {#configuring-your-account-environment}

O Adobe Experience Manager (AEM) fornece a capacidade de configurar a sua conta e determinados aspectos do ambiente de Autor.

Usando a opção [Usuário](#user-settings) no [cabeçalho](/help/sites-cloud/authoring/basic-handling.md#the-header) e a caixa de diálogo [Minhas preferências](#my-preferences) associada, é possível modificar suas opções de usuário, como as seguintes:

Comece acessando a opção [Usuário](#user-settings) no cabeçalho.

## Configurações de usuário {#user-settings}

A caixa de diálogo de configurações do **usuário** concede acesso a:

* Representar como
   * Com a funcionalidade Representar como, um usuário pode trabalhar em nome de outro usuário. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Perfil
   * Ele oferece um link conveniente para suas configurações de usuário <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [Minhas preferências](#my-preferences)
   * Especifique várias configurações de preferências exclusivas para seu usuário

![Configurações de usuário](/help/sites-cloud/authoring/assets/user-settings.png)

### Minhas preferências {#my-preferences}

A caixa de diálogo **Minhas Preferências** é acessada por meio da opção [Usuário](#user-settings) no cabeçalho.

Cada usuário pode definir suas próprias propriedades preferenciais.

![Minhas preferências](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Idioma**

  Isso define o idioma a ser usado na interface do ambiente de criação. Selecione o idioma apropriado na lista.

* **Gerenciamento de janelas**

  Isso define o comportamento ou a abertura de janelas. Selecione um dos seguintes:

   * **Várias janelas** (padrão)

      * As páginas são abertas em uma nova janela.

   * **Uma janela**

      * As páginas são abertas na janela atual.

* **Mostrar ações do desktop para Ativos**

  Essa opção requer o aplicativo de desktop AEM para uso.

* **Cor da anotação**

  Isso define a cor padrão usada ao fazer anotações.

   * Clique no bloco de cores para que você possa abrir o seletor de amostras e selecionar uma cor.
   * Como alternativa, insira o código hexadecimal da cor desejada no campo.

* **Apresentação de data relativa**

  Para melhorar a legibilidade, o AEM renderiza datas nos últimos sete dias como datas relativas (por exemplo, três dias atrás) e datas mais antigas como datas exatas (por exemplo, 20 de março de 2017).

  Essa opção define como as datas no sistema são exibidas. As opções disponíveis são as seguintes:

   * **Sempre mostrar data exata**: a data exata é sempre exibida (nunca uma data relativa).
   * **1 dia**: a data relativa é mostrada para datas dentro de um dia; caso contrário, uma data exata é mostrada.
   * **7 dias (padrão)**: a data relativa é mostrada para datas dentro de sete dias; caso contrário, uma data exata é mostrada.
   * **1 mês**: a data relativa é mostrada para datas dentro de um mês; caso contrário, uma data exata é mostrada.
   * **1 ano**: a data relativa é mostrada para datas dentro de um ano; caso contrário, uma data exata é mostrada.
   * **Sempre mostrar data relativa**: as datas exatas nunca são mostradas, e apenas as datas relativas são mostradas.

* **Habilitar atalhos**

  O AEM oferece suporte a vários atalhos de teclado que tornam a criação mais eficiente.

   * [Atalhos de teclado para editar páginas](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
   * [Atalhos de teclado para os consoles](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)

  Essa opção habilita os atalhos de teclado. Por padrão, eles são ativados, mas podem ser desativados se, por exemplo, um usuário tiver determinados requisitos de acessibilidade.

* **Ativar a Página inicial dos ativos**

  Essa opção só estará disponível se o administrador do sistema tiver ativado a experiência da Página inicial da Assets para toda a organização.

* **Configuração do Stock**

  Esta opção permite especificar a configuração preferencial do Adobe Stock e só estará disponível se o administrador do sistema tiver habilitado a [integração com o Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
