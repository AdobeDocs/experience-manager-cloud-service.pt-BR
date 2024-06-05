---
title: Desenvolvimento de Sites com o pipeline front-end
description: Com o pipeline de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ganhar velocidade substancial. Este documento descreve algumas considerações específicas do processo de build de front-end que devem ser fornecidas.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---


# Desenvolvimento de Sites com o pipeline front-end {#developing-site-with-front-end-pipeline}

[Com o pipeline de front-end,](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) mais independência é dada aos desenvolvedores de front-end e o processo de desenvolvimento pode ganhar velocidade substancial. Este documento descreve como esse processo funciona, além de algumas considerações a serem levadas em conta para que você possa aproveitar ao máximo o potencial desse processo.

>[!TIP]
>
>Se você ainda não estiver familiarizado com o uso do pipeline de front-end e com os benefícios que ele pode trazer, verifique a [Jornada de criação rápida de site](/help/journey-sites/quick-site/overview.md) para obter um exemplo de como implantar rapidamente um novo site e personalizar seu tema completamente independente do desenvolvimento de back-end.

## Contrato de Build de Front-End {#front-end-build-contract}

Semelhante ao [ambiente de build de pilha completa,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) o pipeline de front-end tem seu próprio ambiente. Os desenvolvedores têm alguma flexibilidade ao usar esse pipeline, desde que o seguinte contrato de build de front-end seja observado.

O pipeline de front-end requer o projeto Node.js de front-end para usar o `build` diretiva de script para gerar o build implantado. Isso ocorre porque o Cloud Manager usa o comando `npm run build` para gerar o projeto implantável para a build de front-end.

O conteúdo resultante da variável `dist` pasta é o que é implantado por fim pelo Cloud Manager, servindo-os como arquivos estáticos. Esses arquivos são hospedados externamente para AEM, mas são disponibilizados por meio de um `/content/...` URL no ambiente implantado.

## Versões do nó {#node-versions}

O ambiente de build de front-end é compatível com as seguintes versões do Node.js.

* 12
* 14 (padrão)
* 16
* 18

Você pode usar o `NODE_VERSION` [variável de ambiente](/help/implementing/cloud-manager/environment-variables.md) para definir a versão desejada.

## Única fonte da verdade {#single-source-of-truth}

Uma boa prática geral é manter uma única fonte de verdade para o que é implantado no AEM. O objetivo do Cloud Manager é tornar essa única fonte de verdade óbvia. No entanto, como o pipeline de front-end permite a dissociação da localização de partes do código, alguma responsabilidade adicional reside na configuração correta dos pipelines de front-end. Deve-se ter cuidado para não criar vários pipelines de front-end que são implantados no mesmo site no mesmo ambiente.

Por isso, e especialmente quando vários pipelines de front-end são criados, é recomendável manter uma convenção de nomenclatura sistemática, como a seguinte:

* O nome do módulo de front-end, definido pela variável `name` propriedade do `package.json` arquivo, deve conter o nome do site ao qual se aplica. Por exemplo, para um site localizado em `/content/wknd`, o nome do módulo de front-end seria algo como `wknd-theme`.
* Quando um módulo de front-end compartilha o mesmo repositório Git com outros módulos, o nome da pasta deve ser igual ou conter o mesmo nome do módulo de front-end. Por exemplo, se o módulo de front-end for nomeado como `wknd-theme`, o nome da pasta de delimitação seria algo como `wknd-theme-sources`.
* O nome do pipeline de front-end do Cloud Manager também deve conter o nome do módulo de front-end e adicionar o ambiente no qual ele é implantado (produção ou desenvolvimento). Por exemplo, para o módulo de front-end chamado `wknd-theme`, o pipeline pode ser nomeado como algo como `wknd-theme-prod`.

Essa convenção deve evitar com eficiência os seguintes erros de implantação:

* Aplicando um módulo front-end ao site errado
* Criar vários módulos de front-end que apliquem o mesmo site, os quais se substituiriam
* Criar vários pipelines de front-end para as mesmas fontes, o que pode causar condições de corrida, não garantindo a ordem das implantações

## Separação de problemas {#separation-of-concerns}

