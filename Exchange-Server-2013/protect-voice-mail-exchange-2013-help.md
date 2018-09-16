---
title: 'Caixa postal protegida: Exchange 2013 Help'
TOCTitle: Caixa postal protegida
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52058510
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Caixa postal protegida

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Alguns herdado Private Branch eXchange (PBX) e os sistemas de telefonia IP PBX permitir que o chamador marcar uma mensagem de email de voz como particular, bloquear o destinatário pretendido da mensagem encaminhem a outras pessoas. Em sistemas de correio de voz integrados, uma mensagem de voz pode ser acessada de várias maneiras, que permite que mais de um desafio para evitar mensagens de voz marcado como particulares sejam expostas aos ouvintes indesejadas.

Unified Messaging (UM) pode ser configurado para usar Active Directory Rights Management Services (AD RMS) para proteger as mensagens de voz para uma organização. Esse recurso é conhecido como caixa postal protegida.

Quando uma mensagem de voz está protegida, o destinatário não está bloqueado somente para encaminhamento da mensagem, mas UM também garante que apenas o destinatário pretendido ou destinatários da mensagem podem acessar seu conteúdo. Mensagens de voz protegida podem ser acessados por meio de MicrosoftOutlook 2010 ou posterior, Outlook Web App ou Outlook Voice Access.

**Sumário**

Visão geral do correio de voz protegido

Visão geral do Active Directory Rights Management Services

Recursos de suporte e do usuário final do cliente

Estrutura de correio de voz protegida

Escrevendo uma mensagem de caixa postal protegida

Políticas de caixa de correio de Unificação de MENSAGENS

Notificações de mensagem de texto e caixa postal protegida

## Visão geral da voz protegida

O recurso de caixa postal protegida está disponível com Exchange 2010 e versões posteriores do Unified Messaging (UM). Ele pode ser configurado em uma diretiva de caixa de correio UM, e todas as configurações de caixa postal protegida podem ser configuradas usando o Console de gerenciamento do Exchange ou o Shell no Exchange 2010 ou usando o Centro de administração (EAC) do Exchange ou cmdlets no Shell em Exchange 2013.

Caixa postal protegida é implementada aplicando o gerenciamento de direitos de informação (IRM) às mensagens de voz. Quando as mensagens de voz são protegidas pela Unificação de MENSAGENS:

  - Os usuários podem responder às mensagens de voz protegida.

  - Destinatários de uma mensagem de voz não podem encaminhá-la.

  - Os usuários não podem salvar uma cópia da mensagem de voz.

  - Os usuários não podem salvar ou copiar o áudio do anexo da mensagem de voz.

  - Uma mensagem de voz pode ser aberta somente pelo destinatário pretendido ou destinatários.

Mensagens de voz de atendimento de chamadas e de mensagens de voz interpessoais (mensagens de voz que são enviadas para um usuário usando o Outlook Voice Access) podem ser protegidas pela Unificação de MENSAGENS. No entanto, a proteção não ser aplicada aos seguintes tipos de mensagens:

  - Mensagens de fax.

  - Mensagens de não-voice. Por exemplo, mensagens de email ou solicitações de reunião, mesmo quando eles são criados usando Outlook Voice Access (respostas de voz).

Voltar ao início

## Visão geral do Active Directory Rights Management Services

AD RMS, um componente do Windows Server 2008 e versões posteriores, está disponível para ajudar a proteger arquivos para que apenas os usuários que o remetente pretende visualizar um arquivo podem fazê-lo. AD RMS protege um arquivo, especificando os direitos que um usuário deve ter para acessar o arquivo. Direitos podem ser configurados para permitir que um usuário abrir, modificar, imprimir, encaminhar ou realizar outras ações com as informações de direitos gerenciados. Com o AD RMS, você pode proteger dados quando ele é distribuído fora da rede.

