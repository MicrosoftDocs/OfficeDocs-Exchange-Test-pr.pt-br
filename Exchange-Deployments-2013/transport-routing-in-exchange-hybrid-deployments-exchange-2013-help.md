---
title: 'Roteamento de transporte em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Roteamento de transporte em implantações híbridas do Exchange
ms:assetid: 36c2cea3-2e2f-40ac-88bd-7e1b6bd27828
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659050(v=EXCHG.150)
ms:contentKeyID: 50487115
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Roteamento de transporte em implantações híbridas do Exchange

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-07-29_

Este tópico discute suas opções de roteamento para mensagens de entrada da Internet e mensagens de saída para a Internet.


> [!IMPORTANT]
> Não coloque servidores, serviços ou dispositivos que processem ou modifiquem o tráfego SMTP entre os servidores Exchange no local e o Office 365. A proteção do fluxo de emails entre a organização do Exchange no local e o Office 365 depende das informações contidas nas mensagens enviadas entre a organização. Firewalls que permitem o tráfego SMTP através da porta TCP 25 sem modificação são compatíveis. Se um servidor, um serviço ou um dispositivo processar uma mensagem entre a organização do Exchange no local e o Office 365, essa informação será removida. Se isso acontecer, a mensagem não será mais considerada interna da sua organização e estará sujeita a regras de diário, transporte e filtro antispam, bem como a outras políticas que podem não se aplicar a ela.




> [!TIP]
> Os exemplos neste tópico não incluem a adição de servidores de Transporte de Borda à implantação híbrida. As rotas que as mensagens seguem entre a organização local, a organização do Exchange Online e a Internet não se alteram com a adição de um servidor de Transporte de Borda. O roteamento apenas é alterado dentro da organização local. Para obter mais informações sobre a adição de servidores de Transporte de Borda a uma implantação híbrida, consulte <A href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Servidores de transporte de borda com implantações híbridas</A>.



## Mensagens de entrada da Internet

Faz parte do planejamento e da configuração de sua implantação híbrida decidir se você deseja que todas as mensagens de remetentes da Internet sejam encaminhadas pelo Exchange Online ou através de sua organização local. Todas as mensagens de remetentes da Internet serão inicialmente entregues à organização que você selecionar e, em seguida, serão encaminhadas para o local onde a caixa de correio do destinatário está localizada. A opção de encaminhar as mensagens pelo Exchange Online ou através de sua organização local depende de vários fatores, tais como a aplicação de diretivas de conformidade a todas as mensagens enviadas para ambas as organizações, a quantidade de caixas de correio existentes em cada organização e assim por diante.

O caminho adotado pelas mensagens enviadas a destinatários em suas organizações locais e do Exchange Online depende da forma como você decidir configurar seu registro MX na implantação híbrida. O método preferido é configurar seu registro MX de modo que este aponte para o Exchange Online Protection (EOP) no Office 365 já que essa configuração fornece o filtro de spam mais preciso. O assistente de Configuração Híbrida não configura o roteamento para mensagens de entrada da Internet para as organizações locais e do Exchange Online. Você deve configurar manualmente seu registro MX se deseja alterar a forma como suas mensagens de entrada da Internet são entregues.

  - **Se você alterar seu registro MX para apontar para o serviço da Exchange Online Protection no Office 365**   Essa é a configuração recomendada para implantações híbridas. Todas as mensagens enviadas para qualquer destinatário nas organizações serão roteadas pela organização do Exchange Online primeiro. A mensagem endereçada a um destinatário localizado em sua organização local será encaminhada primeiro através de sua organização do Exchange Online e então entregue ao destinatário em sua organização local. Essa rota também é recomendável se você tiver mais destinatários em sua organização do Exchange Online do que em sua organização local. Exige-se essa configuração no Exchange Online Protection de maneira que ela forneça a verificação e o bloqueio do spam.

  - **Se você mantiver seu registro MX apontado para sua organização local** Todas as mensagens enviadas para qualquer destinatário nas organizações serão roteadas pela organização local primeiro. A mensagem endereçada a um destinatário localizado no Exchange Online será encaminhada primeiramente através de sua organização local e então entregue ao destinatário no Exchange Online. Essa rota pode ser útil nas organizações onde você dispõe de diretivas de conformidade exigindo que as mensagens enviadas e recebidas de uma organização sejam examinadas por uma solução de registro em diário. Se você escolher essa opção, a Exchange Online Protection não conseguirá realizar uma verificação efetiva das mensagens de spam.

