---
title: Suporte XFA no Adaptive Forms baseado em XDP
seo-title: XFA support in XDP-based Adaptive Forms
description: Lista eventos XFA, propriedades, scripts e validação compatíveis no Adaptive Forms.
seo-description: Lists supported XFA events, properties, scripts, and validation in Adaptive Forms.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 5%

---


# Suporte XFA no Adaptive Forms baseado em XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Introdução {#introduction}

O Adaptive Forms oferece suporte a vários eventos, propriedades, scripts e validações XFA definidos em um arquivo XDP, incluindo:

* Execução de scripts definidos em eventos no arquivo XDP.
* Captura de valores padrão e propriedades comportamentais para campos no arquivo XDP.
* Execução de scripts de validação definidos no arquivo XDP.

Quando um formulário adaptável é criado com base em um arquivo XDP, as propriedades, os eventos e as validações são preenchidos automaticamente na interface de criação do formulário. No entanto, os autores de formulário podem substituir alguns desses elementos para criar uma experiência alternativa.

Este artigo lista eventos, propriedades e validações XFA compatíveis honrados no Adaptive Forms e explica como substituí-los no Adaptive Forms.

## Elementos XFA compatíveis e seu mapeamento no Adaptive Forms {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### Campos {#fields}

Quando um formulário adaptável é criado usando um arquivo XDP, você pode arrastar e soltar um campo XFA no formulário adaptável. A tabela a seguir lista como os campos XFA são mapeados para campos de Formulário adaptável.

<table>
 <tbody>
  <tr>
   <td><p><strong>Campo ou contêiner XFA</strong></p> </td>
   <td><p><strong>Componente de formulário adaptável correspondente</strong></p> </td>
  </tr>
  <tr>
   <td><p>Botão </p> </td>
   <td><p>Botão</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de seleção </p> </td>
   <td><p>Caixa de seleção</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de listagem </p> </td>
   <td><p>Lista suspensa</p> </td>
  </tr>
  <tr>
   <td><p>Campo de data/hora </p> </td>
   <td><p>Seletor de data</p> </td>
  </tr>
  <tr>
   <td><p>Rabisco de assinatura</p> </td>
   <td><p>Rabiscar a assinatura</p> </td>
  </tr>
  <tr>
   <td><p>Campo numérico </p> </td>
   <td><p>Caixa numérica</p> </td>
  </tr>
  <tr>
   <td><p>Campo decimal</p> </td>
   <td><p>Caixa numérica</p> </td>
  </tr>
  <tr>
   <td><p>Campo de texto </p> </td>
   <td><p>Caixa de texto</p> </td>
  </tr>
  <tr>
   <td><p>Campo de senha </p> </td>
   <td><p>Caixa Senha</p> </td>
  </tr>
  <tr>
   <td><p>Imagem</p> </td>
   <td><p>Imagem</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>Texto</p> </td>
  </tr>
  <tr>
   <td><p>Subformulário </p> </td>
   <td><p>Painel</p> </td>
  </tr>
  <tr>
   <td><p>Área (Grupo)</p> </td>
   <td><p>Painel</p> </td>
  </tr>
  <tr>
   <td><p>Conjunto de subformulários </p> </td>
   <td><p>Painel</p> </td>
  </tr>
 </tbody>
</table>

### Propriedades {#properties}

A tabela a seguir captura como vários scripts XFA definidos nos arquivos XDP se comportam no Adaptive Forms.

