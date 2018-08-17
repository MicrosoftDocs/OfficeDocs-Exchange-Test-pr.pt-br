---
title: 'Gerenciamento de Direitos de Informação: Exchange 2013 Help'
TOCTitle: Gerenciamento de Direitos de Informação
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 50485790
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciamento de Direitos de Informação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Todos os dias, funcionários que lidam com informações usam emails para trocar informações importantes, como relatórios e dados financeiros, contratos, informações confidenciais de produtos, relatórios e projeções de vendas, análises da concorrência, informações de pesquisas e patentes e informações sobre clientes e empregados. Como as pessoas podem acessar seus emails de praticamente qualquer lugar, as caixas de correio se transformaram em repositórios contendo grandes quantidades de informações potencialmente confidenciais. Como resultado, o vazamento de informações pode ser uma séria ameaça para as organizações. Para evitar o vazamento de informações, o Microsoft Exchange Server 2013 inclui recursos de Gerenciamento de Direitos de Informação (IRM) que oferecem proteção persistente online e offline de mensagens e anexos de email.

**Sumário**

What is information leakage?

Traditional solutions to information leakage

IRM in Exchange 2010

Applying IRM protection to messages

Scenarios for IRM protection

Decrypting IRM-protected messages to enforce messaging policies

Prelicensing

IRM agents

IRM requirements

Configuring and testing IRM

Extend Rights Management with the Rights Management connector

## O que é o vazamento de informações?

O vazamento de informações potencialmente confidenciais pode ser oneroso para uma organização e ter um amplo impacto na organização e em seus negócios, funcionários, clientes e parceiros. Regulamentos locais e industriais controlam, cada vez mais, como certos tipos de informações são armazenadas, transmitidas e protegidas. Para não violar as regulamentações aplicáveis, as organizações devem se proteger contra vazamentos intencionais, inadvertidos e acidentais de informações.

Estas são algumas conseqüências do vazamento de informações:

  - **Danos financeiros**   Dependendo do tamanho, setor e regulamentações locais, o vazamento de informações pode resultar em impactos financeiros, devido a perdas de negócios ou multas e punições impostas por cortes e autoridades de regulamentação. As companhias de capital aberto também se arriscam a perder valor no mercado, devido à cobertura negativa na mídia.

  - **Danos à imagem e credibilidade**   Um vazamento de informações pode prejudicar a imagem e a credibilidade que uma organização tem diante dos seus clientes. Mais do que isso, dependendo da natureza das informações, os emails vazados podem ser uma fonte de embaraços para o remetente e a organização.

  - **Perda de vantagem competitiva**   Uma das ameaças mais sérias do vazamento de informações é a perda de vantagens competitivas nos negócios. A divulgação de planos estratégicos ou de informações de fusão e aquisição pode potencialmente levar a perda de lucros ou capitalização no mercado. Outras ameaças incluem a perda de informações de pesquisa, dados analíticos e outra propriedade intelectual.

Voltar ao início

## Soluções tradicionais para vazamento de informações

Apesar de as soluções tradicionais para vazamento de informações poderem proteger o acesso inicial a dados, elas frequentemente não oferecem proteção constante. A tabela a seguir lista algumas das soluções tradicionais e suas limitações.

