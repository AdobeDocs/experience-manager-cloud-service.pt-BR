---
title: Como preencher previamente campos de formulário adaptável
description: Use dados existentes para preencher previamente os campos de um Formulário adaptável. Os usuários podem preencher previamente as informações básicas em um formulário fazendo logon com seus perfis sociais.
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: preenchimento prévio de formulário adaptável, serviços de entrega de borda de formulários adaptáveis, preenchimento automático de formulário adaptável
exl-id: 7b6224e2-a19c-4146-8545-0ce9d1da9b29
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 1%

---

# Configuração do serviço de preenchimento prévio no Forms adaptável usando o Edge Delivery Services

Preenchimento prévio de formulário é o processo de preencher automaticamente campos de formulário com dados relevantes de fontes externas assim que um usuário abre o formulário. Aproveitando informações de perfis de usuários, bancos de dados, rascunhos salvos ou outros sistemas de back-end, o preenchimento prévio simplifica a experiência de preenchimento de formulário, reduzindo a entrada manual, minimizando erros e acelerando a conclusão. Isso não apenas aumenta a satisfação do usuário, como também aumenta a probabilidade de envios bem-sucedidos de formulários.

## Benefícios do preenchimento prévio do formulário

| Benefício | Descrição |
|---------|-------------|
| **Conclusão mais rápida** | Reduz a entrada manual de dados, ajudando os usuários a preencherem formulários rapidamente |
| **Experiência de usuário aprimorada** | O Forms se sente mais personalizado e conveniente, especialmente para usuários recorrentes |
| **Taxas de conversão mais altas** | Reduz o abandono de formulários minimizando o esforço necessário dos usuários |
| **Erros de Entrada Reduzidos** | Dados de fontes confiáveis diminuem erros de digitação e entradas incorretas |
| **Melhor qualidade dos dados** | Garante dados estruturados, precisos e consistentes para sistemas de back-end |

## Como funciona o preenchimento prévio

O diagrama a seguir ilustra o processo de preenchimento automático que ocorre quando um usuário abre um Formulário adaptável:

