---
title: 'Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server'
TOCTitle: 'Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server'
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52058827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Use esta lista de verificação para instalar e implantar a Unificação de Mensagens (UM) e o Microsoft Lync Server 2013. Neste tópico, \&quot;Lync Server\&quot; também se refere ao Lync Server 2010. Entretanto, Microsoft Office Communications Server 2007 R2 também pode ser implantado em conjunto com a Unificação de Mensagens.

> [!NOTE]  
>

Antes de começar a trabalhar com essa lista de verificação, certifique-se de estar familiarizado com os conceitos em:

  - [Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Coexistência com o Office Communications Server 2007 R2 e o Lync Server](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

Para obter mais informações sobre como executar as tarefas que devem ser concluídas para o Lync Server, consulte [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Lista de verificação para a implantação do Microsoft Lync Server e a Unificação de Mensagens


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Pronto?</th>
<th>Tarefas</th>
<th>Tópico</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Examine os requisitos de sistema antes de instalar o Exchange Server 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Verifique se você atende aos pré-requisitos para instalação.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Examine os pré-requisitos para a integração do Microsoft Lync Server 2013 e o Microsoft Exchange Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Pré-requisitos para integrar Microsoft Lync Server 2013 e Microsoft Exchange Server 2013</a></p>

> [!TIP]
> O Unified Communications Managed API (UCMA) 4.0 Runtime é necessária para o Exchange 2013 e Lync Server 2010 e 2013 e é instalado durante a instalação. Para baixar e revise as informações sobre UCMA 4.0, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</A>


</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Instale os servidores de Acesso para Cliente e de Caixa de Correio necessários.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verifique a instalação e examine os logs de configuração do servidor.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificar uma instalação do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Se necessário, instale os pacotes de idiomas da UM necessários.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Instalar um pacote de idiomas para UM</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Crie a quantidade de planos de discagem de URI de SIP necessários para sua organização.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Criar um plano de discagem de UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Defina a configuração de segurança do plano de discagem.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Definir a configuração de segurança de VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure o número de chamadas concorrentes em seus servidores de Caixa de Correio.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurar o número de chamadas de entrada em um servidor de caixa de correio</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure números do Outlook Voice Access e outras configurações.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Gerenciar um plano de discagem de Unificação de mensagens</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Adicione todos os servidores de Acesso para Cliente e de Caixa de Correio a cada plano de discagem URI do SIP.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure a discagem de saída para Unificação de Mensagens. Permita todas as chamadas nos planos de discagem URI do SIP e políticas de caixa de correio da UM que estejam vinculadas a esses planos de discagem.</p></td>
<td><p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizar chamadas para usuários em um plano de discagem</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autorizar chamadas para um grupo de usuários</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Crie o número necessário de atendedores automáticos.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Criar um Atendedor Automático da UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure cada um dos atendedores automáticos da UM.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Configurar um atendedor automático</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Crie, importe e habilite um novo certificado do Exchange para UM ou habilite um certificado de terceiros mutuamente confiável.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Configure o modo de inicialização da UM como Duplo ou TLS para cada servidor de Acesso para Cliente e de Caixa de Correio.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurar o modo de inicialização em um servidor de caixa de correio</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurar o modo de inicialização em um servidor de acesso para cliente</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Reinicie o serviço Unificação de mensagens do Microsoft Exchange e o serviço Roteador de Chamadas da Unificação de Mensagens em todos os Exchange Servers para carregar os certificados necessários.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Pare o serviço de Unificação de mensagens do Microsoft Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Iniciar o serviço de Unificação de mensagens do Microsoft Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Pare o serviço Microsoft Exchange Unified Messaging roteador de chamadas</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Iniciar o serviço Microsoft Exchange Unified Messaging roteador de chamadas</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Crie uma política de caixa de correio da UM ou configure a política de caixa de correio da UM padrão.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Criar uma política de caixa de correio da UM</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Gerenciar uma política de caixa de correio de Unificação de mensagens</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Habilite usuários para a Unificação de Mensagens com um endereço SIP e vincule-os a um plano de discagem URI do SIP.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Habilitar um usuário para caixa postal</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Examine a documentação de planejamento do Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">Planejamento de</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Instale e implante o Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">Implantando o Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Importe o PKI interno mutuamente confiável ou o certificado de terceiros importado para os servidores da UM do Exchange.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">Configurar certificados para servidores</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">Configurar certificados no servidor executando o Microsoft Exchange Server Unificação de mensagens</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Se necessário, inicie os serviços do Lync em servidores para carregar os certificados.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">Iniciar serviços nos servidores</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Abra o Shell de Gerenciamento do Exchange e execute o script exchucutil.ps1 localizado na pasta %Program Files%\Microsoft\Exchange Server\V15\Scripts.</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">Configurar a Unificação de mensagens para funcionar com o Lync Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Examine os requisitos do Enterprise Voice.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">Pré-requisitos de software para o Enterprise Voice</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">Segurança e pré-requisitos de configuração para o Enterprise Voice</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Implante e configure gateways de mídia ou Servidores de Mediação e defina pares.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">Implantando servidores de mediação e definindo pontos</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure um tronco entre um Servidor de Mediação e um ou mais dos seguintes pares para oferecer conectividade de PSTN (Rede Telefônica Pública Comutada).</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">Configurando troncos</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Crie e configure um plano de discagem do Lync e crie, define e associe regras de normalização.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">Configurar planos de discagem</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure políticas de voz e defina o uso de telefone e rotas de chamada de saída.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">Configurando políticas de voz, registros de uso do PSTN e rotas de voz</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Execute utilitário de Integração do Exchange (ocsumutil.exe), que cria os objetos de contato para o Outlook Voice Access e para os atendedores automáticos.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">Configurar o Lync Server 2013 para trabalhar com o Unified Messaging no Microsoft Exchange Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Defina, implante e configure quaisquer recursos avançados do Enterprise Voice necessários.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">Implantando avançadas recursos do Enterprise Voice</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Habilite os usuários para o Enterprise Voice. Insira uma URI de linha e atribua uma política de voz e um plano de discagem do Lync.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">Habilitar usuários para o Enterprise Voice</a></p></td>
</tr>
</tbody>
</table>

