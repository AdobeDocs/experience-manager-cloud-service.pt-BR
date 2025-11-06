---
title: Adicionar um nome de domínio personalizado
description: Saiba como adicionar um nome de domínio personalizado usando Configurações de domínio no Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 12%

---


# Adicionar um nome de domínio personalizado {#adding-custom-domain-name}

Saiba como adicionar um nome de domínio personalizado usando **Configurações de domínio** no Cloud Manager.

## Requisitos {#requirements}

Atenda a esses requisitos antes de adicionar um nome de domínio personalizado no Cloud Manager.

* Você deve ter adicionado um certificado SSL para o domínio que deseja adicionar *antes* de adicionar um nome de domínio personalizado, conforme descrito no documento [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Você deve ter a função de **Proprietário da empresa** ou **Gerente de implantação** para adicionar um nome de domínio personalizado no Cloud Manager.
* Use o Fastly ou outro CDN (Content Delivery Network).

>[!IMPORTANT]
>
>Se você usar uma CDN gerenciada pela Adobe, ainda precisará adicionar seu domínio ao Cloud Manager.

## Onde adicionar nomes de domínio personalizados {#where-to-add-custom-domain-name}

Você pode adicionar um nome de domínio personalizado na [página Configurações de domínio](#adding-cdn-settings) do Cloud Manager.

Ao adicionar um nome de domínio personalizado, o domínio é distribuído usando o certificado mais específico e válido. Se vários certificados tiverem o mesmo domínio, o mais recente atualizado será escolhido. A Adobe recomenda que você gerencie certificados de modo que não haja domínios sobrepostos.

As etapas para qualquer método descrito neste documento são baseadas no Fastly. Se você usou uma CDN (Content Delivery Network) diferente, configure seu domínio com a CDN que você escolheu usar.

## Adicionar um nome de domínio personalizado {#adding-custom-domain-name-settings}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. No menu lateral, em **Serviços**, clique em ![Ícone de Configurações](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) **Configurações de Domínio**.

   ![A janela Configurações do domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Próximo ao canto superior direito da página **Configurações de Domínio**, clique em **Adicionar Domínio**.

1. Na caixa de diálogo **Adicionar domínio**, no campo **Nome do Domínio**, digite o nome de domínio personalizado que você está usando.
Ao inserir o nome de domínio, não inclua `http://`, `https://` ou espaços.

   >[!NOTE]
   >
   >Se você precisar das versões `www` e `non-www` de um domínio, é necessário adicioná-las separadamente. Por exemplo, `example.com` e `www.example.com`.
   <!-- Marius Petria on SLACK tmp-skyline-cdn-certificates - Actually  my opinion is that this option should be explicit in UI (that was present in the initial mocks of the design but for some reason it was dropped). I think when adding a domain there should be a check mark to also add www.domain. When adding example.com Customer should be prompted with the following options: Do you also want to add www.example.com and have a redirect example.com -> www.example.com?Do you also want to add www.example.com and have a redirect www.example.com -> example.com? -->

1. Clique em **Criar**.

1. Na caixa de diálogo **Verificar domínio**, em **Que tipo de certificado você pretende usar com este domínio?**, selecione uma das seguintes opções:

   | Opção Tipo de certificado | Descrição |
   | --- | --- |
   | Certificado SSL gerenciado pela Adobe (DV) | Selecione esse tipo de certificado se quiser usar um certificado DV (Domain Validation). Essa opção é ideal para a maioria dos casos, fornecendo validação básica de domínio. O Adobe gerencia e renova o certificado automaticamente. |
   | Certificado SSL gerenciado pelo cliente (OV/EV) | Selecione esse tipo de certificado se pretender usar um certificado SSL EV/OV para proteger o domínio. Essa opção oferece segurança aprimorada com OV (Validação da Organização) ou EV (Validação Estendida). Use se uma verificação mais rigorosa, níveis de confiança mais altos ou controle personalizado dos certificados for necessário. |

1. Na caixa de diálogo **Verificar domínio**, com base no tipo de certificado selecionado, siga um destes procedimentos:

   | Se você selecionou o tipo de certificado | Descrição |
   | --- | ---  |
   | Certificado gerenciado pela Adobe | a. Conclua as [etapas de certificado gerenciado pela Adobe](#adobe-managed-cert-steps) abaixo. Ao concluir as etapas, na caixa de diálogo **Verificar domínio**, clique em **Verificar**.<ul><li>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.</li><li>A Cloud Manager verifica a propriedade do nome de domínio e atualiza o status na tabela **Configurações de Domínio**. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.</li>![Verificar status do domínio](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. Agora você está pronto para [adicionar um certificado SSL gerenciado pela Adobe](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Certificado gerenciado pelo cliente | a. Clique em **OK**.<br>b. Agora você está pronto para [adicionar um certificado SSL gerenciado pelo cliente (OV/EV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert).<br>Depois de adicionar o certificado, seu nome de domínio é marcado como verificado na tabela **Configurações de Domínio**. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.</li></ul><br>![Verificar domínio para um certificado EV/OV gerenciado pelo cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |

   >[!NOTE]
   >
   >Se você usa seu próprio certificado SSL gerenciado pelo cliente (OV/EV ou DV), não é necessário adicionar um certificado SSL. Essa regra também se aplica se você planeja usar um ***provedor*** de CDN (Rede de Entrega de Conteúdo) gerenciado pelo cliente. Em vez disso, vá diretamente para [Adicionar um Mapeamento de Domínio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) quando estiver pronto.


### Etapas do certificado gerenciado pela Adobe {#adobe-managed-cert-steps}

Se você selecionou o tipo de certificado *Adobe managed certificate*, conclua a etapa a seguir na caixa de diálogo **Verificar domínio**.

![etapas de certificado gerenciado pela Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Para verificar o domínio em uso, é necessário adicionar e verificar um CNAME.

Um tipo de registro `CNAME` ou `A`, uma vez provisionado, roteia todo o tráfego de Internet do domínio para onde quer que esteja apontando. Se esse local não for provisionado para veicular o tráfego, haverá uma interrupção. Se não for testado, poderá haver erros no conteúdo. É por isso que essa etapa é sempre realizada após a conclusão dos testes, quando você está pronto para entrar em produção.

Para definir essas configurações, determine se um registro `CNAME` ou apex deve ser configurado para apontar seu nome de domínio personalizado para o nome de domínio do Cloud Manager. As seções a seguir deste documento podem ajudar você a determinar qual tipo de registro é apropriado para sua configuração de DNS.

>[!NOTE]
>
>Para CDNs gerenciadas pela Adobe, ao usar certificados DV (Domain Validation, validação de domínio), somente sites com validação ACME são permitidos.


## Configurar DNS{#config-dns}

>[!WARNING]
>
>O princípio &quot;registrar antes de anunciar&quot; se aplica aqui. Ou seja, a configuração do DNS só deve ser executada *depois* de você ter adicionado o mapeamento de domínio com êxito. Isso garante que a Cloud Manager reconheça e valide se o domínio existe em sua própria configuração antes de responder às solicitações dele. Também evita qualquer tentativa de aquisição de domínio.

Certifique-se de atender aos seguintes requisitos *antes* de configurar seus registros DNS:

* Identifique o host ou o registrador do seu domínio, se você ainda não o conhece.
* Ser capaz de editar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa apropriada que pode fazer isso.
* Você já verificou o nome de domínio personalizado configurado, conforme descrito no documento [Verificando o Status do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

### Registro CNAME {#adobe-managed-cert-cname-record}

Um nome canônico ou registro CNAME é um tipo de registro DNS que mapeia um nome de alias a um nome de domínio verdadeiro ou canônico. Os registros CNAME normalmente são usados para mapear um subdomínio como `www.example.com` ao domínio que hospeda o conteúdo desse subdomínio.

Faça logon no provedor de serviços DNS e crie um registro `CNAME` para apontar seu nome de domínio personalizado ao destino, como na tabela a seguir.

| CNAME | Domínio personalizado - apontar para o destino |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

### Registro APEX {#adobe-managed-cert-apex-record}

Um domínio apex é um domínio personalizado que não contém um subdomínio, como `example.com`. Um domínio apex é configurado com um registro `A`, `ALIAS` ou `ANAME` por meio do provedor de DNS. Domínios apex devem apontar para endereços IP específicos.

Adicione os seguintes registros `A` às configurações de DNS do domínio por meio do provedor de domínio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

>[!TIP]
>
>O *registro CNAME* ou o *registro A* pode ser definido no servidor DNS regulador para economizar seu tempo.

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->



<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


