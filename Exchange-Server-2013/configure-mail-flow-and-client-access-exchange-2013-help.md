---
title: 'Configurar o acesso de cliente e o fluxo de email: Exchange 2013 Help'
TOCTitle: Configurar o acesso de cliente e o fluxo de email
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50485537
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o acesso de cliente e o fluxo de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Tarefas de pós-instalação para Exchange Server 2013 mail flow e acesso do cliente, incluindo como configurar um certificado SSL.

Depois de você ter instalado do Microsoft Exchange Server 2013 na sua organização, você precisa configurar o Exchange Server 2013 para fluxo de email e acesso para clientes. Sem estas etapas adicionais, você não poderá enviar emails para a Internet e clientes externos, como dispositivos do Microsoft Office Outlook e ActiveSync, não poderão se conectar à sua organização do Exchange.

As instruções neste tópico consideram uma implantação básica do Exchange com um único site do Active Directory e um único namespace de protocolo de transporte simples de email (SMTP).


> [!IMPORTANT]
> Este tópico usa valores de exemplo, como Ex2013CAS, contoso.com, mail.contoso.com e 172.16.10.11. Substitua os valores por nomes de servidor, FQDNs e endereços IP da sua organização.



Para conhecer tarefas de gerenciamento adicionais relacionadas ao fluxo de email e clientes e dispositivos, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md) e [Clientes e dispositivos móveis](clients-and-mobile-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 50 minutos

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Você poderá receber avisos de certificado ao se conectar ao site do Centro de administração do Exchange (EAC) até configurar um certificado de SSL em um servidor de Acesso para Cliente. Mostraremos como fazer isso ainda neste tópico.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!IMPORTANT]
> Cada organização precisa de, no mínimo, um servidor de Acesso para Cliente e um servidor de Caixa de Correio na floresta do Active Directory. Além disso, todo site do Active Directory que contenha um servidor de Caixa de Correio também deve conter um servidor de Acesso para Cliente, pelo menos. Se você estiver separando suas funções de servidor, recomendamos instalar primeiro a função de servidor Caixa de Correio.




> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar um conector de envio

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de envio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

Antes de você poder enviar emails para a Internet, você precisará criar um conector de Envio no servidor de Caixa de Correio. Faça o seguinte.

1.  Abra o EAC navegando até a URL do seu servidor de Acesso para Cliente. Por exemplo, https://Ex2013CAS/ECP.

2.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e clique em **Entrar**.

3.  Vá até **Fluxo de emails** \> **Conectores de Envio**. Na página **Conectores de Envio**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  No assistente **Novo conector de envio**, especifique um nome para o conector de Envio e selecione **Internet**. Clique em **Avançar**.

5.  Verifique se **Registro MX associado ao domínio do destinatário** está selecionado. Clique em **Avançar**.

6.  Em **Espaço de endereçamento**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar domínio**, certifique-se de que **SMTP** esteja selecionado, no campo **Tipo**. No campo **Nome de Domínio Totalmente Qualificado (FQDN)**, digite **\***. Clique em **Salvar**.

7.  Certifique-se de que a caixa de seleção **Conector de envio com escopo** está desmarcada e clique em **Avançar**.

8.  Em **Servidor de origem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Selecionar um Servidor**, selecione um servidor de Caixa de Correio. Após selecionar o servidor, clique em **Adicionar** e em **OK**.

9.  Clique em **Concluir**.


> [!TIP]
> Um conector de Recebimento de entrada padrão é criado quando Exchange 2013 é instalado. Esse conector de Recebimento aceita conexões SMTP anônimas de servidores externos. Você não precisa de nenhuma configuração adicional, se essa for a funcionalidade que você desejar. Se você quiser restringir as conexões de entrada de servidores externos, modifique o conector de Recebimento <STRONG>Frontend Padrão &lt;servidor de Acesso para Cliente&gt;</STRONG> no servidor de Acesso para Cliente.



## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito um conector de Envio, faça o seguinte:

1.  No EAC, verifique se o novo conector de Envio aparece em **Fluxo de email** \> **Conectores de Envio**.

2.  Abra o Outlook Web App e envie um email para um destinatário externo. Se o destinatário receber a mensagem, você configurou com êxito o conector de Envio.

## Etapa 2: Adicionar domínios aceitos

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios aceitos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

