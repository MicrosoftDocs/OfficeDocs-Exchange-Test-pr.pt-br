---
title: 'Opções de transporte em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Opções de transporte em implantações híbridas do Exchange
ms:assetid: da605a78-5429-4de8-8b04-bc4c45a41ba1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659055(v=EXCHG.150)
ms:contentKeyID: 50487121
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opções de transporte em implantações híbridas do Exchange

 

_<strong>Aplica-se a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

Nas implantações híbridas, você pode ter caixas de correio que residem em sua organização local e em uma organização do Exchange e também em uma organização do Exchange Online. Um componente crítico da criação dessas duas organizações separadas é elas serem visualizadas pelos usuários como uma organização combinada, e as mensagens trocadas entre eles utilizar transporte híbrido. O transporte híbrido faz com que a mensagens que trafegam entre destinatários de quaisquer das organizações sejam autenticadas, criptografadas e transferidas usando Transport Layer Security (TLS). Essas mensagens aparecem como "internas" para componentes do Exchange, tais como regras de transporte, registro em diário e políticas antispam. O transporte híbrido é configurado automaticamente pelo assistente de Configuração Híbrida.

Para a configuração de transporte híbrido funcionar com o assistente de Configuração Híbrida, o ponto de extremidade SMTP local que aceita conexões do Exchange Online deve ser um servidor de Caixa de Correio (Exchange 2016 e mais recente), um servidor de Acesso para Cliente (Exchange 2013), um servidor de Transporte de Hub (Exchange 2010 e mais antigo) ou um servidor de Transporte de Borda (Exchange 2010 e mais recente).


> [!IMPORTANT]
> Não coloque servidores, serviços ou dispositivos que processem ou modifiquem o tráfego SMTP entre os servidores Exchange no local e o Office 365. A proteção do fluxo de emails entre a organização do Exchange no local e o Office 365 depende das informações contidas nas mensagens enviadas entre a organização. Firewalls que permitem o tráfego SMTP através da porta TCP 25 sem modificação são compatíveis. Se um servidor, um serviço ou um dispositivo processar uma mensagem entre a organização do Exchange no local e o Office 365, essa informação será removida. Se isso acontecer, a mensagem não será mais considerada interna da sua organização e estará sujeita a regras de diário, transporte e filtro antispam, bem como a outras políticas que podem não se aplicar a ela.



As mensagens de entrada enviadas para destinatários em ambas as organizações a partir de destinatários externos na Internet seguem uma rota de entrada comum. As mensagens de saída enviadas das organizações para destinatários externos na Internet podem seguir uma rota de saída comum ou podem ser enviadas através de rotas independentes.

