---
title: Criar tabela dinâmica no Editor de comunicação interativa
description: Criar o recurso de Tabela dinâmica que permite aos autores criar tabelas orientadas por dados.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
source-git-commit: 322183c28719db5b8657d9532ef234e1d18821cd
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Criar tabela dinâmica no Editor de comunicação interativa

## Visão geral

O Editor de comunicação interativa fornece uma tabela dinâmica
recurso que permite que os autores criem tabelas orientadas por dados cujo conteúdo é preenchido automaticamente no tempo de execução a partir de fontes de dados estruturadas.

Diferentemente das tabelas estáticas, em que as linhas devem ser criadas manualmente, as tabelas dinâmicas expandem ou contraem automaticamente com base nos registros retornados de uma fonte de dados vinculada. Isso os torna úteis para cenários como demonstrativos de faturamento, históricos de transações, listas de produtos ou programações de políticas.

Este artigo explica como inserir e configurar uma tabela dinâmica com vinculação de dados, gerenciar fluxo de tabela de várias páginas e validar contagens de linhas.

## Inserir uma Tabela Dinâmica

1. Abra o **Editor de Comunicação Interativa**.
1. No **painel Componente**, arraste o **componente Tabela** para o
tela.
1. Especifique o **número de colunas** e as **linhas iniciais** na caixa de diálogo, verifique se a **linha de cabeçalho** está incluída e clique em OK para criar a tabela.

### Vincular dados à tabela dinâmica

As tabelas dinâmicas preenchem linhas automaticamente ao vincular a uma fonte de dados repetível.

![Localizar IC Docu](/help/forms/interactive-communication/assets/databinding-in-table.png)

Para vincular dados à tabela:

1. Selecione a **linha de tabela** no painel de hierarquia.

1. Abra a **Associação de Dados** no painel lateral.

1. Verifique se o esquema de dados selecionado é do tipo matriz.

1. Arraste e solte o esquema de dados de matriz na linha de tabela selecionada para vincular os dados.

### Ativar fluxo de página

As tabelas dinâmicas podem se expandir além de uma única página. Para permitir que a tabela cresça e continue entre páginas, coloque-a dentro de um contêiner de **Conteúdo Fluxado**.

![Localizar IC Docu](/help/forms/interactive-communication/assets/table-data-binding.png)

Para habilitar o fluxo de página:

1. Selecione o **contêiner de layout pai** da tabela.

1. Abra o painel Propriedades e defina o Tipo de Conteúdo como **Fluxo**.

1. Selecione a tabela e verifique se ela também está configurada para suportar conteúdo fluído.

1. Visualize a comunicação para verificar se a tabela continua na próxima página à medida que linhas adicionais são renderizadas.

### Permitir Quebra De Página Na Tabela

![Localizar IC Docu](/help/forms/interactive-communication/assets/table-data-binding.png)

Para garantir que a tabela se divida corretamente entre páginas:

1. Selecione a **tabela** na tela.
1. Abra o painel **Propriedades**.
1. Habilitar **Permitir Quebra De Página No Conteúdo**.

Quando ativada, a tabela é quebrada automaticamente no final de uma página e continua na página seguinte, com a linha de cabeçalho repetida.

### Configurar Validação de Linha

Você pode controlar quantas linhas a tabela dinâmica pode renderizar.

* **Mínimo de linhas:** garante que a tabela renderize pelo menos o número especificado de linhas.
* **Máximo de Linhas:** Limita o total de linhas renderizadas da fonte de dados.
* **Linhas iniciais:** Define quantas linhas aparecem no editor durante a visualização em tempo de design.

>[!NOTE]
>
> A definição de **Linhas Iniciais** como aproximadamente **3-5** fornece uma visualização de layout mais realista antes da aplicação dos dados de tempo de execução.

## Principais recursos

* Vinculação de dados da coluna: vincula cada coluna a um campo no modelo de dados.

* Conteúdo fluido: permite que a tabela se expanda e continue nas páginas.

* Suporte para quebra de página: permite quebras de página em nível de linha na tabela.

* Mínimo de linhas: garante que um número mínimo de linhas seja renderizado.

* Máximo de linhas: limita o total de linhas renderizadas na fonte de dados.

* Linhas iniciais: define as linhas padrão mostradas durante a visualização em tempo de design.

O recurso Tabela dinâmica no Editor de comunicação interativa permite que os autores criem tabelas flexíveis orientadas por dados sem escrever código personalizado. Vinculando a tabela a um array de dados, permitindo o Fluxo de conteúdo, permitindo quebras de página e configurando a validação de linhas, os autores podem produzir comunicações estruturadas que se adaptam sem problemas a volumes variáveis de dados, mantendo um layout consistente.