Outra boa prática que se aplica a qualquer separação de interesses é colocar um cuidado especial na forma como o contrato que separa as preocupações é projetado e gerenciado. No caso do pipeline de front-end, o contrato que separa esse código do restante é o HTML e o JSON renderizados pelo site. Se esse HTML e o JSON permanecerem estáveis, o pipeline de front-end fornecerá seu valor máximo, tornando a equipe de front-end totalmente independente.

No momento, não há nenhum recurso específico para executar o pipeline de pilha completa de forma síncrona com os pipelines de front-end. Por isso, ao dissociar o desenvolvimento de front-end do pipeline de pilha completa, deve-se ter cuidado extra no contrato que separa essas duas áreas de preocupação. Esse contrato geralmente é o HTML e/ou JSON que o Experience Manager renderiza. Por conseguinte, as alterações a esse contrato devem ser bem planejadas entre as equipes que exploram os diferentes gasodutos, para que cheguem a acordo sobre a forma de sequenciar as alterações correspondentes.

As etapas a seguir são geralmente recomendadas quando é necessário executar alterações na saída de HTML e/ou JSON que afetam ambas as áreas de interesse.

1. A equipe de back-end primeiro configura um ambiente de desenvolvimento com a nova saída de HTML e/ou JSON.
   1. Por meio do pipeline de pilha completa, eles implantam o código necessário para renderizar a nova saída de HTML e/ou JSON desejada.
   1. Se isso se refere a um ambiente ao qual a equipe de front-end não tinha acesso anteriormente, as etapas a seguir devem ser executadas.
      1. URL: a equipe de front-end deve saber o URL desse ambiente de desenvolvimento.
      1. ACL: a equipe de front-end deve receber um usuário local do AEM com algo semelhante aos direitos de &quot;Contribuidores&quot;.
      1. Git: a equipe de front-end deve ter um local Git separado para o módulo de front-end que direciona especificamente esse ambiente de desenvolvimento.
         * Uma prática comum é criar um `dev` para que as alterações feitas no ambiente de desenvolvimento possam ser facilmente mescladas com o `main` que será implantada no ambiente de produção.
      1. Pipeline: a equipe de front-end deve ter um pipeline de front-end que seja implantado no ambiente de desenvolvimento. Esse pipeline implantaria o módulo de front-end que normalmente está localizado no `dev` como descrito no ponto anterior.
1. A equipe de front-end faz com que o código CSS e JS funcione com a saída antiga e a nova.
   1. Como de costume, desenvolver localmente:
      1. A variável `npx aem-site-theme-builder proxy` comando executado no módulo de front-end inicia um servidor proxy que solicita o conteúdo de um ambiente AEM, enquanto substitui os arquivos CSS e JS do módulo de front-end pelos do ambiente local `dist` pasta.
      1. Configuração do `AEM_URL` na variável oculta `.env` O arquivo permite controlar de qual ambiente AEM o servidor proxy local consome o conteúdo.
      1. Alterar o valor desse `AEM_URL` portanto, permite alternar entre os ambientes de produção e desenvolvimento para ajustar o CSS e o JS para que se encaixem em ambos os ambientes.
      1. Ele deve funcionar com o ambiente de desenvolvimento que renderiza a nova saída e com o ambiente de produção que renderiza a saída antiga.
   1. O trabalho de front-end é concluído quando o módulo de front-end atualizado funciona para ambos os ambientes e é implantado em ambos.
1. A equipe de back-end pode atualizar o ambiente de produção implantando o código que renderiza a nova saída de HTML e/ou JSON por meio do pipeline de pilha completa.
1. A equipe de front-end pode então limpar o CSS e o JS e remover o que era necessário somente para a saída antiga, implantando a última atualização na produção por meio do pipeline de front-end.

## Recursos adicionais {#additional-resources}

* [Temas do site](/help/sites-cloud/administering/site-creation/site-themes.md) - Saiba como temas de site AEM podem ser usados para personalizar o estilo e o design do site.
* [Criador de temas de site do AEM](https://github.com/adobe/aem-site-theme-builder) - O Adobe fornece um Criador de temas de site AEM como um conjunto de scripts para criar novos temas de site.