### Soluções tradicionais

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Solução</th>
<th>Descrição</th>
<th>Limitações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Protocolo TLS</p></td>
<td><p>O TLS é um protocolo-padrão de Internet usado para proteger as comunicações em uma rede, usando criptografia. Em um ambiente de mensagens, o TLS é usado para proteger as comunicações entre servidores e entre clientes e servidores.</p>
<p>Por padrão, Exchange 2010 usa o TLS para todas as transferências de mensagem interna. TLS oportunista também está habilitado por padrão para as sessões de hosts externos. Exchange primeiro tenta usar a criptografia TLS para a sessão, mas se não é possível estabelecer uma conexão TLS com o servidor de destino, Exchange usa SMTP. Você também pode configurar a segurança de domínio para impor o TLS mútuo com organizações externas.</p></td>
<td><p>O TLS protege apenas a sessão SMTP entre dois hosts SMTP. Em outras palavras, o TLS protege informações sendo transportadas e não fornece proteção no nível de mensagem ou para informações &quot;em repouso&quot;. A menos que as mensagens sejam criptografadas com outro método, os emails nas caixas de correio de destinatários e remetentes permanecem desprotegidos. Para emails enviados fora da organização, você pode exigir o TLS somente para o primeiro salto. Depois que um host SMTP remoto fora da sua organização receber a mensagem, ele pode retransmiti-la para outro host SMTP em uma sessão sem criptografia. Como o TLS é uma tecnologia de camada de transporte, ela não oferece controle sobre o que o destinatário faz com a mensagem.</p></td>
</tr>
<tr class="even">
<td><p>Criptografia de email</p></td>
<td><p>Os usuários podem usar tecnologias como S/MIME para criptografar mensagens.</p></td>
<td><p>Eles decidem se uma mensagem é criptografada. Há mais gastos com uma implantação de infraestrutura de chave pública (PKI), com a consequente sobrecarga de gerenciamento de certificados para usuários e proteção de chaves privadas. Quando a mensagem é descriptografada, não há controle sobre o que o destinatário pode fazer com as informações. Informações descriptografadas podem ser copiadas, impressas ou encaminhadas. Por padrão, anexos salvos não serão protegidos.</p>
<p>As mensagens criptografadas com tecnologias como S/MIME não podem ser acessadas pela sua organização. E, como a organização não pode inspecionar o conteúdo das mensagens, também não pode impor diretivas de envios de mensagens, procurar vírus ou conteúdo prejudicial ou qualquer outra ação que exija acessar o conteúdo.</p></td>
</tr>
</tbody>
</table>


Finalmente, as soluções tradicionais geralmente não têm as ferramentas de imposição que aplicam as políticas de mensagens uniformes para evitar o vazamento de informações. Por exemplo, um usuário envia uma mensagem contendo informações importantes e a marca como **Confidencial da empresa** e **Não encaminhar**. Após a mensagem ser entregue ao destinatário, o remetente ou a organização não tem mais controle sobre as informações. O destinatário pode encaminhar a mensagem, propositalmente ou não (usando recursos como regras de encaminhamento automático) para contas de email externas, expondo sua organização a grandes riscos de vazamento de informações.

Voltar ao início

## IRM no Exchange 2013

No Exchange 2013, você pode usar os recursos de IRM para aplicar proteção persistente para as mensagens e anexos. O IRM usa o Active Directory Rights Management Services (AD RMS), uma tecnologia de proteção de informações do Windows Server 2008 e versões posteriores. Com os recursos de IRM no Exchange 2013, sua organização e seus usuários podem controlar os direitos que os destinatários têm para email. O IRM também ajuda a proteger ou restringir as ações do destinatário, como encaminhar uma mensagem para outros destinatários, imprimir uma mensagem ou anexo ou extrair conteúdo da mensagem ou do anexo via copiar-e-colar. A proteção do IRM pode ser aplicada a usuários do Microsoft Outlook ou Microsoft Office Outlook Web App ou pode ser baseada nas políticas de mensagens da sua organização e aplicada usando regras de proteção de transporte ou regras de proteção do Outlook. Ao contrário de outras soluções de criptografia de emails, o IRM também permite que a sua organização descriptografe conteúdo protegido, para impor a conformidade com as diretivas.

O AD RMS usa certificados e licenças baseados em XrML (eXtensible Rights Markup Language) para certificar computadores e usuários e para proteger conteúdo. Quando conteúdo, como um documento ou uma mensagem, é protegido com AD RMS, é anexada uma licença XrML contendo os direitos que os usuários autorizados têm para o conteúdo anexado. Para acessar o conteúdo protegido por IRM, os aplicativos habilitados para AD RMS devem conseguir uma licença de uso para o usuário autorizado do cluster AD RMS.


> [!NOTE]
> No Exchange 2013, o agente de pré-licenciamento anexa uma licença de uso a mensagens protegidas usando o cluster AD RMS na sua organização. Para mais informações, consulte Prelicensing, posteriormente neste tópico.



