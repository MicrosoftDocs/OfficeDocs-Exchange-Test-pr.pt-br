---
title: 'IRM em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: IRM em implantações híbridas do Exchange
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 50487117
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IRM em implantações híbridas do Exchange

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

**Resumo:** como o IRM funciona em um ambiente híbrido do Exchange e como configurar o IRM para funcionar entre o Exchange Online e seus servidores locais do Exchange.

O Gerenciamento de Direitos de Informação (IRM) ajuda a proteger contra vazamento de informações confidenciais, fornecendo proteção persistente online e offline de mensagens de email e anexos. A organização do Exchange local e o Exchange Online, no Office 365 para empresas, dão suporte ao IRM. Entretanto, existem diferenças entre as duas implementações e é necessário configurar o IRM na organização do Exchange Online antes de os usuários da organização poderem usá-lo.

O IRM usa o Active Directory Rights Management Services (AD RMS), que é um componente do Windows Server 2008 e posteriores. O AD RMS permite que os usuários criem um conteúdo protegido por direitos, como mensagens de email e anexos, além de controlar como o conteúdo é usado e para quem ele é distribuído. Os usuários podem especificar os modelos que determinam como o conteúdo pode ser usado. Por exemplo, um usuário pode especificar que uma mensagem de email não possa ser encaminhada para outros destinatários ou que as informações na mensagem não possam ser copiadas.