Um sistema de AD RMS tem um servidor e um componente de cliente, incluindo o seguinte:

  - Um servidor que tenha Windows Server 2008 R2 ou uma versão posterior instalada e que está executando a função de servidor do Rights Management Services Active Directory, que trata de certificados e licenciamento.

  - Um servidor de banco de dados.

  - O cliente do AD RMS. A versão mais recente do cliente do AD RMS é incluída como parte do Windows 7 e os sistemas operacionais Windows 8.

O componente servidor é composto dos vários serviços da web que são executados em um servidor de Microsoft como Windows Server 2008 ou uma versão posterior. O componente cliente pode ser executado no sistema operacional de um cliente ou o servidor e inclui as funções que permitem que um aplicativo para criptografar e descriptografar o conteúdo, recuperar modelos e listas de revogação e adquirir licenças e certificados em um servidor.

Usando o AD RMS e o cliente AD RMS, você pode aumentar a estratégia de segurança de uma organização protegendo as informações por meio de diretivas de uso persistentes que permanecem com as informações, independentemente de onde ela será movida. Você pode usar o AD RMS para ajudar a evitar que informações confidenciais — como relatórios financeiros, especificações de produtos, dados do cliente e mensagens de email de voz e email confidenciais — intencionalmente ou acidentalmente fique em mãos erradas. Para obter informações detalhadas, consulte [Visão geral do AD RMS](https://go.microsoft.com/fwlink/p/?linkid=199436).

Em UM do Exchange, você pode usar os recursos de gerenciamento de direitos de informação (IRM) para aplicar a proteção persistente para mensagens e anexos.

Usando os recursos de IRM e caixa postal protegida, sua organização e os usuários podem controlar os direitos destinatários tem para acessar mensagens de voz e email. IRM também pode ser usado para restringir o destinatários ações como encaminhamento de uma mensagem para os outros destinatários, imprimir uma mensagem ou um anexo ou extrair o conteúdo de anexo ou mensagem copiando e colando.

## Requisitos de IRM

Antes de implementar IRM no Exchange, você deve primeiro implantar e configurar sua infraestrutura do AD RMS. Para obter informações detalhadas, consulte [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=199439). Para implementar o IRM para oferecer suporte à caixa postal protegida em sua organização do Exchange, sua implantação deve atender aos seguintes requisitos.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cluster do AD RMS</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard ou Enterprise com SP1 ou Windows Server 2012 Standard ou Datacenter. Para obter mais informações sobre requisitos do sistema, consulte <a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</a>.</p></li>
<li><p><strong>Ponto de conexão de serviço (SCP)</strong> Exchange 2013 e aplicativos com reconhecimento de AD RMS usam o SCP registrado no Active Directory descubram URLs e os clusters do AD RMS. AD RMS permite que você registre o SCP dentro da configuração do AD RMS. Se a conta usada para configurar o AD RMS não for um membro do grupo de segurança Administradores corporativos, registro SCP pode ser realizado após a instalação. Há apenas um SCP para o AD RMS em uma floresta Active Directory.   </p></li>
<li><p><strong>Permissões</strong>   Servidores no grupo de servidores Exchange ou individuais Exchange devem ter permissões de leitura e execução para o pipeline de certificação do servidor do AD RMS. O caminho padrão é \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx nos servidores AD RMS.</p></li>
<li><p><strong>Os superusuários do AD RMS</strong>   Para habilitar o IRM, descriptografia do relatório de diário, IRM no Outlook Web App e a descriptografia de transporte para Exchange pesquisa, você deve adicionar a caixa de correio de entrega federados, uma caixa de correio do sistema criada pelo programa de instalação do Exchange, ao grupo de superusuários AD RMS no cluster do AD RMS. Para obter informações detalhadas, consulte <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Configurando e testando o IRM

Você deve usar o Shell para configurar recursos IRM. Para configurar os recursos de IRM individuais, use o cmdlet de [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)) . Para obter mais informações sobre como configurar recursos de IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

