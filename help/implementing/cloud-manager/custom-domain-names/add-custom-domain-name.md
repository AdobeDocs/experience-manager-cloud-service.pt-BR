---
title: Adicionar um nome de domínio personalizado
description: Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2d1382c84d872719332986baa5829d1623d9d9a6
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 18%

---


# Adicionar um nome de domínio personalizado {#adding-cdn}

Saiba como adicionar um nome de domínio personalizado usando o Cloud Manager.

## Requisitos {#requirements}

Atenda a esses requisitos antes de adicionar um nome de domínio personalizado no Cloud Manager.

* Você deve ter adicionado um certificado SSL para o domínio que deseja adicionar antes de adicionar um nome de domínio personalizado, conforme descrito no documento [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Você deve ter a função de **Proprietário da empresa** ou **Gerente de implantação** para adicionar um nome de domínio personalizado no Cloud Manager.
* Estar usando o Fastly ou outro CDN (Content Delivery Network).

>[!IMPORTANT]
>
>Mesmo se você usar um CDN não Adobe, ainda precisará adicionar seu domínio ao Cloud Manager.

## Onde adicionar nomes de domínio personalizados {#where-to-add-cdn}

Você pode adicionar um nome de domínio personalizado a partir dos dois locais a seguir no Cloud Manager:

* [Página Configurações do domínio](#adding-cdn-settings)
* [Página Ambientes](#adding-cdn-environments)

Ao adicionar um nome de domínio personalizado, o domínio é distribuído usando o certificado mais específico e válido. Se vários certificados tiverem o mesmo domínio, o mais recente atualizado será escolhido. A Adobe recomenda que você gerencie certificados de forma que não haja domínios sobrepostos.

As etapas para qualquer método descrito neste documento são baseadas no Fastly. Se você usou uma CDN (Content Delivery Network) diferente, configure seu domínio com a CDN que você escolheu usar.

## Adicionar um nome de domínio personalizado {#adding-cdn-settings}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. No menu lateral, em **Serviços**, selecione **Configurações de Domínio**.

   ![A janela Configurações do domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Próximo ao canto superior direito da página **Configurações de Domínio**, clique em **Adicionar Domínio**.

1. Na caixa de diálogo **Adicionar domínio**, no campo **Nome do Domínio**, digite o nome de domínio personalizado que você está usando.
Não inclua `http://`, `https://` ou espaços ao inserir seu domínio.

1. Clique em **Criar**.

1. Na caixa de diálogo **Verificar Domínio**, em **Que tipo de certificado você pretende usar com este domínio?**, selecione uma das seguintes opções:

   | Opção Tipo de certificado | Descrição |
   | --- | --- |
   | Certificado gerenciado pela Adobe | Selecione se quiser usar um certificado DV (Domain Validation). Essa opção é ideal para a maioria dos casos, fornecendo validação básica de domínio. O Adobe gerencia e renova o certificado automaticamente. |
   | Certificado gerenciado pelo cliente | Selecione se quiser usar um certificado EV/OV. Essa opção oferece segurança aprimorada com EV (Extended Validation) ou OV (Organization Validation). Use se uma verificação mais rigorosa, níveis de confiança mais altos ou controle personalizado dos certificados for necessário. |

1. Na caixa de diálogo **Verificar domínio**, com base no tipo de certificado selecionado, siga um destes procedimentos:

   | Se você selecionou o tipo de certificado | Descrição |
   | --- | ---  |
   | Certificado gerenciado pela Adobe | Conclua as [etapas de certificado gerenciado por Adobe](#adobe-managed-cert-steps) antes de prosseguir para a próxima etapa. |
   | Certificado gerenciado pelo cliente | Conclua as [etapas de certificado gerenciado pelo cliente](#customer-managed-cert-steps) antes de prosseguir para a próxima etapa. |

1. Clique em **Verificar**.

1. Agora você está pronto para [adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

   >[!NOTE]
   >
   >Se você usar um certificado SSL autogerenciado e um provedor CDN autogerenciado, ignore esta etapa e vá diretamente para [Adicionar uma configuração de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) quando estiver pronto.


### Etapas do certificado gerenciado por Adobe {#adobe-managed-cert-steps}

Se você selecionou o tipo de certificado *Adobe managed certificate*, conclua as etapas a seguir na caixa de diálogo **Verificar domínio**.

![etapas de certificado gerenciado Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Para verificar o domínio em uso, é necessário adicionar e verificar um CNAME.

Um registro `CNAME` ou A, uma vez provisionado, roteia todo o tráfego de Internet do domínio para onde quer que esteja apontando. Se esse local não for provisionado para veicular o tráfego, haverá uma interrupção. Se não for testado, poderá haver erros no conteúdo. É por isso que essa etapa é sempre realizada após a conclusão dos testes, quando você está pronto para entrar em produção.

Para definir essas configurações, determine se um registro `CNAME` ou apex deve ser configurado para apontar seu nome de domínio personalizado para o nome de domínio do Cloud Manager. As seções a seguir deste documento podem ajudar você a determinar qual tipo de registro é apropriado para sua configuração de DNS.

>[!NOTE]
>
>Para CDNs gerenciadas por Adobe, ao usar certificados DV (Domain Validation, validação de domínio), somente sites com validação ACME são permitidos.

#### Requisitos {#adobe-managed-cert-dv-requirements}

Atenda a esses requisitos antes de configurar seus registros DNS.

* Identifique o host ou o registrador do seu domínio, se você ainda não o conhece.
* Ser capaz de editar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa apropriada que pode fazer isso.
* Você já deve ter verificado o nome de domínio personalizado configurado, conforme descrito no documento [Verificando o Status do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

#### Registro CNAME {#adobe-managed-cert-cname-record}

Um nome canônico ou registro CNAME é um tipo de registro DNS que mapeia um nome de alias a um nome de domínio verdadeiro ou canônico. Os registros CNAME normalmente são usados para mapear um subdomínio como `www.example.com` ao domínio que hospeda o conteúdo desse subdomínio.

Faça logon no provedor de serviços DNS e crie um registro `CNAME` para apontar seu nome de domínio personalizado ao destino, como na tabela a seguir.

| CNAME | Domínio personalizado - apontar para o destino |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### Registro APEX {#adobe-managed-cert-apex-record}

Um domínio apex é um domínio personalizado que não contém um subdomínio, como `example.com`. Um domínio apex é configurado com um registro `A`, `ALIAS` ou `ANAME` por meio do provedor de DNS. Domínios apex devem apontar para endereços IP específicos.

Adicione os seguintes registros `A` às configurações de DNS do domínio por meio do provedor de domínio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`


### Etapas de certificado gerenciado pelo cliente {#customer-managed-cert-steps}

Se você selecionou o tipo de certificado *Certificado gerenciado pelo cliente*, conclua as etapas a seguir na caixa de diálogo **Verificar domínio**.

![Etapas de certificado gerenciado pelo cliente](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

Para verificar o domínio em uso, é necessário adicionar e verificar um registro TXT.

Um registro de texto (também conhecido como registro TXT) é um tipo de registro de recurso no Sistema de nomes de domínio (DNS). Permite associar texto arbitrário a um nome de host. Esse texto pode incluir detalhes legíveis por humanos, como informações do servidor ou da rede.

O Cloud Manager usa um registro TXT específico para autorizar que um domínio seja hospedado em um serviço CDN. Crie um registro TXT de DNS na zona que autoriza o Cloud Manager a implantar o serviço CDN no domínio personalizado e associá-lo ao serviço de back-end. Essa associação está totalmente sob seu controle e autoriza o Cloud Manager a veicular conteúdo do serviço em um domínio. Esta autorização pode ser concedida e retirada. O registro TXT é específico do domínio e do ambiente Cloud Manager.

#### Requisitos {#customer-managed-cert-requirements}

Atenda a esses requisitos antes de adicionar um registro TXT.

* Identifique o host ou o registrador do seu domínio, se você ainda não o conhece.
* Ser capaz de editar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa apropriada que pode fazer isso.
* Primeiro, adicione um nome de domínio personalizado conforme descrito anteriormente neste artigo.

#### Adicionar um registro TXT para verificação {#customer-managed-cert-verification}

1. Na caixa de diálogo **Verificar domínio**, o Cloud Manager exibe o nome e o valor TXT a serem usados para verificação. Copie este valor.

1. Faça logon no provedor de serviços DNS e localize a seção Registros DNS.

1. Adicione `aemverification.[yourdomainname]` como o **Nome** do valor e adicione o valor TXT exatamente como ele aparece no campo **Nome do Domínio**.

   **Exemplos de registros TXT**

   | Domínio | Nome | Valor TXT |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copie todo o valor exibido na interface do Cloud Manager. Esse valor é específico do domínio e do ambiente. Por exemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copie todo o valor exibido na interface do Cloud Manager. Esse valor é específico do domínio e do ambiente. Por exemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Salve o registro TXT no host do domínio.

#### Verificar registro TXT {#customer-managed-cert-verify}

Quando terminar, você poderá verificar o resultado executando o comando a seguir.

```shell
dig _aemverification.[yourdomainname] -t txt
```

O resultado esperado deve exibir o valor TXT fornecido na guia **Verificação** da caixa de diálogo **Adicionar nome de domínio** da interface do usuário do Cloud Manager.

Por exemplo, se o domínio for `example.com`, execute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Há várias [ferramentas de pesquisa de DNS](https://www.ultratools.com/tools/dnsLookup) disponíveis. O Google DoH pode ser usado para pesquisar entradas de registro TXT e identificar se o registro TXT está ausente ou incorreto.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verifica a propriedade e atualiza o status, que pode ser visto na tabela Configurações do domínio. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>A entrada TXT e o registro CNAME ou A podem ser definidos simultaneamente no servidor DNS regulador, economizando tempo.
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## Adicione um nome de domínio personalizado na página Ambientes {#adding-cdn-environments}

<!-- I DON'T SEE THIS ABILITY ANYMORE IN THE UI -->

As etapas para adicionar um nome de domínio personalizado da página **Ambientes** são as mesmas de [adicionar um nome de domínio personalizado da página Configurações de Domínio](#adding-cdn-settings), mas o ponto de entrada é diferente. Siga estas etapas para adicionar um nome de domínio personalizado na página **Ambientes**.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a página de detalhes **Detalhes do ambiente** do ambiente em que está interessado.

   ![Inserção do nome de domínio na página Detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Use a tabela **Nomes de domínio** para enviar o nome de domínio personalizado.

   1. Insira o nome de domínio personalizado.
   1. Selecione o certificado SSL associado a esse nome na lista suspensa.
   1. Clique em **+Adicionar**.

   ![Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. A caixa de diálogo **Adicionar nome de domínio** é aberta na guia **Nome de Domínio**. Continue como faria para [adicionar um nome de domínio personalizado da página Configurações de Domínio](#adding-cdn-settings). —>