Você deve escolher como encaminhar mensagens de entrada e de saída quando planejar e configurar a implantação híbrida. A rota adotada pelas mensagens de entrada e de saída enviadas e recebidas por destinatários na organização local e na organização do Exchange Online depende do seguinte:

  - Deseja rotear correio de entrada para as suas caixas de correio locais e do Exchange por meio do Exchange Online ou da sua organização local?
    
    A rota seguida pelas mensagens de entrada em ambas as organizações depende de vários fatores, como onde a maioria das suas caixas de correio está localizada, se você deseja proteger sua organização local usando a verificação anti-malware e anti-spam do Office 365, onde sua infraestrutura de conformidade está configurada, e assim por diante.

  - Deseja rotear os emails de saída para destinatários externos de sua organização do Exchange Online pela sua organização local (transporte de email centralizado) ou deseja roteá-los diretamente para a Internet?
    
    Com o transporte de email centralizado, você pode encaminhar todas as mensagens de caixas de correio no Exchange Online através da organização local antes que elas sejam transmitidas para a Internet. Essa abordagem é útil em cenários de conformidade onde todas as mensagens de entrada e de saída da Internet devem ser processadas por servidores locais. Alternativamente, você pode configurar o Exchange Online para encaminhar mensagens a destinatários externos diretamente na Internet.
    

    > [!TIP]
    > O transporte de email centralizado somente é recomendado para organizações com necessidades de transporte relacionadas a conformidade específicas. Nossa recomendação para as organizações típicas do Exchange é de não permitir o transporte de emails centralizado, uma vez que isso pode aumentar significativamente a quantidade de mensagens processadas pelos seus próprios servidores locais, aumentar a largura de banda usada e criar uma dependência desnecessária dos seus servidores locais.



  - Você deseja implantar um servidor de Transporte de Borda em sua organização local?
    
    Se não deseja expor seus servidores internos do Exchange unidos por domínio diretamente à Internet, você pode implantar os servidores de Transporte de Borda em sua rede de perímetro. Para saber mais sobre a adição de um servidor de Transporte de Borda à sua implantação híbrida, confira [Servidores de transporte de borda com implantações híbridas](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

Independentemente de como você encaminha mensagens enviadas e recebidas da Internet, todas as mensagens enviadas entre a organização local e a organização do Exchange Online utilizam transporte seguro. Para obter mais informações, consulte Comunicação confiável, posteriormente neste tópico.

Para saber mais sobre como essas opções afetam o roteamento de mensagens em sua organização, consulte [Roteamento de transporte em implantações híbridas do Exchange](transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md).

## Proteção do Exchange Online em implantações híbridas

O EOP é um serviço online prestado pela Microsoft e utilizado por muitas empresas para proteger suas organizações locais contra vírus, spam, golpes de phishing e violações de políticas. No Office 365, o EOP é usado para proteger organizações do Exchange Online contra as mesmas ameaças. Quando você se inscreve no Office 365, a empresa do EOP é criada automaticamente que é associada à sua organização do Exchange Online.

A empresa do EOP contém várias configurações de transporte de mensagens que você pode ajustar para sua organização do Exchange Online. Você pode especificar quais domínios SMTP devem ser oriundos de endereços IP específicos, exigir certificados TLS e SSL (Secure Sockets Layer), ignorar filtros antispam, diretivas de conformidade e muito mais. O EOP é a porta de entrada para a sua organização do Exchange Online. Todas as mensagens, independentemente da origem, devem passar pelo EOP antes que cheguem às caixas de correio de sua organização do Exchange Online. Adicionalmente, todas as mensagens enviadas pela sua organização do Exchange Online devem passar pelo EOP antes de chegarem à Internet.

Quando você configura uma implantação híbrida com o assistente de Configuração Híbrida, todas as configurações de transporte são automaticamente ajustadas em sua organização local e na empresa do EOP incluída em sua organização do Exchange Online. O assistente de Configuração Híbrida define todos os conectores de entrada e de saída e outras configurações dessa empresa do EOP para proteger as mensagens enviadas entre a organização local e a organização do Exchange Online, encaminhando as mensagens para o destino certo. Se deseja definir configurações de transporte personalizadas para sua organização do Exchange Online, você também as ajustará nessa empresa do EOP.

## Comunicação confiável

Para ajudar a proteger os destinatários na organização local e na organização do Exchange Online e assegurar que as mensagens enviadas entre as organizações não sejam interceptadas e lidas, o transporte entre a organização local e o EOP é configurado de modo a usar TLS forçado. O transporte de email seguro usa certificados TLS/SSL fornecidos por uma Autoridade de Certificação (CA) terceirizada. Mensagens entre EOP e a organização do Exchange Online também usam TLS.

Ao usar o transporte TLS forçado, os servidores de envio e recebimento examinam o certificado configurado no outro servidor. O nome do assunto ou um dos nomes de assunto alternativos (SAN) configurado nos certificados deve corresponder ao FQDN que o administrador especificou explicitamente no outro servidor. Por exemplo, se o EOP for configurado para aceitar e proteger mensagens enviadas do FQDN mail.contoso.com, o servidor de Acesso para Cliente ou de Transporte de Borda local de envio deve ter um certificado SSL com mail.contoso.com no nome de entidade ou no SAN. Se essa exigência não for atendida, a conexão será recusada pelo EOP.


> [!TIP]
> O FQDN usado não precisa corresponder ao nome de domínio de email dos destinatários. O único requisito é que o FQDN no nome de assunto do certificado ou SAN corresponda ao FQDN que os servidores de recebimento ou envio estão configurados para aceitar.



Além de usar TLS, as mensagens entre as organizações são tratadas como "internas". Esta abordagem permite que as mensagens ignorem configurações antispam e outros serviços.

Saiba mais sobre certificados SSL e segurança de domínio em [Requisitos de certificado para implantações híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) e [Noções básicas de Certificados TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

