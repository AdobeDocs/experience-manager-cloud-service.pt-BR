---
title: Criar um fragmento de comunicação interativa
description: Crie fragmentos de comunicação interativa no AEM Forms para criar blocos de conteúdo modulares e reutilizáveis que garantam consistência, economizem tempo e sejam compatíveis com comunicações personalizadas orientadas por dados.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Vinculação de dados no Editor de comunicações interativas

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

A vinculação de dados no Editor de comunicações interativas conecta campos na tela com uma camada de dados controlada para que as comunicações sejam renderizadas com informações reais e contextuais. Vinculando componentes a um Modelo de dados de formulário (FDM) ou a uma carga global, os autores podem garantir a precisão, reduzir o trabalho manual e fornecer experiências dinâmicas e personalizadas.

Além de simplesmente conectar valores, o Vínculo de dados na IC suporta mapeamento visual, preenchimento prévio e sincronização, permitindo que os autores criem mais rápido e, ao mesmo tempo, permaneçam alinhados aos sistemas de back-end e aos modelos de dados.

## &#x200B;2. Propriedades

2.1 Gerenciamento de conexões de dados (FDM)

- **Selecionar o FDM:** Escolha o Modelo de Dados de Formulário apropriado (por exemplo, clientes, contas ou políticas). Isso estabelece o esquema autoritativo para campos, matrizes e objetos usados na comunicação.

- **Criando Associações de Dados:** depois que as associações estiverem habilitadas, cada campo poderá ser associado a caminhos do FDM, minimizando erros e garantindo uma integração consistente.

- **Associando Campos aos Modelos de Dados:** Aponte campos para nós específicos (por exemplo, customer.name, policy.holder.id) para direcionar a renderização com dados dinâmicos e oferecer suporte a validações ou lógica condicional.

2.2 Criação de Associações de Dados

- **Mapeamento Visual:** o mapeamento de arrastar e soltar entre campos e nós do FDM ajuda usuários não técnicos a evitar erros.

- **Associação de Campo:** Defina o caminho de destino, o tipo de dados (texto, número, data, booleano, imagem) e os formatadores opcionais (por exemplo, máscara de data, moeda).

- **Visualização da associação:** teste as associações com conjuntos de dados de exemplo para validar a formatação e a correção antes de publicar.

2.3 Vincular campos a modelos de dados

- **Mapeamento de Campos:** Vincule texto, imagem ou estruturas repetidas (tabelas/listas) com os nós FDM corretos. As coleções podem usar fontes de iteração e linhas de modelo.

- **Sincronização de Dados:** Escolha uma via (interface de usuário preenchida a partir do modelo) ou duas vias (entradas de usuário salvas de volta no modelo).

- **Preenchimento prévio:** Use valores padrão do modelo ou expressões para simplificar a entrada de dados e melhorar a precisão.

## &#x200B;3. Utilização

A Vinculação de dados geralmente é usada quando as comunicações precisam exibir registros autoritativos ou capturar entradas do usuário. Por exemplo:

- **Personalization:** preencha os detalhes do cliente como nome, endereço ou saldo da conta.

- **Conteúdo Condicional:** Mostrar/ocultar seções com base nos valores do modelo (por exemplo, clientes ativos vs. inativos).

- **Coleções e Tabelas:** Renderiza históricos, transações ou listas discriminadas de matrizes.

- **Imagens e Mídia:** Associe fotos de perfil, logotipos de empresa ou imagens de produto.

- **Revisar e assinar eletronicamente:** Preencher formulários previamente com dados e permitir atualizações por meio de sincronização bidirecional.

Normalmente, os autores selecionam o FDM no início do projeto, mapeiam visualmente os campos durante o design e testam com dados de amostra antes da publicação.

## &#x200B;4. Práticas recomendadas

- **Definir esquema antecipadamente:** Finalize o FDM antes da associação para evitar o remapeamento mais tarde.

- **Usar mapeamento visual:** evite erros de digitação e caminhos incompatíveis ao depender do recurso arrastar e soltar.

- **Validar tipos de dados:** aplique formatadores de moeda, datas ou números de telefone para garantir a consistência.

- **Manter associações explícitas:** Cada campo deve mapear claramente para um único nó de dados.

- **Teste com dados de exemplo:** Visualize casos comuns e de borda (por exemplo, valores vazios, matrizes longas).

- **Limitar sincronização bidirecional:** use apenas quando edições ou aprovações forem necessárias.

- **Modular coleções:** Use linhas de modelo para estruturas repetíveis.

- **Proteger dados confidenciais:** Aplique mascaramento, criptografia e acesso de menor privilégio a PII ou detalhes de pagamento.

Ao configurar a Vinculação de dados cuidadosamente, os autores criam uma ponte confiável entre o design e os dados, acelerando a criação de comunicações, garantindo a precisão e fornecendo experiências altamente personalizadas em escala.