Por padrão, quando você implanta uma nova organização do Exchange 2013 em uma floresta do Active Directory, o Exchange usa o nome do domínio do Active Directory em que Setup /PrepareAD foi executado. Se você quiser que os destinatários recebam e enviem mensagens de e para outro domínio, você deve adicionar o domínio como um domínio aceito. Este domínio também é adicionado como o endereço SMTP principal na política de endereço de email padrão, na próxima etapa.


> [!IMPORTANT]
> Um registro de recurso MX de Sistema de Nome de Domínio (DNS) público é necessário para cada domínio SMTP para o qual você aceita emails da Internet. Cada registro MX deve determinar o servidor voltado para a Internet que recebe emails para a sua organização.



1.  Abra o EAC navegando até a URL do seu servidor de Acesso para Cliente. Por exemplo, https://Ex2013CAS/ECP.

2.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e clique em **Entrar**.

3.  Vá até **Fluxo de emails** \> **Domínios aceitos**. Na página **Domínios Aceitos**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  No assistente de **Novo domínio aceito**, especifique um nome para o domínio aceito.

5.  No campo **Domínio aceito**, especifique o domínio do destinatário SMTP que você deseja adicionar. Por exemplo, contoso.com.

6.  Selecione **Domínio autoritativo** e clique em **Salvar**.

## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito um domínio aceito, faça o seguinte:

  - No EAC, verifique se o novo domínio aceito aparece em **Fluxo de email** \> **Domínios aceitos**.

## Etapa 3: Configurar a política de endereço de email padrão

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o entrada "diretivas de endereço de email" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

Se você tiver adicionado um domínio aceito na etapa anterior e quiser que esse domínio seja adicionado a cada destinatário na organização, você precisará atualizar a política de endereço de email padrão.

1.  Abra o EAC navegando até a URL do seu servidor de Acesso para Cliente. Por exemplo, https://Ex2013CAS/ECP.

2.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e clique em **Entrar**.

3.  Vá até **Fluxo de emails** \> **Políticas de endereços de email**. Na página **Políticas de endereços de email**, selecione **Política Padrão** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Na página **Política de Endereço de Email Padrão**, clique em **Formato do Endereço de Email**.

5.  Em **Formato de endereço de email**, clique no endereço SMTP que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

6.  Na página **Formato do endereço de email**, no campo **Parâmetros de endereço de email**, especifique o domínio do destinatário SMTP que você deseja aplicar a todos os destinatários na organização do Exchange. Esse domínio deve corresponder ao domínio aceito que você adicionou na etapa anterior. Por exemplo, @contoso.com. Clique em **Salvar**.

7.  Clique em **Salvar**

8.  No painel de detalhes **Política Padrão**, clique em **Aplicar**.


> [!TIP]
> Recomendamos que você configure um nome principal de usuário (UPN) que corresponda ao endereço de email principal de cada usuário. Se você não fornecer um UPN que corresponda ao endereço de email de um usuário, o usuário dever fornecer manualmente seu domínio\nome de usuário ou UPN, além de seu endereço de email. Se o UPN dele corresponder ao endereço de email, o Outlook Web App, o ActiveSync e o Outlook irão automaticamente comparar o endereço de email ao UPN.



## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito a política de email de endereço padrão, faça o seguinte:

1.  No EAC, vá até **Destinatários** \> **Caixas de Correio**.

2.  Selecione uma caixa de correio e, no painel de detalhes de destinatário, verifique se o campo **Caixa de correio de usuário** foi definido para *\<alias\>*@*\<novo domínio aceito\>*. Por exemplo, david@contoso.com.

3.  Uma opção é criar uma nova caixa de correio e verificar se ela recebeu um endereço de email com o novo domínio aceito, fazendo o seguinte:
    
    1.  Vá até **Destinatários** \> **Caixas de Correio**, clique em **Novo** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione **Caixa de correio do usuário**.
    
    2.  Na página Caixa de correio de novo usuário, forneça as informações necessárias para criar uma nova caixa de correio. Clique em **Salvar**.
    
    3.  Selecione a nova caixa de correio e, no painel de detalhes de destinatário, verifique se o campo **Caixa de correio de usuário** foi definido para *\<alias\>*@*\<novo domínio aceito\>*. Por exemplo, david@contoso.com.

