---
title: 'Assistente de Configuração Híbrida: Exchange 2013 Help'
TOCTitle: Assistente de Configuração Híbrida
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 50487109
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Assistente de Configuração Híbrida

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

Esse tópico oferece a você uma visão geral do processo de configuração de implantação híbrida do Exchange, dos recursos de implantação híbrida e das opções disponíveis a você e o Mecanismo de Configuração Híbrida, que executa as principais ações necessárias para configurar e atualizar uma implantação híbrida.

Para mais informações sobre implantações híbridas, consulte [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

**Sumário**

Processo de configuração híbrida

Recursos da configuração híbrida

Opções de configuração híbrida

Mecanismo de Configuração Híbrida

## Processo de configuração híbrida

Aqui está uma rápida visão geral do processo do assistente de Configuração Híbrida. Primeiro, o assistente cria o objeto **HybridConfiguration** em seu Active Directory local. Esse objeto do Active Directory armazena as informações da configuração híbrida para a implantação híbrida e é atualizado pelo assistente de Configuração Híbrida. Depois, o assistente reúne dados existentes de configuração de topologia locais do Exchange e do Active Directory, dados de configuração do locatário do Office 365 e do Exchange Online, define diversos parâmetros da organização e depois executa uma sequência extensa de tarefas de configuração nas organizações locais e do Exchange Online.


> [!IMPORTANT]
> Há várias considerações e pré-requisitos que você precisa atender antes de poder usar o assistente de Configuração Híbrida. Você precisa atender aos requisitos para implantações híbridas descritos em <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Pré-requisitos de implantação híbrida</A>. Depois, você estará pronto para usar o assistente de Configuração Híbrida para configurar sua organização do Exchange para a implantação híbrida.



As fases gerais do processo de configuração de implantação híbrida são:

1.  **Verificar os pré-requisitos e realizar verificações da topologia**   O assistente de Configuração Híbrida verifica se suas organizações locais e do Exchange Online suportam uma implantação híbrida. Alguns dos itens que o assistente verifica nas organizações local e do Exchange Online são:
    
      - Versões do servidor Exchange no local
    
      - Versão do Exchange Online
    
      - Configuração e presença de sincronização do Active Directory
    
      - Domínios federados e aceitos
    
      - Relações de confiança de federação e organização existentes
    
      - Diretórios virtuais de Serviços Web
    
      - Certificados do Exchange

2.  **Testar credenciais de conta**   Determinadas contas de gerenciamento híbrido local e do Office 365 acessam as organizações locais e do Exchange Online para coletar informações de verificação de pré-requisitos e fazer alterações na configuração dos parâmetros da organização a fim de habilitar a funcionalidade de implantação híbrida. O assistente de Configuração Híbrida verifica se as contas têm as credenciais adequadas e podem se conectar às organizações locais e do Exchange Online. As contas de gerenciamento da implantação híbrida para as organizações locais e do Office 365 precisam ser membros do grupo de função Gerenciamento de Organização para que o assistente de Configuração Híbrida possa concluir essas tarefas com êxito.

3.  **Fazer alterações de configuração na implantação híbrida**   Depois de testar as contas de gerenciamento híbrido, conduzir as verificações gerais e de topologia e coletar as informações de configuração definidas no processo do assistente, o assistente de Configuração Híbrida fará as alterações de configuração para criar e habilitar a implantação híbrida. Todas as alterações na configuração híbrida são automaticamente registradas no log de configuração híbrida. Por padrão, o log de configuração híbrida está localizado no servidor de Caixa de Correio local em `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`.
    

    > [!IMPORTANT]
    > O fluxo de mensagens de entrada é controlado pelo registro MX da sua organização. O email de entrada da Internet para uma implantação híbrida não é configurado pelo assistente de Configuração Híbrida.



## Recursos da configuração híbrida

Por padrão, o assistente de Configuração Híbrida habilita automaticamente todos os recursos da implantação híbrida sempre que é executado. Se deseja desabilitar recursos de configuração híbrida específicos, você precisa usar o Shell de Gerenciamento do Exchange e o cmdlet **Set-HybridConfiguration**. Os seguintes recursos de implantação híbrida são habilitados por padrão pelo assistente:

  - **Compartilhamento de informações de disponibilidade**   O recurso de compartilhamento de informações de disponibilidade habilita o compartilhamento de informações de calendário entre usuários das organizações locais e do Exchange Online. O compartilhamento de informações de disponibilidade é habilitado como parte do compartilhamento federado e da configuração do relacionamento de organização para as organizações locais e do Exchange Online. Saiba mais em [Compartilhamento](https://technet.microsoft.com/pt-br/library/dd638083\(v=exchg.150\)).

  - **Dicas de Email**   As Dicas de Email são mensagens informativas exibidas aos usuários enquanto eles compõem uma mensagem. Com a habilitação das Dicas de Email na implantação híbrida, os remetentes no local e do Exchange Online podem ajustar as mensagens que compõem para evitar situações indesejadas ou notificações de falha na entrega (NDRs) entre as organizações. Saiba mais em [MailTips](https://technet.microsoft.com/pt-br/library/jj649091\(v=exchg.150\)).

  - **Arquivamento online**   O arquivamento online permite que a organização do Exchange Online hospede arquivos mortos de email de usuários para usuários locais e do Exchange Online. Saiba mais em [Configurar o Arquivamento do Exchange Online](http://go.microsoft.com/fwlink/p/?linkid=266565).

  - **Redirecionamento do Outlook na Web**   O redirecionamento do Outlook na Web fornece uma URL única e comum para acesso às caixa de correio local e do Exchange Online. Os servidores de Acesso para Cliente redirecionam automaticamente as solicitações do Outlook na Web para o servidor de caixa de correio no local ou fornece um link aos usuário para suas caixas de correio na organização do Exchange Online.

  - **Redirecionamento do Exchange ActiveSync**  Quando você move uma caixa de correio de sua organização do Exchange local para o Exchange Online, todos os clientes que acessam a caixa de correio precisam ser atualizados para usar o Exchange Online. Isso inclui dispositivos do Exchange ActiveSync. A maioria dos clientes do Exchange ActiveSync é automaticamente reconfigurada quando a caixa de correio é movida para o Exchange Online. Para mais informações, consulte [Configurações de dispositivo do Exchange ActiveSync com implantações híbridas do Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Email seguro**    O Email seguro permite a entrega segura de mensagens entre a organização local e do Exchange Online usando o protocolo TLS. A organização local e do Exchange Online são autenticadas mutuamente através dos assuntos de certificado digital; os cabeçalhos de email e o formato da mensagem de rich text são preservados nas organizações.

## Opções de configuração híbrida

O assistente de Configuração Híbrida permite selecionar opções específicas em várias áreas de uma implantação híbrida. Se desejar atualizar as opções de configuração híbrida específicas após configurar inicialmente sua implantação híbrida, você pode usar o assistente de Configuração Híbrida ou Shell de Gerenciamento do Exchange para selecionar diferentes opções de configuração.

A tabela a seguir destaca as principais opções que o assistente de Configuração Híbrida modifica e configura.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Área de configuração</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domínios</p></td>
<td><p>O assistente adiciona um domínio aceito à organização local para um fluxo de email híbrido e solicitações de Descoberta Automática para a organização em nuvem. Esse domínio, chamado de <em>domínio de coexistência</em>, é adicionado como um domínio de proxy secundário a quaisquer políticas de endereço de email que tenham modelos de <em>PrimarySmtpAddress</em> para domínios selecionados no assistente de Configuração Híbrida. Por padrão, esse domínio é o &lt;domínio&gt;.mail.onmicrosoft.com.</p>
<p>Você pode exibir o domínio aceito executando o comando a seguir no Shell de Gerenciamento do Exchange no Exchange Online.</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>Certificado de email seguro</p></td>
<td><p>O assistente exige que você selecione um certificado específico emitido por uma Autoridade de Certificação (CA) de terceiros que seja usado para autenticar e garantir a segurança de mensagens de email enviadas entre as organizações local e do Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Compartilhamento federado do Exchange</p></td>
<td><p>O assistente verifica se há uma relação de autenticação de OAuth ou uma confiança de federação com o sistema de autenticação doAzure Active Directory para a organização local. Se houver, a autenticação OAuth ou a confiança de federação existente será usada para suportar a implantação híbrida. Caso contrário, o assistente configurará a autenticação OAuth ou criará uma confiança de federação para a organização local com o sistema de autenticação do AD do Azure, dependendo do tipo de configuração do Exchange local. O assistente também adiciona qualquer domínio selecionado no assistente de Configuração Híbrida à confiança de federação, caso seja necessário.</p>
<p>Além da autenticação OAuth e da configuração da confiança de federação, o assistente também cria e configura relações organizacionais para as organizações locais e do Exchange Online. Essas relações organizacionais permitem que o assistente habilite diversos recursos da implantação híbrida, incluindo compartilhamento de informações de disponibilidade, redirecionamento do Outlook na Web e Dicas de Email.</p></td>
</tr>
<tr class="even">
<td><p>Fluxo de mensagens</p></td>
<td><p>O assistente permite que você selecione e configure os servidores do Exchange para manipular o transporte de mensagem segura entre as organizações locais e do Exchange Online. No Exchange 2010, este é um servidor de Transporte de Hub. No Exchange 2013 , este é o servidor de Acesso para Cliente. No Exchange 2016 e mais recente, este é um servidor de Caixa de Correio.</p>
<p>O assistente configura a organização do Exchange e Exchange Online para o roteamento híbrido de mensagens. Com a configuração dos conectores de Envio e Recebimento novos e existentes na organização local e dos conectores de Entrada e Saída no Exchange Online, o assistente permite escolher se as mensagens de saída entregues para a Internet pela organização do Exchange Online serão enviadas diretamente aos destinatários de email externos ou roteadas através dos servidores do Exchange locais incluídos na implantação híbrida.</p>

> [!IMPORTANT]
> O fluxo de mensagens de entrada é controlado pelo registro MX da sua organização. O email de entrada da Internet para uma implantação híbrida não é configurado pelo assistente de Configuração Híbrida.


</td>
</tr>
</tbody>
</table>


## Mecanismo de Configuração Híbrida

O Mecanismo de Configuração Híbrida executa as principais ações necessárias para a configuração e atualização de uma implantação híbrida. Responsável pelo processamento das ações do cmdlet `Update-HybridConfiguration`, o Mecanismo de Configuração Híbrida compara o estado do objeto *HybridConfiguration*Active Directory com as definições de configuração atual do Exchange local e do Exchange Online. Em seguida, ele executa tarefas para comparar as definições de configuração da implantação aos parâmetros definidos no objeto *HybridConfiguration*Active Directory. Se os estados da configuração atual da implantação do Exchange local e do Exchange Online corresponderem às configurações definidas no objeto *HybridConfiguration*Active Directory, nenhuma alteração é feita pelo Mecanismo de Configuração Híbrida nas organizações do Exchange local e do online.

Ao atualizar uma implantação híbrida existente, o Mecanismo de Configuração Híbrida executa as seguintes etapas:

1.  O cmdlet *Update-HybridConfiguration* dispara o Mecanismo de Configuração Híbrida para iniciar.

2.  O Mecanismo de Configuração Híbrida lê o "estado desejado" armazenado no objeto `HybridConfiguration`Active Directory.

3.  O Mecanismo de Configuração Híbrida descobre os dados de topologia e a configuração atual da organização do Exchange local.

4.  O Mecanismo de Configuração Híbrida descobre os dados de topologia e a configuração atual da organização do Exchange Online.

5.  Com base no estado desejado, nos dados de topologia e na configuração atual, o Mecanismo de Configuração Híbrida estabelece a "diferença" entre as organizações locais do Exchange e do Exchange Online e depois executa tarefas de configuração para estabelecer o estado desejado.

A figura a seguir mostra um resumo de como o Mecanismo de Configuração Híbrida recupera e modifica as definições de configuração do servidor Exchange local e do Exchange Online durante o processo de implantação híbrida.

![Fluxo do Mecanismo de Configuração Híbrida](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "Fluxo do Mecanismo de Configuração Híbrida")