Os aplicativos usados para criar conteúdo devem estar habilitados para RMS, para aplicar proteção persistente a conteúdos usando AD RMS. Aplicativos do Microsoft Office, como Word, Excel, PowerPoint e Outlook, são habilitados para RMS e podem ser usados para criar e consumir conteúdo protegido.

O IRM ajuda a fazer o seguinte:

  - Evitar que um destinatário autorizado de conteúdo protegido por IRM encaminhe, modifique, imprima, envie por fax, salve ou copie-e-cole o conteúdo.

  - Proteger os formatos de arquivos anexos suportados com o mesmo nível de proteção da mensagem.

  - Suportar a expiração das mensagens e anexos protegidos por IRM, para que eles não possam mais ser exibidos após o período especificado.

  - Evitar que conteúdo protegido por IRM seja copiado usando a Ferramenta de Captura no Microsoft Windows.

No entanto, o IRM não pode impedir que informações sejam copiadas usando estes métodos:

  - Programas de captura de tela de terceiros

  - Uso de dispositivos de imagem, como câmeras, para fotografar o conteúdo protegido por IRM exibido na tela

  - Usuários lembrando ou transcrevendo manualmente as informações

Para saber mais sobre o AD RMS, consulte [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823).

## Modelos de políticas de direitos do AD RMS

O AD RMS usa modelos de diretiva de direitos baseados em XrML para permitir que aplicativos habilitados para IRM apliquem diretivas de proteção consistentes. No Windows Server 2008 e posteriores, o servidor do AD RMS expõe um servidor da Web que pode ser usado para enumerar e adquirir modelos. O Exchange 2013 vem com o modelo Não encaminhar. Quando o modelo Não Encaminhar é aplicado a uma mensagem, somente os destinatários da mensagem podem descriptografá-la. Os destinatários não podem encaminhar a mensagem, copiar conteúdo dela ou imprimi-la. Você pode criar mais modelos RMS no servidor do AD RMS, na sua organização, para cumprir os requisitos de proteção do IRM.

A proteção de IRM é aplicada, aplicando-se um modelo de diretiva de direitos do AD RMS. Usando modelos de diretiva, você pode controlar as permissões que os destinatários têm sobre uma mensagem. Ações como responder, responder a todos, encaminhar, extrair informações de uma mensagem, salvar uma mensagem ou imprimir uma mensagem podem ser controladas, aplicando-se o modelo de política de direitos apropriada à mensagem.