## Etapa 4: Configurar URLs externas

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações de diretório virtual do *\<Serviço\>*", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Antes que os clientes possam se conectar a seu novo servidor da Internet, é preciso os domínios externos, ou as URLs, nos diretórios virtuais do servidor de Acesso para Cliente e então configurar seus registros de DNS públicos. As instruções abaixo configuram o mesmo domínio externo na URL externa de cada diretório virtual. Se você quiser configurar domínios externos diferentes em um ou mais URLs externas de diretórios virtuais, precisará configurar as URLs externas manualmente. Para obter mais informações, consulte [Gerenciamento de diretório virtual](virtual-directory-management-exchange-2013-help.md).

1.  Abra o EAC navegando até a URL do seu servidor de Acesso para Cliente. Por exemplo, https://Ex2013CAS/ECP.

2.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e clique em **Entrar**.

3.  Vá até **Servidores** \> **Servidores**, selecione o nome do servidor de Acesso para Cliente voltado para a Internet e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Clique em **Outlook em Qualquer Lugar**.

5.  No campo **Especificar o nome de host externo**, especifique o FQDN acessível externamente no servidor de Acesso para Cliente. Por exemplo, mail.contoso.com.

6.  Já que estamos aqui, vamos também definir o FQDN acessível internamente do servidor de Acesso para Cliente. No campo **Especificar o nome de host interno**, insira o FQDN que você usou na etapa anterior. Por exemplo, mail.contoso.com.

7.  Clique em **Salvar**.

8.  Vá até **Servidores** \> **Diretórios virtuais** e clique em **Configurar domínio de acesso externo**![Configurar ícone](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "Configurar ícone").

9.  Em **Selecione os servidores de Acesso para Cliente a serem usados com a URL externa**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")

10. Selecione os servidores de Acesso para Cliente que você deseja configurar e clique em **Adicionar**. Depois de você ter adicionado todos os servidores de Acesso para Cliente que você quiser configurar, clique em **OK**.

11. Em **Inserir o nome de domínio que você irá usar com seus servidores externos de Acesso para Cliente**, digite o domínio externo que você deseja aplicar. Por exemplo, mail.contoso.com. Clique em **Salvar**.
    

    > [!TIP]
    > Algumas organizações usam um FQDN do Outlook Web App exclusivo, para proteger usuários de alterações no FQDN do servidor subjacente. Muitas organizações usam owa.contoso.com como FQDN do Outlook Web App, em vez de mail.contoso.com. Se você quiser configurar um FQDN do Outlook Web App exclusivo, faça o seguinte, após concluir a etapa anterior. Esta lista de verificação pressupõe que você configurou um FQDN do Outlook Web App exclusivo. 
    > <OL>
    > <LI>
    > <P>Selecione <STRONG>owa (Site da Web Padrão)</STRONG> e clique em <STRONG>Editar</STRONG>&nbsp;<IMG title="Ícone de edição" alt="Ícone de edição" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">.</P>
    > <LI>
    > <P>Em <STRONG>URL Externa</STRONG>, digite <STRONG>https://</STRONG>, seguido do FQDN do Outlook Web App exclusivo que você deseja usar, e coloque <STRONG>/owa</STRONG>, no final. Por exemplo, https://owa.contoso.com/owa.</P>
    > <LI>
    > <P>Clique em <STRONG>Salvar</STRONG>.</P>
    > <LI>
    > <P>Selecione <STRONG>ecp (Site da Web Padrão)</STRONG> e clique em <STRONG>Editar</STRONG>&nbsp;<IMG title="Ícone de edição" alt="Ícone de edição" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">.</P>
    > <LI>
    > <P>Em <STRONG>URL Externa</STRONG>, digite <STRONG>https://</STRONG>, seguido do FQDN do Outlook Web App exclusivo que você deseja usar, e coloque <STRONG>/ecp</STRONG>, no final. Por exemplo, https://owa.contoso.com/ecp.</P>
    > <LI>
    > <P>Clique em <STRONG>Salvar</STRONG>.</P></LI></OL>



Depois de você ter configurado a URL externa nos diretórios virtuais do servidor de Acesso para Cliente, você precisará configurar os registros DNS públicos para Descoberta Automática, Outlook Web App e fluxo de emails. Os registros DNS públicos devem apontar para o endereço IP ou FQDN externo do seu servidor de Acesso para Cliente voltado para a Internet e usar os FQDNs acessíveis externamente que você configurou no seu servidor de Acesso para Cliente. A seguir, exemplos de registros DNS recomendados que você deve criar para habilitar o fluxo de emails e a conectividade do cliente externo.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo de registro DNS</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito a URL externa nos diretórios virtuais do servidor de Acesso para Cliente, faça o seguinte:

1.  Na EAC, vá até **Servidores** \> **Diretórios virtuais**.

2.  No campo **Selecionar servidor**, selecione o servidor de Acesso para Cliente voltado para a Internet.

3.  Selecione um diretório virtual e, no painel de detalhes do diretório virtual, verifique se o campo **URL Externa** está preenchido com o FQDN e o serviço corretos, conforme mostrado abaixo:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Diretório virtual</th>
    <th>Valor da URL externa</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Descoberta Automática</strong></p></td>
    <td><p>Nenhuma URL externa exibido</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Para verificar se você configurou com êxito seus registros DNS públicos, faça o seguinte:

1.  Abra um prompt de comando e execute `nslookup.exe`.

2.  Altere para um servidor DNS que pode consultar sua zona DNS pública.

3.  No `nslookup`, procure o registro de cada FQDN que você criou. Verifique se o valor retornado para cada FQDN está correto.

4.  Em `nslookup`, digite `set type=mx` e procure o domínio aceito que você adicionou na Etapa 1. Verifique se o valor retornado corresponde ao FQDN no servidor de Acesso para Cliente.

## Etapa 5: Configurar URLs internas

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações de diretório virtual do *\<Serviço\>*", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Antes que os clientes possam se conectar ao seu novo servidor da Intranet, é preciso os domínios internos, ou as URLs, nos diretórios virtuais do servidor de Acesso para Cliente e então configurar seus registros DNS privados.