Depois de configurar um servidor Exchange, você pode usar o cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979798\(v=exchg.150\)) para realizar testes de ponta a ponta da sua implantação do IRM. Este cmdlet verifica a configuração do IRM para uma organização e deve ser executado antes de habilitar a caixa postal protegida. O cmdlet **Test-IRMConfiguration** executa os seguintes testes:

  - Inspeciona a configuração do IRM para sua organização do Exchange.

  - Verifica se o servidor do AD RMS para obter informações de versão e hotfix.

  - Verifica se um servidor de Exchange pode ser ativado por RMS, recuperando um certificado de conta de direitos e um certificado de licenciante do cliente (CLC).

  - Adquire modelos de diretiva de direitos do AD RMS do servidor do AD RMS.

  - Verifica se o remetente especificado pode enviar mensagens protegidas com IRM.

  - Recupera uma licença de uso de superusuário para o destinatário especificado.

  - Adquire uma licença prévia para o destinatário especificado.

Voltar ao início

## Recursos de suporte e do usuário final do cliente

O software de cliente de email que é usado para ouvir uma mensagem de caixa postal protegida deve oferecer suporte ao IRM e saber como ler uma mensagem de voz da Unificação de MENSAGENS protegidas. Clientes de email que são suportados incluem MicrosoftOutlook 2010 ou versões posteriores, Outlook Web App e Outlook Voice Access. A tabela a seguir contém uma lista de clientes de email e se eles são suportados.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente de email</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Protegido voz mensagens são suportadas no Outlook 2010 e versões posteriores.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Outlook Web App em Exchange 2010 ou versões posteriores oferece suporte a mensagens de caixa postal protegida. Versões anteriores do Outlook Web App, conhecido como Outlook Web Access, não há suporte para eles.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook Voice Access</p></td>
<td><ul>
<li><p>Outlook Acesso de voz em Exchange 2010 e versões posteriores oferece suporte a caixa postal protegida. Outlook Acesso de voz incluído Exchange 2007 não tem suporte para a caixa postal protegida.</p></li>
<li><p>Caixa de correio do usuário deve residir em um servidor de caixa de correio no Exchange 2010 ou uma versão posterior.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile ou Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile não oferece suporte a caixa postal protegida. No entanto, o Windows Phone 7 e Windows Phone 8 suportam a caixa postal protegida.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Caixa postal protegida é suportada no Exchange 2010 SP1 e versões posteriores.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outros clientes de email</p></td>
<td><ul>
<li><p>Caixa postal protegida não é suportada.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Voltar ao início

## Estrutura da mensagem de voz protegido

Há realmente duas mensagens envolvidas para cada mensagem de caixa postal protegida. A primeira mensagem é a mensagem externa, que não é criptografada. Ele contém um anexo denominado message.rpmsg. O anexo contém a mensagem de voz protegido por IRM e dados de controle de gerenciamento de direitos internos. Os dados de controle de gerenciamento de direitos incluem uma informações de chave e direitos de conteúdo que especifica quem pode acessar a mensagem de voz e como os usuários podem acessá-lo.

Protegido voz mensagens são mostradas na caixa de entrada do usuário na pasta de pesquisa de **Caixa postal**. O usuário poderá escutar as mensagens de voz usando o reprodutor de áudio incorporado, assim como seria ouvir a uma mensagem de voz regular, exceto que o botão encaminhar será desabilitado e uma nota será mostrada na parte superior da mensagem informando que ele estiver protegido e que ele não pode ser encaminhado.

Para clientes de email que não há suporte para caixa postal protegida, será exibido o corpo da mensagem externa. Os administradores podem incluir texto quando o software do cliente não tem suporte para a caixa postal protegida usando políticas de caixa de correio de Unificação de MENSAGENS. Você pode personalizar o texto padrão que está incluído na mensagem de email, definindo uma política de caixa de correio de Unificação de MENSAGENS. Por exemplo, você poderia configurar a política de caixa de correio de Unificação de MENSAGENS com texto personalizado, como *"You can't open this voice mail message because it's protected. To view or listen to this voice message, sign in to your mailbox at https://mail.contoso.com or call +1 (425) 555-1234 to call in to Outlook Voice Access."*

Voltar ao início

