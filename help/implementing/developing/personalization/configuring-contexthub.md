---
title: Configuração do ContextHub
description: Saiba como configurar o Context Hub.
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 1%

---


# Configuração do ContextHub {#configuring-contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. Para obter mais detalhes sobre o ContextHub, consulte a visão geral [do desenvolvedor do](contexthub.md)ContextHub.

Você pode configurar a barra de ferramentas do ContextHub para controlar se ela aparece no modo de Pré-visualização, para criar armazenamentos do ContextHub e adicionar módulos de interface.

## Mostrar e ocultar a interface do usuário do ContextHub {#showing-and-hiding-the-contexthub-ui}

Configure o serviço OSGi do Adobe Granite ContextHub para mostrar ou ocultar a interface do usuário [do](/help/sites-cloud/authoring/personalization/targeted-content.md) ContextHub em suas páginas. O PID deste serviço é `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Para configurar o serviço, você pode usar o Console [da](/help/implementing/deploying/configuring-osgi.md) Web ou usar um nó JCR no repositório:

* **Console da Web:** Para mostrar a interface do usuário, selecione a propriedade Mostrar interface do usuário. Para ocultar a interface do usuário, limpe a propriedade Ocultar interface do usuário.
* **Nó JCR:** Para mostrar a interface do usuário, defina a `com.adobe.granite.contexthub.show_ui` propriedade booleana como `true`. Para ocultar a interface do usuário, defina a propriedade como `false`.

Ao mostrar a interface do usuário do ContextHub, ela só aparece nas páginas AEM instâncias do autor. A interface do usuário não aparece nas páginas das instâncias de publicação.

## Adicionando módulos e módulos de interface do usuário do ContextHub {#adding-contexthub-ui-modes-and-modules}

Configure os modos e módulos de interface que aparecem na barra de ferramentas do ContextHub no modo de Pré-visualização:

* Modos da interface: Grupos de módulos relacionados
* Módulos: Widgets que expõem dados de contexto de uma loja e permitem que os autores manipulem o contexto

Os modos de interface são exibidos como uma série de ícones no lado esquerdo da barra de ferramentas. Quando selecionados, os módulos de um modo de interface aparecem à direita.

![Barra de ferramentas do ContextHub](assets/contexthub-toolbar.png)

Os ícones são referências da biblioteca [de ícones da interface do](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)Coral.

### Adicionando um modo de interface do usuário {#adding-a-ui-mode}

Adicione um modo de interface para agrupar módulos ContextHub relacionados. Ao criar o modo de interface do usuário, você fornece o título e o ícone exibidos na barra de ferramentas do ContextHub.

1. No painel Experience Manager, clique ou toque em Ferramentas > Sites > Context Hub.
1. Clique ou toque no Container de configuração padrão.
1. Clique ou toque em Configuração do Context Hub.
1. Clique ou toque no botão Criar e, em seguida, clique ou toque em Modo de interface do usuário do Context Hub.

   ![Adicionar modo de interface](assets/contexthub-ui-mode.png)

1. Forneça valores para as seguintes propriedades:

   * Título do modo da interface do usuário: O título que identifica o modo da interface do usuário
   * Ícone Modo: O seletor para o ícone [da interface do](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) Coral a ser usado, por exemplo `coral-Icon--user`
   * Ativado: Selecione para mostrar o modo da interface na barra de ferramentas do ContextHub

1. Clique ou toque em Salvar.

### Adicionando um módulo de interface {#adding-a-ui-module}

Adicione um módulo de interface do ContextHub a um modo de interface do usuário para que ele apareça na barra de ferramentas do ContextHub para visualizar o conteúdo da página. Ao adicionar um módulo de interface, você está criando uma instância de um tipo de módulo que está registrado no ContextHub. Para adicionar um módulo de interface, é necessário saber o nome do tipo de módulo associado.

AEM fornece um tipo de módulo de interface de usuário base, além de vários tipos de exemplo de módulo de interface de usuário nos quais você pode basear um módulo de interface de usuário. A tabela a seguir fornece uma breve descrição de cada uma. Para obter informações sobre como desenvolver um módulo de interface personalizado, consulte [Criação de módulos](extending-contexthub.md#creating-contexthub-ui-module-types)de interface do usuário do ContextHub.

As propriedades do módulo de interface incluem uma configuração detalhada na qual você pode fornecer valores para propriedades específicas do módulo. Você fornece a configuração detalhada no formato JSON. A coluna Tipo de módulo na tabela fornece links para informações sobre o código JSON necessário para cada tipo de módulo de interface.

| Tipo de módulo | Descrição | Armazenar |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | Um tipo de módulo de interface genérica | Configurado nas propriedades do módulo da interface do usuário |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | Exibe informações sobre o navegador | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | Exibe informações de data e hora | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | Exibe a latitude e a longitude do cliente, bem como o local em um mapa. Permite alterar o local. | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | Exibe a orientação da tela do dispositivo (paisagem ou retrato) | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | Exibe estatísticas sobre tags de página | `tagcloud` |
| [granite.perfil](sample-modules.md#granite-profile-ui-module-type) | Exibe as informações do perfil para o usuário atual, incluindo `authorizableID`, `displayName` e `familyName`. Você pode alterar o valor de `displayName` e `familyName`. | `profile` |

1. No painel Experience Manager, clique ou toque em Ferramentas > Sites > ContextHub.
1. Clique ou toque no Container Configuração ao qual deseja adicionar um módulo de interface do usuário.
1. Clique ou digite a Configuração do ContextHub à qual você deseja adicionar o módulo da interface.
1. Clique ou toque no modo de interface do usuário ao qual você está adicionando o módulo de interface.
1. Clique ou toque no botão Criar e, em seguida, clique ou toque em Módulo de interface do usuário do ContextHub (genérico).

   ![Módulo de interface do usuário do ContextHub](assets/contexthub-ui-module.png)

1. Forneça valores para as seguintes propriedades:

   * Título do módulo da interface do usuário: Um título que identifica o módulo da interface do usuário
   * Tipo de módulo: O tipo de módulo
   * Ativado: Selecione para mostrar o módulo da interface na barra de ferramentas do ContextHub

1. (Opcional) Para substituir a configuração de armazenamento padrão, insira um objeto JSON para configurar o Módulo de interface.
1. Clique ou toque em Salvar.

## Criação de uma loja do ContextHub {#creating-a-contexthub-store}

Crie um repositório do Context Hub para manter os dados do usuário e acessar os dados conforme necessário. As lojas do ContextHub são baseadas em candidatos a lojas registradas. Ao criar a loja, você precisa do valor de storeType com o qual o candidato da loja foi registrado. (Consulte [Criação de Candidatos](extending-contexthub.md#creating-custom-store-candidates)à Loja Personalizada.)

### Configuração detalhada da loja {#detailed-store-configuration}

Quando você configura uma loja, a propriedade Configuração de detalhes permite que você forneça valores para propriedades específicas da loja. O valor é baseado no `config` parâmetro da `init` função do repositório. Portanto, se você precisa fornecer esse valor e o formato do valor depende da loja.

O valor da propriedade Detail Configuration é um `config` objeto no formato JSON.

### Amostra de candidatos à loja {#sample-store-candidates}

AEM fornece os seguintes candidatos de armazenamento de amostra nos quais você pode basear uma loja.

| Tipo de armazenamento | Descrição |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | Armazenar para segmentos do ContextHub resolvidos e não resolvidos. Recupera automaticamente segmentos do ContextHub SegmentManager |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | Armazena a latitude e a longitude do local do navegador. |
| [granite.emuladores](sample-stores.md#granite-emulators-sample-store-candidate) | Define as propriedades e os recursos de vários dispositivos e detecta o dispositivo cliente atual |
| [granite.perfil](sample-stores.md#granite-profile-sample-store-candidate) | Armazena dados do perfil para o usuário atual |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | Armazena informações sobre o cliente, como informações do dispositivo, tipo de navegador e orientação da janela |

1. No painel Experience Manager, clique ou toque em Ferramentas > Sites > ContextHub.
1. Clique ou toque no container de configuração padrão.
1. Clique ou toque em Configuração do Contexthub
1. Para adicionar uma loja, clique ou toque no ícone Criar e, em seguida, clique ou toque em Configuração da loja do ContextHub.

   ![Configuração do repositório do ContextHub](assets/contexthub-store-configuration.png)

1. Forneça valores para as propriedades de configuração básicas e clique ou toque em Avançar:

   * **Título da configuração:** O título que identifica a loja
   * **Tipo de armazenamento:** O valor da propriedade storeType do candidato da loja no qual basear a loja
   * **Obrigatório:** Selecionar
   * **Ativado:** Selecione para ativar a loja

1. (Opcional) Para substituir a configuração de armazenamento padrão, digite um objeto JSON na caixa Configuração de detalhes (JSON).
1. Clique ou toque em Salvar.

## Exemplo: Uso de um serviço JSONP  {#example-using-a-jsonp-service}

Este exemplo ilustra como configurar uma loja e exibir os dados em um módulo de interface do usuário. Neste exemplo, o serviço MD5 do site jsontest.com é usado como uma fonte de dados para uma loja. O serviço retorna o código de hash MD5 de uma determinada string, no formato JSON.

Uma loja contexthub.generic-jsonp é configurada para que armazene dados para a chamada de serviço `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. O serviço retorna os seguintes dados exibidos em um módulo de interface do usuário:

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Criação de uma loja contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