O procedimento abaixo permite que você escolha se deseja que os usuários usem a mesma URL na sua Intranet e na Internet para acessar seu servidor Exchange ou se eles deverão usar uma URL diferente. O que você escolhe depende do esquema de endereçamento que você já tem posicionado ou que você deseja implementar. Se estiver implementando um novo esquema de endereçamento, recomendamos que você use a mesma URL para URLs internas e externas. Usar a mesma URL facilita o acesso dos usuários ao servidor Exchange, pois eles precisam memorizar apenas um endereço. Independente da escolha que você fizer, precisará se certificar de configurar uma zona de DNS privado para o espaço de endereçamento que você configurar. Para obter mais informações sobre a administração de zonas DNS, consulte [Administrando um servidor DNS](http://go.microsoft.com/fwlink/p/?linkid=190631).

Para obter mais informações sobre URLs internas e externas em diretórios virtuais, consulte [Gerenciamento de diretório virtual](virtual-directory-management-exchange-2013-help.md).

## Configurar URLs internas e externas para que elas sejam iguais

1.  Abra o Shell de Gerenciamento do Exchange no servidor de Acesso para Cliente.

2.  Armazene o nome de host do seu servidor de Acesso para Cliente em uma variável que será usada na próxima etapa. Por exemplo, Ex2013CAS.
    
        $HostName = "Ex2013CAS"

3.  Execute cada um destes comandos no Shell, para configurar cada URL interna para corresponder à URL externa do diretório virtual.
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  Já que estamos falando no Shell, vamos configurar também o endereço catálogo Offline (OAB) para permitir a descoberta automática selecionar o diretório virtual direita para distribuir o OAB. Execute os seguintes comandos para fazer isso.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Depois de ter configurado a URL interna nos diretórios virtuais do servidor de Acesso para Cliente, você precisará configurar os registros DNS privados para o Outlook Web App e outras conectividades. Dependendo da sua configuração, você precisará configurar seus registros DNS privados de forma que eles apontem para o endereço IP interno ou externo ou para o FQDN (nome de domínio totalmente qualificado) do seu servidor de Acesso para Cliente. Veja a seguir alguns exemplos de registros DNS recomendados que você deve criar para habilitar a conectividade de cliente interna.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo de registro DNS</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito a URL interna nos diretórios virtuais do servidor de Acesso para Cliente, faça o seguinte:

1.  Na EAC, vá até **Servidores** \> **Diretórios virtuais**.

2.  No campo **Selecionar servidor**, selecione o servidor de Acesso para Cliente voltado para a Internet.

3.  Selecione um diretório virtual e clique em **Editar** ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Verifique se o campo **URL Interna** está preenchido com o FQDN e serviço corretos, conforme indicado a seguir:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Diretório virtual</th>
    <th>Valor da URL interna</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Descoberta Automática</strong></p></td>
    <td><p>Nenhuma URL interna exibida</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Para verificar se você configurou com êxito seus registros DNS privados, faça o seguinte:

1.  Abra um prompt de comando e execute `nslookup.exe`.

2.  Altere para um servidor DNS capaz de consultar a zona DNS privada.

3.  No `nslookup`, procure o registro de cada FQDN que você criou. Verifique se o valor retornado para cada FQDN está correto.

## Configurar URLs internas e externas diferentes

1.  Abra o EAC navegando até a URL do seu servidor de Acesso para Cliente. Por exemplo, https://Ex2013CAS/ECP.

2.  Vá até **Servidores** \> **Diretórios virtuais**.

3.  No campo **Selecionar servidor**, selecione o servidor de Acesso para Cliente voltado para a Internet.

4.  Selecione o diretório virtual que você deseja alterar e clique em **Editar** ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

5.  Em **URL Interna**, substitua o nome de host entre **https://** e a primeira barra (**/** ) pelo novo FQDN que você deseja usar. Por exemplo, se você quiser alterar o FQDN do diretório virtual do EWS de Ex2013CAS.corp.contoso.com para internal.contoso.com, altere a URL interna de https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx para https://internal.contoso.com/ews/exchange.asmx.

6.  Clique em **Salvar**.

7.  Repita as etapas 5 e 6 para cada diretório virtual que você deseja alterar.
    

    > [!TIP]
    > As URLs internas de diretório virtual do ECP e do OWA devem ser iguais.<BR>Não é possível definir uma URL interna no diretório virtual de Descoberta Automática.



8.  Finalmente, precisamos abra o Shell e configurar o endereço catálogo Offline (OAB) para permitir a descoberta automática selecionar o diretório virtual direita para distribuir o OAB. Execute os seguintes comandos para fazer isso.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Depois de ter configurado a URL interna nos diretórios virtuais do servidor de Acesso para Cliente, você precisará configurar os registros DNS privados para o Outlook Web App e outras conectividades. Dependendo da sua configuração, você precisará configurar seus registros DNS privados de forma que eles apontem para o endereço IP interno ou externo ou para o FQDN do seu servidor de Acesso para Cliente. A seguir, um exemplo de um registro DNS recomendado que você deve criar para habilitar a conectividade do cliente interno, se tiver configurado suas URLs internas do diretório virtual para usar internal.contoso.com.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo de registro DNS</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito a URL interna nos diretórios virtuais do servidor de Acesso para Cliente, faça o seguinte:

1.  Na EAC, vá até **Servidores** \> **Diretórios virtuais**.

2.  No campo **Selecionar servidor**, selecione o servidor de Acesso para Cliente voltado para a Internet.

3.  Selecione um diretório virtual e clique em **Editar** ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Verifique se o campo **URL Interna** está preenchido com o FQDN correto. Por exemplo, talvez você tenha definido as URLs internas para usar internal.contoso.com.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Diretório virtual</th>
    <th>Valor da URL interna</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Descoberta Automática</strong></p></td>
    <td><p>Nenhuma URL interna exibida</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Para verificar se você configurou com êxito seus registros DNS privados, faça o seguinte:

1.  Abra um prompt de comando e execute `nslookup.exe`.

2.  Altere para um servidor DNS capaz de consultar a zona DNS privada.

3.  No `nslookup`, procure o registro de cada FQDN que você criou. Verifique se o valor retornado para cada FQDN está correto.

## Etapa 6: Configurar um certificado SSL

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de certificado" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

Alguns serviços, como o Outlook em Qualquer Lugar e o Exchange ActiveSync, exigem certificados para serem configurados no seu servidor Exchange 2013. As etapas a seguir mostram como configurar um certificado SSL de uma autoridade de certificação de terceiros (CA):

1.  Abra o EAC navegando até a URL do seu servidor de Acesso para Cliente. Por exemplo, https://Ex2013CAS/ECP.

2.  Insira seu nome de usuário e senha em **Domínio\\nome de usuário** e **Senha** e clique em **Entrar**.

3.  Vá até **Servidores** \> **Certificados**. Na página **Certificados**, certifique-se de que seu servidor de Acesso para Cliente esteja selecionado no campo **Selecionar servidor** e clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  No assistente de **Novo Certificado do Exchange**, selecione **Criar uma solicitação de certificado de uma autoridade de certificação** e clique em **Avançar**.

5.  Especifique um nome para este certificado e clique em **Avançar**.

6.  Se quiser solicitar um certificado de curinga, selecione **Solicitar um certificado de curinga** e depois especifique o domínio raiz de todos os subdomínios no campo **Domínio raiz**. Se não quiser solicitar um certificado de curinga e, em vez disso, preferir especificar cada domínio a ser adicionado ao certificado, deixe essa página em branco. Clique em **Avançar**.

7.  Clique em **Procurar** e especifique um servidor Exchange no qual armazenar o certificado. O servidor selecionado deve ser o servidor de Acesso para Cliente voltado para a Internet. Clique em **Avançar**.

8.  Para cada serviço na lista exibida, verifique se os nomes de servidores internos ou externos que os usuários utilizam para se conectar ao servidor Exchange estão corretos. Por exemplo:
    
      - Se você tiver configurado suas URLs internas e externas de forma que elas sejam idênticas, o **Outlook Web App (quando acessado na Internet)** e o **Outlook Web App (quando acessado na Internet)** devem mostrar owa.contoso.com. O **OAB (quando acessado na Internet)** e o **OAB (quando acessado na Intranet**) devem mostrar mail.contoso.com.
    
      - Se você tiver configurado suas URLs internas como internal.contoso.com, o **Outlook Web App (quando acessado na Internet)** deverá mostrar owa.contoso.com, enquanto o **Outlook Web App (quando acessado na Internet)** deve mostrar internal.contoso.com.
    
    Estes domínios serão usados para criar a solicitação de certificado SSL. Clique em **Avançar**.

9.  Adicione domínios adicionais que você deseja incluir no certificado SSL.

10. Selecione o domínio que você deseja que seja o nome comum do certificado e clique em **Definir como nome comum**. Por exemplo, contoso.com. Clique em **Avançar**.

11. Forneça informações sobre a sua organização. Essas informações serão incluídas no certificado SSL. Clique em **Avançar**.

12. Especifique a localização de rede na qual você deseja que essa solicitação de certificado seja salva. Clique em **Concluir**.

Depois de salvar a solicitação de certificado, envie-a à autoridade de certificação. Esta pode ser uma autoridade de certificação interna ou uma autoridade de certificação de terceiros, dependendo da sua organização. Clientes que se conectam ao servidor de Acesso para Cliente devem confiar na autoridade de certificação que você usar. Depois de receber o certificado da autoridade de certificação, conclua as seguintes etapas:

1.  Na página **Servidor** \> **Certificados** do EAC, selecione a solicitação de certificado criada nas etapas anteriores.

2.  No painel de detalhes da solicitação de certificado, clique em **Concluir** em **Status**.

3.  Na página Concluir Solicitação Pendente, especifique o caminho para o arquivo de certificado SSL e clique em **OK**.

4.  Selecione o novo certificado que você acabou de adicionar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

5.  Na página de certificado, clique em **Serviços**.

6.  Selecione os serviços que você deseja atribuir a esse certificado. Você deve selecionar pelo menos **SMTP** e **IIS**. Clique em **Salvar**.

7.  Se você receber o aviso **Sobrescrever o certificado SMTP padrão existente?**, clique em **Sim**.

## Como saber se essa etapa funcionou?

Para verificar se você adicionou um novo certificado com êxito, faça o seguinte:

1.  No EAC, vá até **Servidores** \> **Certificados**.

2.  Selecionar o novo certificado e, no painel de detalhes do certificado, verifique se o seguinte é verdadeiro:
    
      - **Status** mostra **Válido**
    
      - **Atribuído aos serviços** mostra, no mínimo, **IIS** e **SMTP**.

## Como saber se essa tarefa funcionou?

Para verificar se você configurou o fluxo de emails e Acesso para Clientes externos, faça o seguinte:

1.  No Outlook, em um dispositivo Exchange ou ActiveSync, ou em ambos, crie um novo perfil. Verifique se o Outlook ou o dispositivo móvel cria com êxito o novo perfil.

2.  No Outlook ou no dispositivo móvel, envia uma nova mensagem para um destinatário externo. Verifique se que o destinatário externo recebe a mensagem.

3.  Na caixa de correio de destinatário externo, responda à mensagem que você acabou de enviar da caixa de correio do Exchange. Verifique se que a caixa de correio do Exchange recebe a mensagem.

4.  Vá até https://owa.contoso.com/owa e verifique se não há nenhum aviso de certificado.

