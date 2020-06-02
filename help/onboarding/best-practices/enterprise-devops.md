---
title: Enterprise DevOps
description: Saiba mais sobre os processos, os métodos e a comunicação necessários para facilitar a implantação e simplificar a colaboração.
translation-type: tm+mt
source-git-commit: 5fe4eb9f9cad4ad2f1d259ebb5fa0302ea5c515f
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# Enterprise DevOps{#enterprise-devops}

DevOps abrange os processos, métodos e comunicações necessários para:

* Facilite a implantação do software em vários ambientes.
* Simplifique a colaboração entre as equipes de desenvolvimento, teste e implantação.

DevOps visa evitar problemas como:

* Erros manuais.
* Elementos esquecidos; por exemplo, arquivos, detalhes de configuração.
* Discrepâncias; por exemplo, entre o ambiente local de um desenvolvedor e outros ambientes.

## Ambientes {#environments}

O Adobe Experience Manager (AEM) como um serviço em nuvem geralmente consiste em vários ambientes, usados para propósitos diferentes em níveis diferentes:

* [Desenvolvimento](#development)
* [Garantia de qualidade](#quality-assurance)
* [Estágios](#staging)
* [Produção](#production-author-and-publish)

>[!NOTE]
>
>O ambiente de produção deve ter pelo menos um autor e um ambiente de publicação.
>
>Recomenda-se que todos os outros ambientes também consistam em um autor e um ambiente de publicação para refletir o ambiente de produção e permitir testes iniciais.

### Desenvolvimento {#development}

Os desenvolvedores são responsáveis por desenvolver e personalizar o projeto proposto (seja site, aplicativos móveis, implementação de DAM etc.), com toda a funcionalidade necessária. Eles:

* Desenvolver e personalizar os elementos necessários; por exemplo, modelos, componentes, workflows, aplicativos
* realizar o design
* desenvolver os serviços e scripts necessários para implementar a funcionalidade necessária

A configuração do ambiente de [desenvolvimento](/help/implementing/developing/introduction/development-guidelines.md) pode depender de vários fatores, embora geralmente seja composta de:

* Um sistema de desenvolvimento integrado com controle de versão para fornecer uma base de código integrada. Isso é usado para unir e consolidar o código dos ambientes de desenvolvimento individuais usados por cada desenvolvedor.
* Um ambiente pessoal para cada desenvolvedor; geralmente residentes na sua máquina local. Em intervalos adequados, o código é sincronizado com o sistema de controle de versão

Dependendo da escala do seu sistema, o ambiente de desenvolvimento pode ter instâncias de autor e publicação.

### Garantia de qualidade {#quality-assurance}

Este ambiente é usado pela equipe de garantia de qualidade para testar o novo sistema de forma abrangente; design e função. Ele deve ter ambientes de autor e publicação, com conteúdo adequado, e fornecer todos os serviços necessários para habilitar um conjunto completo de testes.

### Estágios {#staging}

O ambiente de preparo deve ser um espelho do ambiente de produção - configuração, código e conteúdo:

* É usado para testar os scripts usados para implementar a implantação real.
* Ele pode ser usado para testes finais (design, funcionalidade e interfaces) antes da implantação para os ambientes de produção.
* Embora nem sempre seja possível ter o ambiente de preparo idêntico ao ambiente de produção, deve ser o mais próximo possível para permitir o teste de desempenho e carga.

### Produção - Autor e publicação {#production-author-and-publish}

O ambiente de produção consiste nos ambientes necessários para [criar e publicar](/help/sites-cloud/authoring/getting-started/concepts.md) sua implementação.

Um ambiente de produção consiste em pelo menos uma instância do autor e uma instância de publicação:

* Uma instância de [criação](#author) para a entrada de conteúdo.
* Uma instância de [publicação](#publish) para conteúdo disponibilizado para seus visitantes/usuários.

Dependendo da escala do projeto, ele geralmente consiste em várias instâncias de autor e/ou publicação. Em um nível inferior, o repositório também pode ser agrupado em várias instâncias.

#### Autor {#author}

As instâncias do autor normalmente estão localizadas atrás do firewall interno. Este é o ambiente no qual você e seus colegas farão tarefas de criação, como:

* administrar todo o sistema
* inserir seu conteúdo
* configurar o layout e o design do seu conteúdo
* ativar seu conteúdo no ambiente de publicação

O conteúdo que foi ativado é empacotado e colocado na fila de replicação do ambiente do autor. O processo de replicação transporta esse conteúdo para o ambiente de publicação.

Para reverter a replicação de dados gerados em um ambiente de publicação de volta ao ambiente do autor, um ouvinte de replicação no ambiente do autor sondará o ambiente de publicação e recuperará esse conteúdo da caixa de saída de replicação reversa do ambiente de publicação.

#### Publicação {#publish}

Um ambiente de publicação geralmente está localizado na Zona desmilitarizada (DMZ). Este é o ambiente no qual os visitantes acessarão seu conteúdo (por exemplo, através de um site ou na forma de um aplicativo móvel) e interagirão com ele; seja público, ou dentro da sua intranet. Um ambiente de publicação:

* contém conteúdo replicado do ambiente do autor
* disponibiliza esse conteúdo para os visitantes
* armazena dados do usuário gerados por seus visitantes, como comentários ou outros envios de formulário
* pode ser configurado para adicionar esses dados de usuário a uma caixa de saída, para replicação reversa de volta ao ambiente do autor

O ambiente publish gera seu conteúdo dinamicamente em tempo real e o conteúdo pode ser personalizado para cada usuário individual.

## Movimento de código {#code-movement}

O código deve ser sempre propagado de baixo para cima:

* o código é inicialmente desenvolvido nos ambientes de desenvolvimento local e depois integrado
* seguido de testes minuciosos no(s) ambiente(s) de garantia da qualidade
* e testados novamente nos ambientes de preparo
* só então o código deve ser implantado nos ambientes de produção

O código (por exemplo, funcionalidade personalizada do aplicativo da Web e modelos de design) é transferido normalmente pela exportação e importação de pacotes entre os diferentes repositórios de conteúdo. Quando significativa, essa replicação pode ser configurada como um processo automático.

O AEM como um projeto de serviço em nuvem geralmente aciona a implantação do código:

* Automaticamente: para transferência para os ambientes de desenvolvimento e controle de qualidade.
* Manualmente: as implementações nos ambientes de armazenamento temporário e de produção são efetuadas de forma mais controlada, muitas vezes manual; embora a automação seja possível, se necessário.

![Movimento de código](assets/code-movement.png)

## Movimento de conteúdo {#content-movement}

O conteúdo que está sendo criado para produção deve ser **sempre** criado na instância do autor da produção.

O conteúdo não deve seguir a mudança de código de ambientes inferiores para superiores, já que fazer com que os autores criem conteúdo em máquinas locais ou ambientes menores e, em seguida, movê-lo para o ambiente de produção não é uma boa prática e provavelmente introduzirá erros e inconsistências.

O conteúdo de produção deve ser movido do ambiente de produção para o ambiente de preparo para garantir que o ambiente de preparo forneça um ambiente de teste eficiente e preciso.

>[!NOTE]
>
>Isso não significa que o conteúdo temporário precisa ser sincronizado continuamente com a produção, atualizações regulares são suficientes, mas especialmente antes de testar uma nova iteração do código. O conteúdo dos ambientes de controle de qualidade e desenvolvimento não precisa ser atualizado com a mesma frequência, deve ser apenas uma boa representação do conteúdo de produção.

O conteúdo pode ser transferido:

* Entre os diferentes ambientes - exportando e importando pacotes.
* Entre instâncias diferentes - replicando diretamente (AEM como uma replicação do serviço de nuvem) o conteúdo (usando uma conexão HTTP ou HTTPS).

![Movimento de conteúdo](assets/content-movement.png)