Para obter mais informações sobre modelos de diretiva de direitos, consulte [Considerações de modelo de política do AD RMS](https://go.microsoft.com/fwlink/p/?linkid=179455).

Para obter mais informações sobre a criação de modelos de diretiva de direitos do AD RMS, consulte o [Guia de passo a passo do AD RMS direitos política modelos de implantação](https://go.microsoft.com/fwlink/p/?linkid=136593).

Voltar ao início

## Aplicar proteção IRM a mensagens

Em Exchange 2010, proteção IRM pode ser aplicada às mensagens usando os seguintes métodos:

  - **Manualmente por usuários do Outlook**   Os usuários Outlook podem proteger o IRM mensagens com os modelos de diretiva de direitos do AD RMS disponíveis para eles. Esse processo usa a funcionalidade do IRM em Outlook e Exchange. No entanto, você pode usar Exchange para acessar mensagens, e você pode tomar ações (por exemplo, a aplicação de regras de transporte) para impor a sua organização mensagens da política. Para obter mais informações sobre como usar o IRM no Outlook, consulte [Introdução ao IRM para mensagens de email](https://go.microsoft.com/fwlink/p/?linkid=166897).

  - **Manualmente, por usuários do Outlook Web App**   Quando você habilita o IRM no Outlook Web App, os usuários podem proteger, com IRM, mensagens que eles enviam e ver mensagens protegidas por IRM que eles recebem. Na Atualização Cumulativa 1 (CU1) do Exchange 2013, os usuários do Outlook Web App também podem exibir os anexos protegidos por IRM usando a Exibição de Documento Webready. Para obter mais informações sobre IRM no Outlook Web App, consulte [Gerenciamento de direitos de informação no Outlook Web App](information-rights-management-in-outlook-web-app-exchange-2013-help.md).

  - **Manualmente pelo Windows Mobile e usuários de dispositivos do Exchange ActiveSync**   Em release to manufacturing (RTM) versão do Exchange 2010, os usuários de dispositivos móveis do Windows podem exibir e criar mensagens protegidas por IRM. Isso requer que os usuários se conectem a seus dispositivos móveis de suportados Windows a um computador e ativá-los para IRM. Na Exchange 2010 SP1, você pode habilitar o IRM no Microsoft Exchange ActiveSync para permitir que os usuários de dispositivos Exchange ActiveSync (incluindo os dispositivos móveis Windows ) para exibir, responder para encaminhar e criar mensagens protegidas por IRM. Para obter mais informações sobre o IRM no Exchange ActiveSync, consulte [Gerenciamento de direitos de informação no Exchange ActiveSync](information-rights-management-in-exchange-activesync-exchange-2013-help.md).

  - **Automaticamente no Outlook 2010 e posteriores**   Você pode criar regras de proteção do Outlook para proteger automaticamente com IRM as mensagens no Outlook 2010 e posteriores. As regras de proteção do Outlook são implantadas automaticamente para clientes do Outlook 2010, e a proteção de IRM é aplicada pelo Outlook 2010 quando o usuário compõe uma mensagem. Para mais informações sobre regras de proteção do Outlook, consulte [Regras de proteção do Outlook](outlook-protection-rules-exchange-2013-help.md).

  - **Automaticamente nos servidores de Caixa de Correio**   Você pode criar regras de proteção de transporte para proteger com IRM automaticamente as mensagens nos servidores de Caixa de Correio do Exchange 2013. Para mais informações sobre regras de proteção de transporte, consulte [Regras de proteção de transporte](transport-protection-rules-exchange-2013-help.md).
    

    > [!NOTE]
    > A proteção de IRM não é aplicada novamente a mensagens que já estão protegidas por IRM. Por exemplo, se um usuário proteger com IRM uma mensagem no Outlook ou Outlook Web App, a proteção com IRM não será aplicada à mensagem, com o uso de uma regra de proteção de transporte.



Voltar ao início

## Cenários para proteção de IRM

Os cenários para proteção de IRM são descritos na tabela abaixo.

### Cenários para proteção de IRM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Enviando mensagens protegidas por IRM</th>
<th>Suportado</th>
<th>Requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Na mesma implantação local do Exchange 2013</p></td>
<td><p>Sim</p></td>
<td><p>Para obter detalhes, consulte IRM Requirements mais adiante neste tópico.</p></td>
</tr>
<tr class="even">
<td><p>Entre florestas diferentes em uma implantação local</p></td>
<td><p>Sim</p></td>
<td><p>Para requisitos, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=199009">Configurando o AD RMS para se integrar ao Exchange Server 2010 em várias florestas</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Entre uma implantação no local do Exchange 2013 e uma organização do Exchange baseada em nuvem</p></td>
<td><p>Sim</p></td>
<td><ul>
<li><p>Use um servidor AD RMS no local.</p></li>
<li><p>Exporte o domínio de publicação confiável do seu servidor AD RMS no local.</p></li>
<li><p>Importe o domínio de publicação confiável na sua organização baseada em nuvem.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Para destinatários externos</p></td>
<td><p>Não</p></td>
<td><p>Exchange 2010 não inclui uma solução para enviar mensagens protegidas por IRM para destinatários externos em uma organização não federados. AD RMS oferece soluções usando diretivas de confiança. Você pode configurar uma política de confiança entre seu cluster AD RMS e a conta da Microsoft (anteriormente conhecido como Windows Live ID). Para mensagens enviadas entre duas organizações, você pode criar uma relação de confiança federada entre as duas florestas Active Directory usando Active Directory serviços de Federação (AD FS). Para saber mais, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=182909">Understanding AD RMS confiar Policies</a>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Descriptografando mensagens protegidas com IRM para impor políticas de mensagens

Para impor diretivas de mensagens e para conformidade regulamentar, você deve poder acessar o conteúdo da mensagem criptografada. Para atender a requisitos de descoberta eletrônica devido a litígios, auditorias regulamentares ou investigações internas, você deverá ter a possibilidade de pesquisar mensagens criptografadas. Para ajudar com essas tarefas, o Exchange 2013 inclui os seguintes recursos do IRM:

  - **Descriptografia de transporte**   Para aplicar diretivas de mensagens, os agentes de transporte, como o agente de Regras de Transporte, devem ter acesso ao conteúdo da mensagem. As descriptografia de transporte permite que os agentes de transporte instalados nos servidores do Exchange 2013 acessem o conteúdo da mensagem. Para mais informações, consulte [Descriptografia de transporte](transport-decryption-exchange-2013-help.md).

  - **Descriptografia do relatório de registro em diário**   Para cumprir os requisitos de conformidade ou negócios, as organizações podem usar o Registro em diário para preservar o conteúdo da mensagem. O agente de Registro no diário cria um relatório de registro no diário para mensagens sujeitas a esse registro e inclui metadados sobre a mensagem no relatório. A mensagem original é anexada ao relatório de registro no diário. Se a mensagem em um relatório de registro no diário for protegida com IRM, a descriptografia de relatório de registro no diário anexa uma cópia em texto simples da mensagem ao relatório de registro no diário. Para mais informações, consulte [Criptografia do relatório de diário](journal-report-decryption-exchange-2013-help.md).

  - **Descriptografia do IRM para a Pesquisa do Exchange**   Com a descriptografia do IRM para a Pesquisa do Exchange, a Pesquisa do Exchange pode indexar o conteúdo de mensagens protegidas com IRM. Quando um gerenciador de descobertas executa uma pesquisa de Descoberta Eletrônica In-loco, as mensagens protegidas com IRM que tiverem sido indexadas são retornadas nos resultados da pesquisa. Para mais informações, consulte [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md).
    

    > [!NOTE]
    > Na Exchange 2010 SP1 e posterior, os membros do grupo de função de gerenciamento de descoberta podem acessar mensagens protegidas por IRM retornado por uma pesquisa de descoberta e que residem em uma caixa de correio de descoberta. Para habilitar essa funcionalidade, use o parâmetro <EM>EDiscoverySuperUserEnabled</EM> com <A href="https://technet.microsoft.com/pt-br/library/dd979792(v=exchg.150)">Set-IRMConfiguration</A> cmdlet. Para obter mais informações, consulte <A href="configure-irm-for-exchange-search-and-in-place-ediscovery-exchange-2013-help.md">Configurar o IRM para descoberta eletrônica In-loco e de pesquisa do Exchange</A>.



Para habilitar esses recursos de descriptografia, os servidores do Exchange devem ter acesso à mensagem. Isso é conseguido adicionando-se a caixa de correio de Federação, uma caixa de correio do sistema criada pela Configuração do Exchange, para o grupo de superusuários no servidor AD RMS. Para detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

Voltar ao início

## Pré-licenciamento

Exibir mensagens e anexos protegidos com IRM, o Exchange 2013 automaticamente anexa uma pré-licença às mensagens protegidas. Isso evita que o cliente tenha que fazer repetidas viagens ao servidor do AD RMS para recuperar uma licença de uso e habilita a visualização offline de mensagens e anexos protegidos por IRM. O pré-licenciamento também permite que as mensagens protegidas por IRM sejam exibidas no Outlook Web App. Quando você ativa recursos do IRM, o pré-licenciamento é ativado por padrão.

Voltar ao início

## Agentes IRM

No Exchange 2013, a funcionalidade do IRM é habilitada usando-se agentes de transporte no serviço de Transporte, nos servidores de Caixa de Correio. Os agentes do IRM são instalados pela Instalação do Exchange em um servidor de Caixa de Correio. Não é possível controlar agentes IRM usando as tarefas de gerenciamento de agentes de transporte.


> [!NOTE]
> No Exchange 2013, os agentes de IRM são agentes embutidos. Agentes integrados não estão incluídos na lista de agentes retornados pelo cmdlet <STRONG>Get-TransportAgent</STRONG>. Para mais informações, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



A tabela a seguir lista os agentes IRM implementados no serviço de Transporte em servidores de Caixa de Correio.

### Agentes IRM no serviço de Transporte, em servidores de Caixa de Correio

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Agente</th>
<th>Evento</th>
<th>Função</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente de descriptografia do RMS</p></td>
<td><p>OnEndOfData (SMTP) e OnSubmittedMessage</p></td>
<td><p>Descriptografa mensagens para permitir o acesso a agentes de transporte.</p></td>
</tr>
<tr class="even">
<td><p>Agente de Regras de Transporte</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Sinaliza mensagens que correspondam às condições da regra em uma regra de proteção de transporte a ser protegida com IRM pelo agente de criptografia do RMS.</p></td>
</tr>
<tr class="odd">
<td><p>Agente de criptografia do RMS</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Aplica a proteção do IRM às mensagens sinalizadas pelo agente de Regras de Transporte e recriptografa as mensagens criptografadas para transporte.</p></td>
</tr>
<tr class="even">
<td><p>Agente de pré-licenciamento</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Anexa uma pré-licença a mensagens protegidas por IRM.</p></td>
</tr>
<tr class="odd">
<td><p>Agente de descriptografia do relatório de registro no diário</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>Descriptografa mensagens protegidas por IRM anexadas a relatórios de registros no diário e inclui versões em texto simples com as mensagens criptografadas originais.</p></td>
</tr>
</tbody>
</table>


Para mais informações sobre agentes de transporte, consulte [Agentes de transporte](transport-agents-exchange-2013-help.md).

Voltar ao início

## Requisitos de IRM

Para implementar o IRM na sua organização do Exchange 2013, sua implantação deve atender aos requisitos descritos na seguinte tabela.

### Requisitos de IRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cluster do AD RMS</p></td>
<td><ul>
<li><p><strong>Sistema operacional</strong>   Windows Server 2012, Windows Server 2008 R2 ou Windows Server 2008 SP2 com o hotfix <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973247">Um hotfix está disponível para a função do Active Directory Rights Management Services no Windows Server 2008: 26 de agosto de 2009</a> é necessário.</p></li>
<li><p><strong>Ponto de conexão de serviço</strong> Exchange 2010 e aplicativos com reconhecimento de AD RMS usam o ponto de conexão de serviço registrado no Active Directory para descobrir um cluster AD RMS e URLs. AD RMS permite que você registre o ponto de conexão de serviço de dentro da configuração do AD RMS. Se a conta usada para configurar o AD RMS não for um membro do grupo de segurança Administradores de empresa, o registro de ponto de conexão de serviço pode ser realizado quando a instalação for concluída. Há somente um serviço ponto de conexão para o AD RMS em uma floresta Active Directory.   </p></li>
<li><p><strong>Permissões</strong>   As permissões de Leitura e Execução para o pipeline de certificação de servidor AD RMS (arquivo <code>ServerCertification.asmx</code> nos servidores AD RMS) devem se atribuídas ao seguinte:</p>
<ul>
<li><p>Grupo de servidores Exchange ou servidores Exchange individuais</p></li>
<li><p>Grupo de serviços do AD RMS em servidores AD RMS</p></li>
</ul>
<p>Por padrão, o arquivo ServerCertification asmx está localizada na pasta <code>\inetpub\wwwroot\_wmcs\certification\</code> servidores AD RMS. Para obter detalhes, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=186951">Definir permissões no Pipeline de certificação do servidor AD RMS</a>.</p></li>
<li><p><strong>Superusuários do AD RMS</strong>   Para habilitar a descriptografia do transporte, a descriptografia do relatório de registro no jornal, o IRM no Outlook Web App e o IRM para Pesquisa do Exchange, você deve adicionar a caixa de correio de Federação, uma caixa de correio do sistema criada pela Configuração do Exchange 2013, ao grupo de superusuários no cluster do AD RMS. Para detalhes, consulte <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Exchange 2010 ou posterior é necessário.</p></li>
<li><p>O hotfix <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973136">CORREÇÃO: ArgumentNullException mensagem de erro de exceção quando um aplicativo baseado no .NET Framework 2.0 SP2 tenta processar uma resposta com comprimento zero de conteúdo a uma solicitação de serviço da Web ASP.NET assíncrona: &quot;O valor não pode ser nulo&quot;</a> é recomendado para o Microsoft .NET Framework 2.0 SP2.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Os usuários podem proteger mensagens com IRM no Outlook. Começando com o Outlook 2003, os modelos do  AD RMS para proteger mensagens com IRM têm suporte.</p></li>
<li><p>regras de proteção de Outlook são um recurso Exchange 2010 e Outlook 2010. Versões anteriores do Outlook não oferecem suporte a esse recurso.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Os dispositivos que oferecem suporte à versão 14.1 do protocolo do Exchange ActiveSync, incluindo dispositivos Windows, podem oferecer suporte ao IRM no Exchange ActiveSync. O aplicativo de email móvel em um dispositivo deve oferecer suporte à marca <strong>RightsManagementInformation</strong> definida na versão 14.1 do Exchange ActiveSync. No Exchange 2013, o IRM no Exchange ActiveSync permite, aos usuários com dispositivos com suporte, visualizar, responder, encaminhar e criar mensagens protegidas por IRM sem solicitar que o usuário conecte o dispositivo a um computador e o ative para IRM. Para detalhes, consulte <a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Gerenciamento de direitos de informação no Exchange ActiveSync</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <EM>ClusterAD RMS</EM> é o termo usado para a implantação do AD RMS em uma organização, incluindo uma implantação de um servidor único. O AD RMS é um serviço da web. Você não precisa configurar um cluster de failover do Windows Server. Para alta disponibilidade e equilíbrio de carga, você pode implantar vários servidores do AD RMS no cluster e usar Balanceamento de Carga de Rede.




> [!IMPORTANT]
> Em um ambiente de produção, não é possível instalar o AD RMS e o Exchange no mesmo servidor.



Exchange 2013 Recursos de IRM oferecem suporte a formatos de arquivo do Microsoft Office. Você pode estender a proteção de IRM para outros formatos de arquivo Implantando protetores personalizados. Para obter mais informações sobre protetores personalizados, consulte proteção de informações e parceiros de controle em [Fornecedores independentes de Software](https://go.microsoft.com/fwlink/p/?linkid=210336).

Voltar ao início

## Configurando e testando o IRM

Você deve usar o Shell de Gerenciamento do Exchange para configurar os recursos de IRM no Exchange 2013. Para configurar recursos de IRM individuais, use o cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)). Você pode habilitar ou desabilitar o IRM para mensagens internas, descriptografia de transporte, descriptografia de relatório do registro no diário, Pesquisa do Exchange e Outlook Web App. Para mais informações sobre como configurar recursos do IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

Depois de configurar um servidor do Exchange 2013, você poderá usar o cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979798\(v=exchg.150\)) para executar testes de ponta a ponta da sua implantação do IRM. Esses testes são úteis para verificar a funcionalidade do IRM imediatamente após a configuração inicial do IRM e também continuamente. O cmdlet executa os testes a seguir:

  - Inspeciona a configuração do IRM para sua organização do Exchange 2013.

  - Examina o servidor do AD RMS para obter informações de versão e hotfix.

  - Verifica se um servidor do Exchange pode ser ativado por RMS, recuperando Certificados de Contas de Direitos (RAC) e um certificado de licenciante do cliente.

  - Adquire modelos de política de direitos do AD RMS do servidor do AD RMS.

  - Verifica se o remetente especificado pode enviar mensagens protegidas com IRM.

  - Recupera uma licença de uso de superusuário para o destinatário especificado.

  - Adquire uma pré-licença para o destinatário especificado.

Voltar ao início

## Estenda o Gerenciamento de Direitos com o conector Rights Management.

O conector Microsoft Rights Management (conector RMS) é um aplicativo opcional que aumenta a proteção dos dados para o seu servidor do Exchange 2013 usando os serviços baseados na nuvem do Microsoft Rights Management. Ao instalar o conector RMS, o mesmo oferece proteção contínua dos dados durante o tempo de vida das informações e como estes serviços são personalizáveis, você pode definir o nível de proteção de que você precisa. Por exemplo, você pode limitar o acesso à mensagem de email para usuários específicos ou definir direitos somente de leitura para certas mensagens.

Para saber mais sobre o conector RMS e como instalá-lo, consulte [conector Rights Management](https://technet.microsoft.com/en-us/library/dn375964.aspx).