Para saber mais, consulte [Práticas recomendadas de fluxo de emails para Exchange Online e Office 365 (visão geral)](https://technet.microsoft.com/pt-br/library/jj937232\(v=exchg.150\)).

Leia a seção abaixo que corresponde a como você planeja encaminhar mensagens enviadas de destinatários da Internet para seus destinatários locais e do Exchange Online. Em cada seção, o "servidor local do Exchange" pode ser um servidor de Acesso para Cliente do Exchange 2013 ou um servidor caixa de correio do Exchange 2016.

## Encaminhar mensagens recebidas da Internet através da organização do Exchange Online

As etapas e os diagramas a seguir ilustram o caminho das mensagens recebidas que será tomado em sua implantação híbrida se você decidir apontar seu registro MX para o serviço de EOP na organização do Office 365. O caminho da mensagem difere dependendo de se você selecionou habilitar ou não o transporte de email centralizado.


> [!IMPORTANT]
> Pode ser necessário adquirir licenças do EOP para cada caixa de correio local que recebe mensagens entregues primeiro ao EOP e depois encaminhadas através da organização do Exchange Online. Entre em contato com o seu revendedor Microsoft para obter mais informações.



Quando o transporte de email centralizado está **desabilitado** (configuração padrão), as mensagens recebidas da Internet são roteadas da seguinte maneira em uma implantação híbrida:

1.  Uma mensagem de entrada é enviada de um remetente da Internet para os destinatários sara@contoso.com e davi@contoso.com. A caixa de correio de Sara está localizada em um servidor de Caixa de Correio do Exchange na organização local. A caixa de correio de Davi está localizada no Exchange Online.

2.  Como ambos os destinatários têm endereços de email contoso.com e o registro MX de contoso.com aponta para o EOP, a mensagem é entregue ao EOP.

3.  O EOP roteia as mensagens de ambos os destinatários para o Exchange Online.

4.  O Exchange Online examina a mensagem à procura de vírus e realiza uma pesquisa para cada destinatário. Através dessa pesquisa, ele determina que a caixa de correio de Sara está localizada na organização local e a de Davi na organização do Exchange Online.

5.  Exchange Online divide a mensagem em duas cópias. Uma cópia é entregue na caixa de correio de David.

6.  A segunda cópia é enviada do Exchange Online de volta para o EOP.

7.  O EOP envia a mensagem para um servidor local do Exchange na organização local.

8.  O Exchange envia a mensagem para o servidor de Caixa de Correio do Exchange, onde ela é entregue à caixa de correio de Sara.

**Encaminhar mensagens através da organização do Exchange Online para ambas as organizações, a local e a do Exchange Online, com o transporte de email centralizado desabilitado (configuração padrão)**

![Entrada centralizada para EXO](images/JJ659050.f98341e0-088d-49f0-bf8e-09f35255bf9e(EXCHG.150).png "Entrada centralizada para EXO")

Quando o transporte de email centralizado está **habilitado**, as mensagens recebidas da Internet são roteadas da seguinte maneira em uma implantação híbrida:

1.  Uma mensagem de entrada é enviada de um remetente da Internet para os destinatários sara@contoso.com e davi@contoso.com. A caixa de correio de Sara está localizada em um servidor de Caixa de Correio do Exchange na organização local. A caixa de correio de Davi está localizada no Exchange Online.

2.  Como ambos os destinatários têm endereços de email contoso.com e o registro MX de contoso.com aponta para o EOP, a mensagem é entregue ao EOP e verificada quanto a vírus.

3.  Como o transporte de email centralizado está habilitado, o EOP encaminha as mensagens para ambos os destinatários para o servidor local do Exchange.

4.  O servidor local do Exchange executa uma pesquisa para cada destinatário. Através dessa pesquisa, ele determina que a caixa de correio de Sara está localizada na organização local e a de Davi na organização do Exchange Online.

5.  O servidor local do Exchange divide a mensagem em duas cópias. Uma cópia da mensagem é entregue na caixa de correio de Sara no servidor de Caixa de Correio local do Exchange.

6.  A segunda cópia é enviada do servidor local do Exchange de volta para o EOP.

7.  O EOP envia a mensagem para Exchange Online.

8.  O Exchange entrega a mensagem para a caixa de correio de Davi.

**Encaminhar mensagens através da organização do Exchange Online para ambas as organizações, a local e a do Exchange Online, com o transporte de email centralizado habilitado**

![EXO de entrada, centralizado habilitado](images/JJ659050.062422d5-9cb6-42c2-9ec0-31962cd7ada6(EXCHG.150).png "EXO de entrada, centralizado habilitado")

## Encaminhar mensagens recebidas da Internet através de sua organização no local

As etapas e o diagrama a seguir ilustram o caminho das mensagens recebidas da Internet que será tomado em sua implantação híbrida se você decidir manter seu registro MX apontado para sua organização local.

1.  Uma mensagem de entrada é enviada de um remetente da Internet para os destinatários sara@contoso.com e davi@contoso.com. A caixa de correio de Sara está localizada em um servidor de Caixa de Correio do Exchange na organização local. A caixa de correio de Davi está localizada no Exchange Online.

2.  Como ambos os destinatários têm endereços de email contoso.com e o registro MX de contoso.com aponta para a organização local, a mensagem é entregue a um servidor local do Exchange.

3.  O servidor local do Exchange executará uma pesquisa para cada destinatário usando um servidor local do catálogo global. Por meio da pesquisa de catálogo global, ele determina que a caixa de correio de Sara está localizada no servidor de Caixa de Correio do Exchange, enquanto a caixa de correio de Davi está localizada na organização do Exchange Online e tem um endereço de roteamento híbrido davi@contoso.mail.onmicrosoft.com.

4.  O servidor local do Exchange divide a mensagem em duas cópias. Uma cópia da mensagem é enviada ao servidor de Caixa de Correio local do Exchange, onde é entregue à caixa de correio de Sara.

5.  A segunda cópia da mensagem é enviada pelo servidor local do Exchange para o EOP, que recebe mensagens enviadas para a organização do Exchange Online, usando um conector de Envio configurado para usar TLS.

6.  O EOP envia a mensagem para a organização do Exchange Online, onde ela é verificada quanto a vírus e entregue à caixa de correio de David.

**Encaminhar mensagens através da organização local para ambas as organizações, a local e a do Exchange Online**

![Mensagem de entrada centralizada, local](images/JJ659050.a246a1e2-7593-4d13-9426-73622a545c9a(EXCHG.150).png "Mensagem de entrada centralizada, local")

## Mensagens de saída para a Internet

Além de escolher como as mensagens de entrada endereçadas a destinatários em suas organizações são encaminhadas, você também pode escolher como as mensagens de saída enviadas por destinatários do Exchange Online são encaminhadas. Quando você executa o assistente de Configuração Híbrida, é possível selecionar uma de duas opções:

  - **Não habilitar o transporte de email centralizado**   Selecionada por padrão no assistente de Configuração Híbrida, essa opção encaminha mensagens de saída enviadas pela organização do Exchange Online diretamente para a Internet. Use esta opção se não precisar aplicar nenhuma diretiva de conformidade local ou outras regras de processamento a mensagens enviadas por destinatários na organização do Exchange Online.

  - **Habilitar transporte de email centralizado**   Selecionar essa opção encaminha mensagens de saída enviadas da organização do Exchange Online através de sua organização local. Exceto pelas mensagens enviadas para outros destinatários na mesma organização do Exchange Online, todas as mensagens enviadas de destinatários na organização do Exchange Online são enviadas através da organização local. Isso permite aplicar regras de conformidade a essas mensagens e quaisquer outros processo ou requisitos que tenham que ser aplicados a todos os seus destinatários, estejam eles localizados na organização do Exchange Online ou na organização local.
    

    > [!TIP]
    > O transporte de email centralizado somente é recomendado para organizações com necessidades de transporte relacionadas a conformidade específicas. Nossa recomendação para organizações do Exchange típicas é não habilitar o transporte de email centralizado.



Mensagens enviadas de destinatários locais sempre são enviadas diretamente para os destinatários na Internet usando DNS, independentemente de qual das opções acima foi selecionada no assistente de Configuração Híbrida.

As etapas e o diagrama a seguir ilustram o caminho das mensagens de saída enviadas de destinatários locais.

1.  Sara, que possui uma caixa de correio no servidor de Caixa de Correio local do Exchange, envia uma mensagem para um destinatário externo na Internet, mila@cpandl.com.

2.  O servidor do Exchange pesquisa o registro MX em busca de cpandl.com e envia a mensagem para os servidores de email de cpandl.com localizados na Internet.

**Mensagens de remetentes no local para destinatários da Internet**

![Email de saída do local](images/JJ659050.71f287d6-b814-4820-a0dc-575f17d13894(EXCHG.150).png "Email de saída do local")

Leia a seção abaixo que corresponde a como você planeja encaminhar mensagens enviadas de destinatários na organização do Exchange Online para destinatários na Internet.

## Entregar mensagens de Internet do Exchange Online usando o DNS (transporte de email centralizado desabilitado)

As etapas e o diagrama a seguir ilustram o caminho de mensagem de saída para mensagens enviadas de destinatários do Exchange Online para um destinatário da Internet que é tomado quando **Habilitar o transporte de email centralizado** não está selecionado no assistente de Configuração Híbrida, que é a configuração padrão.

1.  David, que possui uma caixa de correio na organização do servidor Exchange Online, envia uma mensagem para um destinatário externo na Internet, erin@cpandl.com.

2.  Exchange Online examina a mensagem à procura de vírus e a envia para a empresa do EOP do Exchange Online.

3.  O EOP pesquisa o registro MX em busca de cpandl.com e envia a mensagem para os servidores de email de cpandl.com localizados na Internet.

**Mensagem de remetentes do Exchange Online roteada diretamente para a Internet com o transporte de email centralizado desabilitado (configuração padrão)**

![Mensagem de saída diretamente do EXO](images/JJ659050.fe1c4241-0d6e-47bf-b61d-5af732d2dbbc(EXCHG.150).png "Mensagem de saída diretamente do EXO")

## Encaminhar mensagens da Internet a partir do Exchange Online por meio de sua organização local (transporte de email centralizado habilitado)

As etapas e o diagrama a seguir ilustram o caminho de mensagem de saída para mensagens enviadas de destinatários do Exchange Online para um destinatário da Internet que é tomado quando você seleciona **Habilitar o transporte de email centralizado** no assistente de Configuração Híbrida.

1.  David, que possui uma caixa de correio na organização do servidor Exchange Online, envia uma mensagem para um destinatário externo na Internet, erin@cpandl.com.

2.  Exchange Online examina a mensagem à procura de vírus e a envia para o EOP.

3.  O EOP é configurado para enviar todas as mensagens de Internet para um servidor local, então, a mensagem é roteada para um servidor local do Exchange. A mensagem é enviada usando o protocolo TLS.

4.  Um servidor local do Exchange realiza os processos de conformidade, antivírus e demais processos configurados pelo administrador na mensagem de Davi.

5.  O servidor local do Exchange pesquisa o registro MX em busca de cpandl.com e envia a mensagem para os servidores de email de cpandl.com localizados na Internet.

**Mensagem de remetentes do Exchange Online encaminhadas através da organização local com o transporte de email centralizado habilitado**

![Mensagem EXO de saída por meio do local](images/JJ659050.7ea9ffee-944b-45ae-ba4d-c3484100399b(EXCHG.150).png "Mensagem EXO de saída por meio do local")