## Escrevendo uma mensagem de caixa postal protegida

Há duas situações em que mensagens de voz protegida podem ser criadas:

  - **Atendimento de chamadas**   Atendimento de chamadas ocorre quando um chamador chama um usuário habilitado, mas o usuário não está disponível para atender a chamada ou encaminha diretamente para a caixa postal. Em cenários de atendimento de chamadas, o sistema de caixa postal será reproduzido uma série de prompts de voz depois que o chamador registra uma mensagem de voz.
    
    O chamador pode escolher adicionais nas opções da mensagem, incluindo a opção para marcar a mensagem de voz como particular pressionando a tecla de cerquilha (\#). Se o chamador pressionar a tecla \#, eles podem siga as instruções fornecidas pela Unificação de MENSAGENS para marcar a mensagem como particular, remova a marcação privada a mensagem de voz privada ou marcar a mensagem de voz com alta prioridade. O diagrama a seguir mostra as opções de menu que estão disponíveis para os chamadores quando eles deixam uma mensagem de voz privada para um usuário.
    

    > [!NOTE]
    > Para chamadas de atendimento de chamadas, o UM utiliza as configurações de caixa postal protegida na política de caixa de correio de Unificação de MENSAGENS do destinatário da mensagem, porque o chamador não seja autenticado.

    
    **Criar uma mensagem de caixa postal protegida usando atendimento de chamada**
    
    ![Criar mensagem de voz protegida usando atendimento de chamadas](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "Criar mensagem de voz protegida usando atendimento de chamadas")  

  - **Outlook Voice Access** Outlook Acesso de voz permite o acesso de usuários habilitados para UM suas caixas de correio usando analógico, digital ou telefones celulares discando seus Outlook número de acesso de voz. Existem duas interfaces de usuário para Unificação de mensagens disponível para usuários habilitados para UM: a interface do usuário de telefone (TUI) e a interface de usuário de voz (VUI).   
    
    Outlook Usuários de acesso de voz podem pesquisar contatos no diretório e enviar-lhes mensagens de voz. Se a caixa postal protegida tiver sido habilitada para os destinatários habilitado, os chamadores podem marcar as mensagens como particular após eles estão registrados. Como alternativa, os administradores podem configurar uma política de caixa de correio de Unificação de MENSAGENS para garantir que todas as mensagens de voz enviadas por usuários autenticados são protegidas pela Unificação de MENSAGENS.
    

    > [!NOTE]
    > Se um chamador for autenticado, são aplicadas as configurações de caixa postal protegida na diretiva de caixa de correio de Unificação de MENSAGENS que está vinculada ao chamador, independentemente das configurações de diretiva de caixa de correio de Unificação de MENSAGENS para o destinatário pretendido da mensagem de voz.

    
    **Criar uma mensagem de caixa postal protegida usando a interface de usuário de voz**
    
    ![Criar mensagem de voz protegida usando interface de voz](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "Criar mensagem de voz protegida usando interface de voz")  
    
    **Criar uma mensagem de caixa postal protegida usando a interface do usuário de telefone**
    
    ![Criar mensagem de voz protegida usando a entrada de discagem por tom](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "Criar mensagem de voz protegida usando a entrada de discagem por tom")  

Voltar ao início

## políticas de caixa de correio de UM

Você pode criar uma política de caixa de correio de Unificação de mensagens para aplicar um conjunto comum de configurações de diretiva de Unificação de MENSAGENS, como configurações de diretiva PIN, restrições de discagem e configurações de caixa postal protegida, a uma coleção de caixas de correio habilitadas para UM. Para saber mais sobre políticas de caixa de correio de Unificação de MENSAGENS, consulte [Gerenciar uma política de caixa de correio de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy).

Você pode usar o EAC ou o cmdlet **Set-UMMailboxPolicy** no Shell para configurar as opções de caixa postal protegida. A tabela a seguir lista as configurações que podem ser configuradas para caixa postal protegida.

**Configurações de caixa postal protegidas**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro Shell</th>
<th>Configuração disponíveis no EAC?</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>ProtectAuthenticatedVoiceMail</em> Especifica se habilitado os usuários podem enviar mensagens de voz protegida quando estiver acessando suas caixas de correio usando Outlook Voice Access. A configuração padrão é <code>None</code>. Isso significa que nenhuma proteção é aplicada quando as mensagens de voz são compostas e que os chamadores não terão a opção de marcar mensagens de voz como particular. Se o valor é definido como <code>Private</code>, somente as mensagens marcadas como particulares pelo chamador estão protegidas. Se o valor é definido como <code>All</code>, todas as mensagens de voz estiver protegida, independentemente da opção escolhida pelo chamador.</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>ProtectUnauthenticatedVoiceMail</em> Especifica se os servidores de caixa de correio que atender a chamadas para usuários habilitados para UM associados a uma diretiva de caixa de correio UM criam mensagens de voz protegida. Essa configuração também se aplica quando uma mensagem é enviada de um atendedor automático para um usuário habilitado para UM. A configuração padrão é <code>None</code>. Isso significa que nenhuma proteção é aplicada às mensagens de voz e que o chamador não é oferecido a opção para marcar a mensagem como particular. Se o valor é definido como <code>Private</code>, somente as mensagens marcadas como particulares pelo chamador estão protegidas. Se o valor é definido como <code>All</code>, todas as mensagens de voz estiver protegida, independentemente se a mensagem foi marcada como particular pelo chamador.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>ProtectedVoiceMailText</em> Especifica o texto a ser incluído no corpo da mensagem externa de uma mensagem de caixa postal protegida. Esse texto será mostrado em todos os aplicativos de cliente de email que não há suporte para mensagens de caixa postal protegida. Observe que uma mensagem padrão sempre é fornecida pela Unificação de MENSAGENS quando essa propriedade estiver definida como <code>Null</code> ou está vazia.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>RequireProtectedPlayOnPhone</em> Especifica se os usuários associados a diretiva de caixa de correio de Unificação de MENSAGENS serão forçados para ouvir a mensagem de voz protegida por telefone (usando tocar no telefone). O valor padrão é <code>$false.</code> quando o valor é definido como <code>$true</code>, o áudio de media player nos formulários de caixa postal protegida em Outlook ou Outlook Web App serão exibidos como desabilitado. Observe que o texto de visualização para a mensagem de voz sempre pode ser acessado. O usuário não pode reproduzir o arquivo de áudio usando qualquer software de player de mídia ou usar o player de mídia incorporada para ouvir a mensagem de voz.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>AllowVoiceResponseToOtherMessageTypes</em> Especifica se chamadores que foram autenticadas em Outlook Voice Access para acessar seus emails poderão redigir uma resposta de voz para mensagens de email e solicitações de reunião.</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre como gerenciar as configurações de caixa postal protegida, consulte [Procedimentos de caixa postal protegidos](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/protected-voice-mail-procedures) ou [Set-UMMailboxPolicy](https://technet.microsoft.com/pt-br/library/bb124903\(v=exchg.150\)).

Voltar ao início

## Notificações de mensagem de texto e caixa postal protegida

Os usuários que configurar sua conta da Unificação de MENSAGENS para enviar texto notificações de mensagens (também chamadas de notificações de SMS) para seu telefone móvel quando mensagens de voz são recebidas também receberá texto transcrições de áudio (visualização da caixa postal) como parte do corpo da mensagem de texto. No entanto, para mensagens de voz protegida, isso representa um problema de segurança porque o conteúdo das mensagens de voz sempre deve ser protegido.

Quando UM cria uma notificação de mensagem de texto para uma mensagem de voz que estiver protegida, ele verifica se a mensagem de voz está marcada como particular. Em caso afirmativo, ele não adicionará o texto de áudio transcrita na mensagem de texto que ele envia para o telefone celular. O seguinte texto será incluído na mensagem de texto em vez disso: "Usar Outlook Voice Access para acessar essa mensagem de voz protegido".

Voltar ao início