O candidato de armazenamento de amostra contexthub.generic-jsonp permite recuperar dados de um serviço JSONP ou de um serviço da Web que retorna dados JSON. Para o candidato a esta loja, use a configuração da loja para fornecer detalhes sobre o serviço JSONP a ser usado.

A função [init](contexthub-api.md#init-name-config) da classe `ContextHub.Store.JSONPStore` Javascript define um `config` objeto que inicializa esse candidato de armazenamento. O `config` objeto contém um `service` objeto que inclui detalhes sobre o serviço JSONP. Para configurar a loja, forneça o `service` objeto no formato JSON como o valor da propriedade Detail Configuration.

Para salvar dados do serviço MD5 do site jsontest.com, use o procedimento em [Criar uma loja](#creating-a-contexthub-store) do ContextHub usando as seguintes propriedades:

* **Título da configuração:** md5
* **Tipo de armazenamento:** contexthub.generic-jsonp
* **Obrigatório:** Selecionar
* **Ativado:** Selecionar
* **Configuração detalhada (JSON):**

   ```javascript
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### Adicionar um módulo de interface para os dados md5 {#adding-a-ui-module-for-the-md-data}

Adicione um módulo de interface à barra de ferramentas do ContextHub para exibir os dados armazenados no armazenamento md5 de exemplo. Neste exemplo, o módulo contexthub.base é usado para produzir o seguinte módulo de interface:

![Armazenamento MD5 ContextHub](assets/contexthub-md5-store.png)

Use o procedimento em [Adicionar um módulo](#adding-a-ui-module) de interface para adicionar o módulo de interface a um modo de interface de usuário existente, como o exemplo do modo de interface pessoal. Para o Módulo de interface, use os seguintes valores de propriedade:

* **Título do módulo da interface do usuário:** MD5
* **Tipo de módulo:** contexthub.base
* **Configuração detalhada (JSON):**

   ```javascript
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Conversion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## Depuração do ContextHub {#debugging-contexthub}

Um modo de depuração do ContextHub pode ser habilitado para permitir a solução de problemas. O modo de depuração pode ser ativado pela configuração do ContextHub ou pelo CRXDE.

### Pela configuração {#via-the-configuration}

Edite a configuração do ContextHub e marque a opção **Depurar**

1. No painel, clique ou toque em **Ferramentas > Sites > ContextHub**
1. Clique ou toque no Container **Configuração padrão**
1. Selecione a Configuração **do** ContextHub e clique ou toque em **Editar elemento selecionado**
1. Clique ou toque em **Depurar** e clique ou toque em **Salvar**

### Via CRXDE {#via-crxde}

Use a CRXDE Lite para definir a propriedade como `debug` true **** em:

* `/conf/global/settings/cloudsettings` ou
* `/conf/<site>/settings/cloudsettings`

### Registrando mensagens de depuração para o ContextHub {#logging-debug-messages-for-contexthub}

Configure o serviço OSGi do Adobe Granite ContextHub (PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`) para registrar mensagens de Depuração detalhadas que são úteis ao desenvolver.

Para configurar o serviço, você pode usar o Console [da](/help/implementing/deploying/configuring-osgi.md) Web ou usar um nó JCR no repositório:

* Console da Web: Para registrar mensagens de Depuração, selecione a propriedade Depuração.
* Nó JCR: Para registrar mensagens de Depuração, defina a `com.adobe.granite.contexthub.debug` propriedade booleana como `true`.

### Modo silencioso {#silent-mode}

O modo silencioso suprime todas as informações de depuração. Ao contrário da opção de depuração normal, que pode ser definida independentemente para cada configuração do ContextHub, o modo silencioso é uma configuração global que tem precedência sobre qualquer configuração de depuração no nível de configuração do ContextHub.

Isso é útil para a sua instância de publicação, onde você não quer nenhuma informação de depuração. Como é uma configuração global, ela é ativada via OSGi.

1. Abra a Configuração **do Console da Web do** Adobe Experience Manager em `http://<host>:<port>/system/console/configMgr`
1. Procurar **Adobe Granite ContextHub**
1. Clique no **Adobe de configuração do ContextHub** Granite para editar suas propriedades
1. Marque a opção Modo **silencioso** e clique em **Salvar**

## Desabilitando o ContextHub {#disabling-contexthub}

O ContextHub pode ser desabilitado para impedir que ele carregue js/css e inicialize. Há duas opções para desativar o ContextHub:

* Edite a configuração do ContextHub e marque a opção **Desativar o ContextHub**

   1. No painel, clique ou toque em **Ferramentas > Sites > ContextHub**
   1. Clique ou toque no Container **Configuração padrão**
   1. Selecione a Configuração **do** ContextHub e clique ou toque em **Editar elemento selecionado**
   1. Clique ou toque em **Desativar ContextHub** e clique ou toque em **Salvar**

ou

* Use CRXDE Lite para definir a propriedade como `disabled` true **** em `/conf/global/settings/cloudsettings/<configName>/contexthub`