<table>
 <tbody>
  <tr>
   <td><p><strong>Propriedades do componente XFA</strong></p> </td>
   <td><p><strong>Comportamento correspondente no Adaptive Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Mapeado para a propriedade Referência de vínculo (bindRef) no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>presença </p> </td>
   <td><p>Mapeado para a propriedade visível no Formulário adaptável. É possível substituí-lo usando a expressão Visibility.</p> </td>
  </tr>
  <tr>
   <td><p>acesso </p> </td>
   <td><p>Mapeado para a propriedade ativada no Formulário adaptável. Você pode substituí-lo usando a expressão Access.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: função </p> </td>
   <td><p>Mapeado para a propriedade de função no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: speakPriority </p> </td>
   <td><p>Mapeado para a propriedade speakPriority no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: speakText</p> </td>
   <td><p>Mapeado para o texto personalizado de Acessibilidade no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: toolTip </p> </td>
   <td><p>Mapeado para a propriedade de descrição curta no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>legenda<em> (todos os tipos de campos)</em></p> </td>
   <td><p>Mapeado para a propriedade de título no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (todos os tipos de campos)</em></p> </td>
   <td><p>Mapeado para o padrão de exibição no formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (todos os tipos de campos)</em></p> </td>
   <td><p>Mapeado para a propriedade de valor no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>itens<em> (Caixa de listagem, Caixa de seleção)</em></p> </td>
   <td><p>Mapeado para a propriedade de opções no Formulário adaptável. Você pode substituí-lo usando a expressão Options.</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (Campo de texto)</em></p> </td>
   <td><p>Mapeado para a propriedade Máximo de caracteres permitidos no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>multilinha<em> (Campo de texto)</em></p> </td>
   <td><p>Mapeado para a propriedade Permitir várias linhas no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (Campo Numérico, Campo Decimal)</em></p> </td>
   <td><p>Mapeado para a propriedade de dígitos Frac no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (Campo Numérico, Campo Decimal)</em></p> </td>
   <td><p>Mapeado para a propriedade de dígitos de cliente potencial no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (Caixa de listagem)</em></p> </td>
   <td><p>Mapeado para a propriedade Permite seleção múltipla no Formulário adaptável.</p> </td>
  </tr>
 </tbody>
</table>

### Scripts {#scripts}

A tabela a seguir captura como vários scripts XFA definidos no arquivo XDP se comportam no Adaptive Forms.

<table>
 <tbody>
  <tr>
   <td><p><strong>Eventos de script XFA</strong></p> </td>
   <td><p><strong>Comportamento correspondente no Adaptive Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>inicializar </p> </td>
   <td><p>Esse script é executado no tempo de execução e não pode ser substituído no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>calcular</p> </td>
   <td><p>Mapeado para a expressão Calcular no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>validar </p> </td>
   <td><p>Mapeado para a expressão Validação no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Esse script é executado no tempo de execução e não pode ser substituído no Formulário adaptável.<br /> </p> </td>
  </tr>
  <tr>
   <td><p>sair </p> </td>
   <td><p>Esse script é executado no tempo de execução e não pode ser substituído no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>clique em (campos de botão)</p> </td>
   <td><p>Mapeado para a expressão Click do botão.</p> </td>
  </tr>
  <tr>
   <td><p>Suporte para script de servidor</p> </td>
   <td><p>Esse script é executado no tempo de execução e não pode ser substituído no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Suporte para serviços da Web</p> </td>
   <td><p>Esse script é executado no tempo de execução e não pode ser substituído no Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Alterar (campo de rabisco, botão de opção, caixa de seleção)</p> </td>
   <td><p>Esse script é executado no tempo de execução e não pode ser substituído no Formulário adaptável.</p> </td>
  </tr>
 </tbody>
</table>

### Validações {#validations}

A tabela a seguir captura como as validações XFA são mapeadas para validações no Adaptive Forms.

<table>
 <tbody>
  <tr>
   <td><p><strong>Validação de XFA</strong></p> </td>
   <td><p><strong>Validação correspondente no Formulário adaptável</strong></p> </td>
  </tr>
  <tr>
   <td><p>Padrão de validação (formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>Mensagem do padrão de validação (formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>Obrigatório (nullTest )</p> </td>
   <td><p>obrigatório </p> </td>
  </tr>
  <tr>
   <td><p>Mensagem vazia (nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>Validar script (scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>Mensagem do script de validação (scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Não é possível substituir a propriedade obrigatória pelo botão de opção Formulário adaptável e pelo grupo de caixas de seleção vinculados aos botões de seleção XFA.