![Fluxo do processo de preenchimento prévio do formulário](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

O processo de preenchimento prévio envolve quatro etapas principais:

1. **O usuário abre o formulário**: o usuário acessa um formulário adaptável por meio de uma URL ou navegação
1. **Identificar Source de Dados**: o serviço de Preenchimento Prévio determina a fonte de dados configurada (Modelo de Dados de Formulário ou serviço de Rascunho)
1. **Recuperar Dados**: o sistema busca dados de usuário relevantes com base no contexto, nos parâmetros ou na identificação do usuário
1. **Mapear e Exibir**: os dados são mapeados para campos de formulário usando propriedades `bindRef` e o formulário preenchido é exibido ao usuário

Esse processo automatizado garante que os usuários vejam um formulário pré-preenchido com suas informações relevantes, melhorando significativamente a experiência do usuário e as taxas de conclusão do formulário.

## Estrutura de dados para preenchimento prévio

O Forms adaptável oferece suporte a dois tipos de campos:

- **Campos associados**: campos conectados a uma fonte de dados com uma propriedade `bindRef` não vazia
- **Campos não associados**: campos autônomos com `bindRef` valores vazios

A estrutura de dados de preenchimento prévio inclui:

- **afBoundData**: contém dados para campos e painéis ligados
- **afUnBoundData**: contém dados para campos não associados

O formato de dados deve corresponder ao seu modelo de formulário:

- **Formulários XFA**: XML compatível com esquema de modelo XFA
- **Formulários de esquema XML**: XML correspondente à estrutura do esquema
- **Formulários de esquema JSON**: compatível com JSON com o esquema
- **Formulários do Modelo de Dados de Formulário (FDM)**: JSON correspondente à estrutura do FDM
- **Formulários sem esquema**: todos os campos estão desvinculados e usam XML desvinculado

## Pré-requisitos

Antes de configurar os serviços de preenchimento prévio, verifique se você tem:

### Configuração necessária

- [Repositório GitHub configurado para o Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [Bloco Forms adaptável adicionado ao projeto](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [Fonte de dados configurada](/help/forms/configure-data-sources.md)
- [Modelo de dados de formulário (FDM) criado](/help/forms/create-form-data-models.md)

### Requisitos de acesso

- Acesso ao AEM Forms as a Cloud Service
- Permissões para criar e editar formulários
- Acesso ao Universal Editor com extensões necessárias habilitadas

>[!TIP]
>
> Também é possível editar formulários para integrar o Modelo de dados de formulário (FDM) no Editor universal para buscar dados de várias fontes de back-end. Para obter detalhes, consulte o artigo [Integrar formulários com o Modelo de dados de formulário no Editor Universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

## Opções de serviço de preenchimento prévio

O Editor universal fornece duas opções de serviço de preenchimento prévio:

| Tipo de serviço | Propósito | Fonte de Dados | Melhor para |
|--------------|---------|-------------|----------|
| **Preenchimento Prévio de Rascunho do Portal de Formulários** | Retoma formulários parcialmente preenchidos | Rascunhos salvos no Forms Portal | Continuação de aplicativos incompletos |
| **Preenchimento de Modelo de Dados de Formulário** | Preenche campos de sistemas externos | Bancos de dados de back-end via FDM | Preenchimento automático de dados de perfil do usuário |

### Comparação detalhada

| Destaque | Serviço de preenchimento de rascunho | Serviço de preenchimento prévio do FDM |
|---------|----------------------|---------------------|
| **Autenticação** | Requer logon de usuário para acesso de rascunho | Configurável com base na fonte de dados |
| **Complexidade da Instalação** | Configuração mínima | Exige configuração e mapeamento de FDM |
| **Tipo de dados** | Dados estáticos salvos | Dados dinâmicos em tempo real |
| **Caso de uso** | Retomar aplicativos salvos | Preencher previamente com base em perfis de usuário ou bancos de dados |


## Configurar o serviço de preenchimento prévio para um formulário

+++Fase 1: Configuração Do Modelo De Dados De Formulário

### Etapa 1: Criar modelo de dados do formulário

1. Faça logon na sua instância do AEM Forms as a Cloud Service
1. Navegue até **Adobe Experience Manager** > **Forms** > **Integrações de Dados**
1. Selecione **Criar** > **Modelo de Dados de Formulário**
1. Escolha sua **Configuração do Data Source** e selecione o **Data Source** configurado

   ![Modelo de dados de formulário criado](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >Para obter instruções detalhadas sobre como criar Modelos de Dados de Formulário, consulte [Criar Modelo de Dados de Formulário](/help/forms/create-form-data-models.md).

### Etapa 2: Configurar Serviços do FDM

1. Ir para **Adobe Experience Manager** > **Forms** > **Integrações de Dados**
1. Abrir o modelo de dados de formulário no modo de edição
1. Selecione um objeto de modelo de dados e clique em **Editar Propriedades**
1. Configurar os serviços **Leitura** e **Gravação** para os objetos de modelo de dados selecionados

   ![Configurar serviço de leitura/gravação](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. Configurar argumentos do serviço:

   - Clique no ícone de edição para o argumento do serviço de leitura
   - Associe o argumento a um **Atributo de Perfil de Usuário**, **Atributo de Solicitação** ou **Valor literal**
   - Especifique o valor da associação (por exemplo, `petid` para um formulário de registro de animal de estimação)

   ![Configurar argumento de id do animal de estimação](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. Clique em **Concluído** para salvar o argumento e em **Salvar** para salvar o FDM

   >[!NOTE]
   >
   > Saiba mais sobre como configurar serviços do FDM em [Trabalhar com o Modelo de Dados de Formulário (FDM)](/help/forms/work-with-form-data-model.md).

+++

+++Fase 2: Criação e configuração do formulário adaptável

### Etapa 3: Criar um formulário adaptável

1. Navegue até **Adobe Experience Manager** > **Forms** > **Forms e Documentos**
1. Selecione **Criar** > **Forms Adaptável**
1. Na guia **Source**, selecione um modelo do Edge Delivery Services:

   ![Modelo do Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

1. Clique em **Criar** para abrir o assistente **Criar Formulário**

   >[!NOTE]
   >
   > Você pode configurar a fonte de dados na guia **Dados** ou posterior editando as propriedades do formulário.

1. Especifique os detalhes do formulário:

   - **Nome**: insira um nome descritivo para o formulário
   - **Título**: forneça um título amigável
   - **URL do GitHub**: insira sua URL de repositório (por exemplo, `https://github.com/wkndforms/edsforms`)

1. Clique em **Criar**

   ![Criar formulário baseado em esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

O formulário é aberto no Editor universal para criação.

### Etapa 4: configurar o Form Data Source

1. Selecione seu formulário e clique em **Propriedades**

   ![Selecionar Propriedades do Formulário](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. Abra a guia **Modelo de formulário**
3. Na lista suspensa **Selecionar de**, escolha **Modelo de Dados de Formulário (FDM)**
4. Selecione o modelo de dados de formulário criado (por exemplo, PetFDM) na lista suspensa

   ![Guia Selecionar modelo de formulário](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. Clique em **Salvar e fechar**
6. Abrir o formulário para edição no Editor Universal

Os elementos de formulário do FDM aparecem na guia **Datasource** do **Navegador de Conteúdo**.

### Etapa 5: Adicionar vinculação de dados a campos de formulário

1. Selecionar elementos de dados na guia **Fonte de Dados**
2. Clique em **Adicionar** ou arraste e solte elementos para criar seu formulário

   ![Captura de tela do Editor Universal mostrando o formulário baseado em esquema](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. Adicionar vinculação de dados a campos de formulário:

   - Selecionar um campo de formulário
   - No painel **Propriedades**, localize a propriedade **Referência de Ligação**
   - Selecione a referência de vinculação de dados apropriada

     ![Associação de Dados](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++Fase 3: Configuração do serviço de preenchimento prévio

### Etapa 6: Ativar extensões necessárias

Verifique se essas extensões estão habilitadas no Universal Editor:

1. **Extensão de Propriedades do Formulário do AEM**

   - Abrir **Extension Manager** no Editor Universal
   - Habilitar a extensão **Propriedades do Formulário AEM**

   ![Ícone de propriedades do formulário](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **Extensão do Data Source**

   - Habilite a extensão **Fonte de dados** se você não visualizar o ícone **Fontes de dados**

   ![Captura de tela do Universal Editor Extension Manager](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > Para obter instruções detalhadas sobre como gerenciar extensões, consulte [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

### Etapa 7: configurar o serviço de preenchimento prévio

1. Abra o formulário adaptável no Editor universal
2. Clique no ícone de extensão **Propriedades do AEM Form**

   ![Ícone Selecionar Propriedades do Formulário](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. Clique na guia **Preenchimento prévio**
4. Selecionar **Serviço de Preenchimento de Modelo de Dados de Formulário**

   ![Selecionar serviço de preenchimento prévio](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. Clique em **Salvar e fechar**

+++

+++Fase 4: Testar A Configuração De Preenchimento Prévio

### Etapa 8: pré-visualização e teste

1. Ir para **Forms** > **Forms e Documentos**
2. Selecione o formulário adaptável
3. Escolher **Visualizar como HTML**
4. Teste o preenchimento prévio anexando parâmetros ao URL:

   `https://your-preview-url.com?<bindreferencefield>=<value>`

   **Exemplo:**

   https://your-preview-url.com?petid=12345

   ![Preencher Formulário](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

O formulário deve ser preenchido automaticamente com dados com base no parâmetro fornecido.

+++

## Exemplos

### Estruturas de dados de preenchimento prévio de exemplo

**Exemplo de JSON para o Formulário baseado em FDM:**

```
  {
    "afBoundData": {
      "user": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@example.com",
        "phone": "+1-555-0123"
      }
    },
    "afUnBoundData": {
      "additionalInfo": "User preferences loaded"
    }
  }
```

**Exemplo XML para o Formulário baseado em XFA:**

```
  <?xml version="1.0" encoding="UTF-8"?>
  <afData>
    <afBoundData>
      <user>
        <firstName>John</firstName>
        <lastName>Doe</lastName>
        <email>john.doe@example.com</email>
      </user>
    </afBoundData>
  </afData>
```

### Exemplo de URLs de preenchimento prévio

Os URLs abaixo são apenas para fins de ilustração e não funcionarão como estão. Substitua o host e os parâmetros pelos relevantes ao seu próprio ambiente ao testar a funcionalidade de preenchimento prévio.

**Teste básico de preenchimento prévio:**

`https://preview.example.com/form.html?userId=12345`

**Teste de vários parâmetros:**

`https://preview.example.com/form.html?userId=12345&category=premium`


## Resolução de problemas

+++Problemas comuns e soluções

| Problema | Causa possível | Solução |
|-------|----------------|----------|
| **Campos de formulário não preenchidos previamente** | Valores de `bindRef` incorretos | Verificar se `bindRef` corresponde exatamente a nomes de campos FDM |
| **Erros de formato de dados** | Estrutura de dados incompatível | Garantir que os dados pré-preenchidos correspondam ao esquema do modelo de formulário |
| **Serviço não encontrado** | Problemas de configuração do FDM | Verifique se os serviços do FDM estão configurados e salvos corretamente |
| **Erros de autenticação** | Conectividade da fonte de dados | Verificar credenciais e conectividade da fonte de dados |
| **Carregamento de dados parcial** | Mapeamentos de campo ausentes | Verificar se todos os campos obrigatórios têm vínculos de dados adequados |

+++

+++Etapas de depuração

1. **Verificar Configuração do FDM:**

   - Verificar se os serviços estão configurados corretamente
   - Testar os serviços do FDM independentemente
   - Validar conectividade da fonte de dados

2. **Verificar Configuração do Formulário:**

   - Confirmar se o formulário está associado ao FDM correto
   - Verificar os valores do campo `bindRef`
   - Formulário de ensaio sem preenchimento prévio

3. **Testar Fluxo de Dados:**

   - Usar ferramentas de desenvolvedor do navegador para inspecionar solicitações de rede
   - Verifique se há erros de JavaScript no console
   - Validar formato de dados de resposta

4. **Mensagens de Erro Comuns:**

   - &quot;Serviço de preenchimento prévio não encontrado&quot;: verifique a configuração do serviço
   - &quot;Falha na associação de dados&quot;: verifique a precisão `bindRef`
   - &quot;Formato de dados inválido&quot;: verifique se os dados correspondem ao esquema

+++

## Práticas recomendadas

+++Práticas recomendadas de configuração

- **Usar nomenclatura descritiva**: nomeie seus FDMs e serviços com clareza
- **Validar esquemas de dados**: verifique se a estrutura de dados corresponde aos requisitos do formulário
- **Testar incrementalmente**: configurar e testar um campo por vez
- **Mapeamentos de documentos**: acompanhar os mapeamentos de campo para dados

+++

+++Otimização do desempenho

- **Minimizar volume de dados**: preencher apenas os campos necessários
- **Usar armazenamento em cache**: configurar o armazenamento em cache apropriado para os dados acessados com frequência
- **Otimizar consultas**: verifique se as consultas ao banco de dados são eficientes
- **Monitorar desempenho**: Rastrear tempos de carregamento de formulário com preenchimento prévio habilitado

+++

+++Considerações sobre segurança

- **Validar parâmetros de entrada**: sempre validar parâmetros de URL
- **Limpar dados**: limpe os dados antes de preencher formulários previamente
- **Implementar controles de acesso**: certifique-se de que os usuários só possam acessar seus próprios dados
- **Usar HTTPS**: sempre usar conexões seguras para transmissão de dados

+++

+++Diretrizes de experiência do usuário

- **Fornecer feedback**: Mostrar indicadores de carregamento durante a busca de dados
- **Lidar com erros normalmente**: exibir mensagens de erro úteis
- **Permitir substituições**: permitir que os usuários modifiquem dados preenchidos previamente
- **Manter consistência**: usar comportamento de preenchimento prévio consistente em formulários

+++

## Perguntas frequentes

+++Como testar se o preenchimento prévio está funcionando corretamente?

Visualize o formulário e anexe parâmetros de preenchimento prévio à URL usando este formato: `?<bindreferencefield>=<value>`. Verifique se o campo tem um `bindRef` válido que corresponda à estrutura de dados. Use as ferramentas de desenvolvedor do navegador para inspecionar solicitações de rede e verificar se os dados estão sendo obtidos corretamente.

+++

+++Quais formatos de dados são compatíveis com o preenchimento prévio do Adaptive Forms?

O Forms adaptável é compatível com vários formatos, dependendo do modelo de formulário:

- **Formulários XFA**: XML correspondente ao esquema XFA
- **Formulários de esquema JSON**: dados JSON compatíveis com o esquema
- **Formulários FDM**: JSON que mapeia para a estrutura do modelo de dados
- **Formulários de esquema XML**: XML correspondente à estrutura do esquema

+++

+++Posso preencher previamente campos vinculados e não vinculados?

Sim, você pode preencher previamente ambos os tipos de campos. Os campos associados usam a seção `afBoundData` e devem corresponder ao esquema do modelo de formulário. Campos desatados usam a seção `afUnBoundData` e podem conter dados adicionais.

+++

+++O que devo fazer se apenas alguns campos estiverem sendo preenchidos previamente?

Verifique se todos os campos têm `bindRef` valores corretos que correspondam exatamente ao seu FDM. Verifique se a fonte de dados contém todos os campos obrigatórios e se a estrutura de dados corresponde ao esquema do modelo de formulário.

+++

+++Posso usar vários serviços de preenchimento prévio em um formulário?

É possível configurar um serviço de preenchimento prévio principal por formulário. No entanto, é possível combinar diferentes fontes de dados em um único Modelo de dados de formulário para obter funcionalidade semelhante.

+++

+++Como gerenciar a autenticação de serviços de preenchimento prévio?

A autenticação depende da configuração da fonte de dados. Para preenchimento prévio baseado em FDM, configure a autenticação nas configurações da fonte de dados. Para o preenchimento prévio de rascunho, os usuários normalmente precisam estar conectados para acessar os rascunhos salvos.

+++



## Tópicos relacionados

- [Integrar formulários com o Modelo de dados de formulário no Editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [Criar modelos de dados de formulário](/help/forms/create-form-data-models.md)
- [Trabalhar com o modelo de dados de formulário (FDM)](/help/forms/work-with-form-data-model.md)
- [Configurar fontes de dados](/help/forms/configure-data-sources.md)
- [Introdução ao Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
