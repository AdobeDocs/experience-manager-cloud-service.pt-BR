---
title: Subformulário no Editor de comunicação interativa
description: Subformulário no Editor de comunicação interativa gerencie layouts, controle o posicionamento de objetos e defina como o conteúdo flui pelas páginas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Subformulário no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

## &#x200B;1. Introdução

Um Subformulário no Editor de comunicação interativa é um objeto de contêiner usado para agrupar campos, objetos e componentes em uma seção lógica. Ele ajuda a gerenciar layouts, controlar o posicionamento de objetos e definir como o conteúdo flui entre páginas. Os subformulários são essenciais para criar comunicações estruturadas, reutilizáveis e responsivas, especialmente ao lidar com conteúdo dinâmico ou repetido.

Ao usar subformulários, os autores podem manter a consistência, gerenciar a paginação e vincular seções inteiras a fontes de dados estruturados.

## &#x200B;2. Propriedades

Layouts de design do formulário 2.1

- **Layout Fixo:** Os objetos mantêm posições exatas na página. Melhor para designs estáticos nos quais a disposição de precisão é necessária (por exemplo, faturas ou cartas oficiais).

- **Layout fluível:** Os objetos são ajustados dinamicamente com base no comprimento do conteúdo e no tamanho da tela. Adequado para comunicações que exigem design responsivo ou comprimentos de dados variáveis.

2.2 Posicionamento do subformulário

- **Paginação:** Controle como os subformulários quebram entre páginas. As opções incluem manter os subformulários juntos ou permitir quebras de página neles.

- **Posição:** especifique se o subformulário é colocado em relação ao seu container pai ou se flui naturalmente dentro do layout.

- **Aparência:** Defina o plano de fundo, as bordas e o estilo do subformulário para separar visualmente o conteúdo.

- **Presença:** Defina as configurações de visibilidade — Visível, Oculto ou Condicional — dependendo das regras de negócios ou dos valores de dados.

2.3 Vinculação de dados

- Os subformulários podem ser vinculados diretamente aos nós ou matrizes do **Modelo de Dados de Formulário (FDM)**.

- A vinculação permite que o subformulário seja repetido dinamicamente para cada registro em uma coleção (por exemplo, várias políticas, transações ou endereços).

- Aceita preenchimento estático e dinâmico de conteúdo com base na estrutura de dados.

## &#x200B;3. Utilização

Os subformulários são amplamente usados para:

- Estruturar documentos em seções como cabeçalho, corpo e rodapé.

- Repetição de conteúdo, como tabelas, listas discriminadas ou listas de políticas.

- Gerenciamento de paginação para que o conteúdo agrupado permaneça unido.

- Exibição condicional de seções com base em regras ou valores de dados.

- Aplicar controle de layout (fixo ou fluível) dependendo do tipo de comunicação.

Os autores podem arrastar um subformulário da Biblioteca de objetos para a tela e ajustar seu layout, posicionamento e vínculo no Painel Propriedades.

## &#x200B;4. Práticas recomendadas

- **Escolha o layout com sabedoria:** Use o layout fixo para formulários que exigem posicionamento exato e o layout fluível para comunicações dinâmicas orientadas por dados.

- **Associe as coleções com cuidado:** Para listas ou matrizes, associe os subformulários diretamente às coleções do FDM com linhas de modelo.

- **Otimizar paginação:** evite quebras estranhas agrupando objetos relacionados em um subformulário.

- **Usar presença condicional:** Ocultar ou exibir subformulários dinamicamente com base em valores de dados.

- **Manter hierarquia:** aninha subformulários logicamente para facilitar o gerenciamento de layouts complexos.

- **Testar com dados variados:** Visualizar com conjuntos de dados curtos, longos e vazios para garantir que o design se adapte corretamente.

Ao utilizar os Subformulários de maneira eficaz, os autores podem obter layouts mais limpos, melhor controle sobre o conteúdo dinâmico e garantir que as comunicações se adaptem perfeitamente a cenários orientados por dados e estáticos.
