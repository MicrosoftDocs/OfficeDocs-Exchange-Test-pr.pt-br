---
title: 'Domínios aceitos: Exchange 2013 Help'
TOCTitle: Domínios aceitos
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 50486554
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domínios aceitos

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-06-16_

Um domínio aceito é qualquer intervalo de nomes (namespace) SMTP para o qual o Microsoft Exchange Server 2013 envia ou recebe emails. Os domínios aceitos incluem os domínios para os quais a organização do Exchange é autoritativa. Uma organização do Exchange é autoritativa quando trata a entrega de mensagens para destinatários no domínio aceito. Domínios aceitos também incluem domínios para os quais a organização do Exchange recebe emails e, em seguida, retransmite-os para um servidor de email que está fora da organização para entregá-los ao destinatário.

**Sumário**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## Configurando Domínios Aceitos

Domínios aceitos são definidos como configurações globais para a organização do Exchange. Você deve configurar todos os domínios para os quais sua organização do Exchange retransmite ou entrega mensagens como um domínio aceito na sua organização.

Há três tipos de domínios aceitos: autoritativos, de retransmissão internos e de retransmissão externos. Esses tipos de domínios aceitos serão discutidos nas seções a seguir.


> [!TIP]
> Se você tiver um servidor de Transporte de Borda inscrito em sua rede de perímetro, configure os domínios aceitos em um servidor de Caixa de Correio em sua organização do Exchange. A configuração de domínios aceitos é replicada para o servidor de Transporte de Borda durante a sincronização do EdgeSync. Para saber mais, confira <A href="edge-subscriptions-exchange-2013-help.md">Inscrições de Borda</A>.



## Domínios autoritativos

Uma organização pode ter mais de um domínio SMTP. O conjunto de domínios de email de uma organização forma os domínios autoritativos. No Exchange 2013, um domínio aceito é considerado autoritativo quando a organização do Exchange hospeda caixas de correio para destinatários neste domínio SMTP.

Por padrão, quando o primeiro servidor de caixa de correio do Exchange 2013 é instalado, um domínio aceito é configurado como autoritativo para a organização do Exchange. O domínio padrão aceito é um FQDN (nome de domínio totalmente qualificado) para seu domínio raiz de floresta. Geralmente, o nome do domínio interno é diferente do nome do domínio externo. Por exemplo, o nome de seu domínio interno pode ser contoso.local, embora o nome do domínio externo seja contoso.com. O DNS de troca de email (MX) da sua organização registra as referências a contoso.com, que é o intervalo de nome (namespace) SMTP atribuído aos usuários, quando uma política de endereço de email é criada. Você deve criar um domínio aceito correspondente ao nome do domínio externo.

Para saber mais, consulte:

  - [Configurar um domínio aceito na organização do Exchange como autoritativo](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [Configurar o Exchange para aceitar emails de vários domínios autoritativos](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## Domínios de retransmissão

Geralmente, a maioria dos servidores de mensagens da Internet estão configurados para não aceitar que outros domínios sejam retransmitidos por meio deles. No entanto, pode haver situações nas quais você quer permitir que sócios ou subsidiários retransmitam emails através de seus servidores Exchange. No Exchange 2013, é possível configurar domínios aceitos como domínios de retransmissão. Sua organização recebe os emails e, em seguida, retransmite-os para outro servidor de email.

É possível configurar um domínio de retransmissão como interno ou externo. Esses dois tipos de domínios de retransmissão serão descritos nas seções a seguir.

## Domínio de Retransmissão Interno

Ao configurar um domínio de retransmissão interno, alguns ou todos os destinatários deste domínio não têm caixas de correio nesta organização do Exchange. Emails da Internet são retransmitidos a este domínio através de servidores de transporte nesta organização do Exchange. Esta configuração é usada nos cenários descritos nesta seção.

Pode ser necessário que uma organização compartilhe o mesmo intervalo de endereço SMTP entre dois ou mais sistemas de email. Por exemplo, pode ser necessário compartilhar o espaço de endereço SMTP entre o Exchange e um sistema de email de terceiros ou entre os ambientes do Exchange configurados em diferentes florestas Active Directory. Nestes cenários, os usuários em cada sistema de email possuem o mesmo sufixo de domínio como parte de seus endereços de email.

Para oferecer suporte nestes casos, você deve criar um domínio aceito configurado como domínio de retransmissão interno. Você também deve adicionar um conector de Envio originado no servidor de caixa de correio e configurado para enviar emails para o intervalo de endereço compartilhado. Se um domínio aceito for configurado como autoritativo e um destinatário não for encontrado no serviço de diretório do Active Directory, uma notificação de falha na entrega (NDR) é retornada para o remetente. O domínio aceito configurado como domínio de retransmissão interno primeiro tenta fazer a entrega a um destinatário na organização do Exchange. Se o destinatário não for encontrado, a mensagem será encaminhada para o conector de Envio que tem o espaço de endereço mais próximo.

Se uma organização contiver mais de uma floresta e tiver configurado a sincronização da lista de endereços global (GAL), o domínio SMTP de uma floresta pode ser configurado como um domínio de retransmissão interno em uma segunda floresta. As mensagens da Internet que são endereçadas aos destinatários nos domínios de transmissão internos são retransmitidos aos servidores de email na mesma organização. Os servidores de caixa de correio de recebimento encaminham as mensagens para os servidores de caixa de correio na floresta do destinatário. Configure o domínio SMTP como um domínio de retransmissão interno para garantir que o email endereçado a esse domínio seja aceito pela organização do Exchange. A configuração de conectores de sua organização define o modo de roteamento das mensagens.

Para saber mais, consulte [Configurar um domínio aceito para uma unidade de negócios com caixas de correio fora da sua organização do Exchange](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md).

## Domínio de Retransmissão Externo

Ao configurar um domínio de retransmissão externo, as mensagens serão retransmitidas para um servidor de email que está fora da sua organização do Exchange e do perímetro de rede da organização.

Para saber mais, consulte [Configurar um domínio aceito para uma unidade de negócios independente](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md).

## Domínios aceitos e políticas de endereço de email

Você precisará configurar um domínio aceito para que esse espaço de endereçamento SMTP possa ser usado em uma política de endereço de email. Quando você cria um domínio aceito, você pode usar um caractere curinga (\*) no espaço de endereço para indicar que todos os subdomínios do espaço de endereço SMTP também são aceitos pela organização Exchange. Por exemplo, para configurar contoso.com e todos os seus subdomínios como domínios aceitos, insira **\*. contoso.com** como o SMTP espaço de endereçamento. As entradas de domínio aceito estarão automaticamente disponíveis para uso em uma política de endereço de email.

Se um domínio aceito usado em uma política de endereço de email for excluído, essa política não será mais válida e os destinatários com os endereços de email existentes nesse domínio SMTP não poderão enviar ou receber emails.

