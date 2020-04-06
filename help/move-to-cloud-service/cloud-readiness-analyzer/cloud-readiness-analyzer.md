---
title: Avaliação da complexidade da mudança para o serviço em nuvem
description: Avaliação da complexidade da mudança para o serviço em nuvem
translation-type: tm+mt
source-git-commit: 83f7a1d57fae92e6ce15e4d9d6e00682d4596d05

---


# Avaliação da complexidade da mudança para o serviço em nuvem {#accesing-complexity}

## Visão geral {#overview}

O CRA (Cloud Readiness Analyzer) permite que você verifique as instâncias existentes do AEM quanto à prontidão para se mover para o serviço de nuvem detectando padrões que:

* Usar um recurso do AEM 6.x que não é suportado no momento no serviço em nuvem

* Violar certas regras que serão afetadas pela mudança para o serviço em nuvem

>[!NOTE]
>O resultado do CRA acelera a avaliação do esforço de desenvolvimento que será necessário para mudar para o serviço em nuvem.

## Configuração do Cloud Readiness Analyzer {#setting-up-cra}

O CRA é lançado como um pacote que funciona em qualquer versão de origem do AEM de XX e superiores, explorando uma mudança para o serviço de nuvem.

Ele está disponível no Portal de distribuição de software e pode ser instalado usando o Gerenciador de pacotes.

### Uso do Cloud Readiness Analyzer {#using-cra}

>[!NOTE]
> A CRA pode ser executada em qualquer ambiente, incluindo instâncias de desenvolvimento local.

>[IMPORTANTE]
>No entanto, para aumentar a taxa de detecção e evitar qualquer lentidão em instâncias críticas para os negócios, é recomendável executá-la em ambientes de armazenamento temporário tão próximos quanto possível dos de produção nas áreas de aplicativos, conteúdo e configurações do usuário

### Exibindo a Saída no Analisador de Prontidão da Nuvem {#viewing-output-cra}


1. Navegue até o console da Web do AEM navegando até Configuração **do console da Web do** Adobe Experience Manager usando `https://serveraddress:serverport/system/console/configMgr`.

1. Selecione Status - Analisador de prontidão para nuvem, conforme mostrado na imagem abaixo.

1. Você também pode visualização a saída por meio de uma interface JSON regular ou baseada em texto reativo.

>[!NOTE]
> Consulte o [Detector](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) de padrões para obter mais detalhes sobre esses métodos). É necessário adicionar esta seção quando o CRA estiver pronto para uso.

## Próximas etapas em prontidão para a nuvem {#the-next-steps}

Para obter mais informações sobre sua prontidão para o serviço em nuvem, a Adobe precisa avaliar a saída do CRA.

Siga as etapas abaixo para enviar o arquivo de volta:

1. Navegue até o console da Web do AEM e baixe o arquivo xx conforme mostrado na imagem abaixo.

1. Abra um ticket do DayCare para enviar o arquivo para a Adobe ao:
   1. Registrando um ticket de suporte no Daycare intitulado como Saída do Analisador de prontidão **da nuvem**
   1. Anexar um arquivo de saída ao ticket