Saiba mais sobre o IRM no Exchange 2010 em: [Noções Básicas Sobre o Gerenciamento de Direitos de Informação](https://technet.microsoft.com/pt-br/library/dd638140\(v=exchg.141\).aspx).

Saiba mais sobre o IRM no Exchange 2013 e Exchange 2016 em [Gerenciamento de Direitos de Informação](https://technet.microsoft.com/pt-br/library/dd638140\(v=exchg.150\)).

Saiba mais sobre o AD RMS em [Visão geral do Active Directory Rights Management Services](http://go.microsoft.com/fwlink/p/?linkid=215243).

## Diferenças entre o IRM no Exchange no Local e no Exchange Online

A funcionalidade do IRM disponível em sua organização local do Exchange pode ser diferente das funcionalidades disponíveis na organização do Exchange Online. A tabela a seguir fornece um resumo dos recursos e funcionalidades disponíveis em cada organização. (Saiba mais sobre esses recursos em: [Gerenciamento de Direitos de Informação](https://technet.microsoft.com/pt-br/library/dd638140\(v=exchg.150\)))

### Recursos disponíveis de IRM

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Disponível no Exchange 2007 e anteriores</th>
<th>Disponível no Exchange 2010</th>
<th>Disponível no Exchange Online e no Exchange 2013 e posteriores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Proteção manual de mensagens no Outlook</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Proteção manual de mensagens no Outlook Web App</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Exibir mensagens protegidas por IRM no Outlook</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Exibir mensagens protegidas por IRM no Outlook Web App</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Agente de pré-licenciamento de IRM</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Modelos de política RMS</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Descriptografia de transporte</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Criptografia do relatório de diário</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Descriptografia de pesquisa e descoberta do Exchange</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Regras de proteção automática do Outlook</p></td>
<td><p>Não</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Regras de proteção de transporte automática</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


## IRM em implantações híbridas

O Exchange usa servidores AD RMS na floresta do Active Directory na qual o servidor do Exchange está instalado. Para os servidores locais do Exchange, o servidor local do AD RMS é usado. Para a organização do Exchange Online, os servidores do AD RMS mantidos dentro dos data centers do Office 365 são usados. A configuração do AD RMS que cada organização do Exchange usa é independente de qualquer outra implantação do AD RMS.

A configuração do AD RMS e, portanto, a configuração do IRM, não é duplicada automaticamente entre a organização local do Exchange e a organização do Exchange Online. Todos os modelos do AD RMS que você definiu não são copiados automaticamente para a organização do Exchange Online. Se desejar que os mesmos modelos AD RMS estejam disponíveis na organização do Exchange Online, exporte os modelos da sua organização local manualmente e aplique-os na organização do Office 365. Confira Configurar o IRM nas implantações híbridas mais adiante neste tópico.

## Experiência do usuário

A configuração de IRM que é aplicada a um usuário depende do cliente usado pelo usuário e da localização da caixa de correio do usuário. A tabela a seguir mostra o servidor AD RMS que usuário deve utilizar.

### Servidor AD RMS Ativo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>Caixa de correio local</th>
<th>Caixa de correio do Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Clientes da área de trabalho do Outlook</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS local</p></td>
</tr>
<tr class="even">
<td><p>Outlook na Web</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS do Exchange Online</p></td>
</tr>
<tr class="odd">
<td><p>Dispositivo ActiveSync</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS do Exchange Online</p></td>
</tr>
</tbody>
</table>


Dependendo da configuração do AD RMS que você definir em suas organizações local e do Exchange Online, é possível que um usuário que usa o Outlook 2007 e o Outlook na Web veja modelos de AD RMS diferentes. Por esse motivo, é altamente recomendável que você aplique os mesmos modelos para as organizações do Exchange Online e local.

Não deve haver nenhuma diferença na experiência do IRM para os usuários clientes do Outlook, independentemente se suas caixas de correio estão localizadas na organização do Exchange Online ou local.

Um usuário do Outlook na Web com caixa de correio localizada em um servidor local do Exchange só pode abrir mensagens protegidas por direitos depois de instalar o complemento Rights Management para Internet Explorer. Ele não poderá responder ou criar novas mensagens protegidas por direitos.

Um usuário do Outlook na Web cuja caixa de correio está localizada no Exchange Online pode abrir mensagens protegidas por direitos sem nenhum software adicional, além de responder e criar novas mensagens protegidas por direitos.

## Funcionalidade do servidor

Os servidores do Exchange no local usam o agente de pré-licenciamento AD RMS para descriptografar as mensagens protegidas por direitos para que os usuários não precisem fornecer as credenciais quando abrirem essas mensagens. O servidor do Exchange local contata o servidor do AD RMS local para verificar direitos e políticas de uso e solicitar a autorização para descriptografar a mensagem.

A organização do Exchange Online oferece vários recursos adicionais relacionados a IRM que usam o AD RMS do Exchange Online. Esses recursos, como descriptografia de relatório de diário, disponibilizam o conteúdo de mensagens protegidas por direitos para os serviços do Exchange para processamento adicional. Por exemplo, o conteúdo descriptografado de uma mensagem registrada no diário pode ser salvo junto com a mensagem original protegida por direitos para permitir uma descoberta mais fácil. Além disso, os modelos IRM podem ser aplicados às mensagens automaticamente usando regras de transporte ou regras de proteção do Outlook para garantir que mensagens estejam de acordo com as políticas da organização relacionadas a proteção das informações.

## Configurar IRM em implantações híbridas

O IRM no Exchange depende do AD RMS que estiver sendo implantado na floresta do Active Directory na qual o servidor do Exchange reside. A configuração do AD RMS não é sincronizada automaticamente entre as organizações do Exchange Online e local. Você deve exportar manualmente a configuração do AD RMS, conhecida como um domínio de publicação confiável (TPD), do seu servidor do AD RMS local e importar essa configuração para a organização do Exchange Online. O TPD contém a configuração do AD RMS, incluindo modelos, que a organização do Exchange Online precisa para usar o IRM.

Saiba mais em [Considerações de domínio de publicação confiável AD RMS](http://go.microsoft.com/fwlink/p/?linkid=215244).

Além de aplicar suas configuração do AD RMS local para a organização do Exchange Online, você deve garantir que seus servidores AD RMS podem ser contatados pelos clientes do Outlook e do ActiveSync de fora da sua rede local. Você deve fazer isso se quiser que esses clientes acessem mensagens protegidas por direitos fora da sua rede local.

Depois de configurar a sua rede local e exportar os dados de TPD, você precisa configurar a organização do Exchange Online importando os dados de TPD e habilitando o IRM.


> [!TIP]
> Sempre que você modificar as configurações do AD RMS local, deve aplicar manualmente a nova configuração na organização do Exchange Online. Para fazer isso, exporte os dados TPD do servidor AD RMS local e importe-os para a organização do Exchange Online.



## Como configurar o IRM em implantações híbridas do Exchange

Se você usa o IRM em sua organização do Exchange local e deseja que os usuários do Exchange Online também usem o IRM, é necessário fazer o seguinte:

1.  Configurar o Gerenciamento de Direitos de Informação (AD RMS) do servidor do Active Directory local.

2.  Habilitar o IRM da organização do Exchange Online.

3.  Distribuir os modelos do AD RMS importados para os usuários da organização do Exchange Online.

## Como configurar os servidores AD RMS local?

Para configurar o IRM em uma implantação híbrida, você precisa usar o Windows PowerShell para acessar o servidor AD RMS local. Saiba mais em: [Usando o Windows PowerShell para administrar o AD RMS](http://go.microsoft.com/fwlink/p/?linkid=214938)

Siga este procedimento para exportar dados de domínio de publicação confiável (TPD) do servidor do AD RMS local e, em seguida, configure o acesso ao servidor AD RMS para clientes externos.

1.  Exporte dados TPD da organização local. Saiba mais em: [Exportando um domínio de publicação confiável](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  Configure o acesso aos servidores do AD RMS de clientes externos. Saiba mais em: [Adicionando uma URL de Cluster da Extranet](http://go.microsoft.com/fwlink/p/?linkid=214945)

## Como habilitar o IRM na organização do Exchange Online?

Depois de exportar os dados TPD do servidor do AD RMS local, você precisa importar dados para a organização do Exchange Online e, em seguida, habilitar o IRM.

1.  Na organização do Exchange Online, importe os dados TPD.
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  Habilitar o IRM na organização do Exchange Online.
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## Como distribuir o modelos AD RMS na organização do Exchange Online?

Depois de habilitar o IRM na organização do Exchange Online, distribua os modelos do AD RMS importados. Os seguintes recursos e usuários do Exchange Online usam os modelos de AD RMS:

  - Usuários do Outlook na Web

  - Usuários do Exchange ActiveSync

  - Regras de transporte

  - Criptografia do relatório de diário

  - Regras de proteção do Outlook

<!-- end list -->

1.  Na organização do Exchange Online, recupere uma lista de modelos do AD RMS.
    
        Get-RMSTemplate -Type All

2.  Distribua os modelos do AD RMS aos usuários e recursos na organização do Exchange Online.
    
        Set-RMSTemplate <template name> -Type Distributed
    

    > [!TIP]
    > Você não pode modificar o modelo "Não encaminhar" do AD&nbsp;RMS.



3.  Repita a etapa 2 para cada modelo do AD RMS que você deseja distribuir.

## Como saber se funcionou?

Os usuários do Outlook na Web podem aplicar modelos AD RMS às novas mensagens. Os usuários do Outlook na Web e do Exchange ActiveSync devem conseguir ler as mensagens que possuem modelos AD RMS aplicados a elas. Além disso, todos os modelos do AD RMS que foram importados da organização local devem estar listados quando você executa o cmdlet **Get-RMSTemplate**.

Execute o comando a seguir na organização do Exchange Online.

    Get-RMSTemplate 

Saiba mais em: [Gerenciamento de direitos de informação no Outlook Web App](https://technet.microsoft.com/pt-br/library/dd876891\(v=exchg.150\))

