---
title: 'Credenciais de inscrição de borda: Exchange 2013 Help'
TOCTitle: Credenciais de inscrição de borda
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61183346
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Credenciais de inscrição de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Este tópico explica como o processo de Inscrição de Borda provisiona as credenciais que são usadas para ajudar a proteger o processo de sincronização do EdgeSync e como o EdgeSync usa essas credenciais para estabelecer uma conexão LDAP segura entre um servidor de Caixa de Correio do Exchange 2013 e um servidor de Transporte de Borda. Para saber mais sobre Inscrições de Borda, consulte [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

**Sumário**

Edge Subscription process

EdgeSync replication accounts

Authenticate initial replication

Authenticate scheduled synchronization sessions

Renew EdgeSync replication accounts

## Processo de Inscrição de Borda

O servidor de Transporte de Borda é inscrito em um site do Active Directory para estabelecer um relacionamento de sincronização entre os servidores de Caixa de Correio em um site do Active Directory e o servidor de Transporte de Borda inscrito. As credenciais fornecidas durante o processo de Inscrição de Borda são usadas para ajudar a proteger a conexão LDAP entre um servidor de Caixa de Correio e um servidor de Transporte de Borda na rede de perímetro.

Quando você executa o cmdlet **New-EdgeSubscription** em um servidor de Transporte de Borda, as credenciais ESBRA (conta de replicação de inicialização do EdgeSync) são criadas no diretório do AD LDS (Lightweight Directory Services) no servidor local e depois gravadas no arquivo de Inscrição de Borda. Essas credenciais são usadas apenas para estabelecer a sincronização inicial e expirarão 24 horas depois que o arquivo de Inscrição de Borda for criado. Se o processo de Inscrição de Borda não for concluído em 24 horas, será necessário executar o cmdlet **New-EdgeSubscription** novamente para criar um novo arquivo de Inscrição de Borda. O arquivo XML de Inscrição de Borda armazena dados de configuração para a Inscrição de Borda.

O arquivo XML de Inscrição de Borda contém os dados mostrados na tabela a seguir.

### Conteúdo de arquivo de Inscrição de Borda

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Dados de inscrição</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>O nome NetBIOS do servidor de Transporte de Borda. O nome da Inscrição de Borda no Active Directory corresponderá a esse nome.</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>O FQDN (nome de domínio totalmente qualificado) do servidor de Transporte de Borda. Os servidores de Caixa de Correio no site do Active Directory inscrito devem poder localizar o servidor de Transporte de Borda usando DNS para resolver o FQDN.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>A chave pública do certificado auto-assinado do servidor de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>O nome atribuído à ESBRA. A conta ESBRA tem o seguinte formato: ESRA.<em>nome do servidor de Transporte de Borda</em>. ESRA significa conta de replicação do EdgeSync; observe a diferença entre ESBRA (conta de replicação de inicialização) e ESRA.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>A senha atribuída à ESBRA. A senha é gerada usando um gerador de número aleatório e é armazenada no arquivo de Inscrição de Borda em texto não criptografado.</p></td>
</tr>
<tr class="even">
<td><p><strong>EffectiveDate</strong></p></td>
<td><p>A data de criação do arquivo de Inscrição de Borda.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Duração</strong></p></td>
<td><p>O período em que essas credenciais serão válidas antes de expirarem. A conta ESBRA é válida somente por 24 horas.</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>A porta LDAP segura à qual o serviço EdgeSync é associado ao sincronizar dados do Active Directory com o AD LDS. Por padrão, essa é a porta TCP 50636.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>As informações de licenciamento do servidor de Transporte de Borda. Você precisa licenciar o servidor de Transporte de Borda antes de criar a Inscrição de Borda.</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>O número da versão do arquivo de Inscrição de Borda.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>A versão do Exchange do servidor de Transporte de Borda.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> As credenciais da ESBRA são gravadas no arquivo de Inscrição de Borda em texto não criptografado. Você deve proteger esse arquivo por todo o processo de inscrição. Após o arquivo de Inscrição de Borda ser importado para a sua organização do Exchange, você deverá excluir imediatamente esse arquivo do servidor de Transporte de Borda, do compartilhamento de rede que você usou para importar o arquivo para a sua organização do Exchange e de qualquer mídia removível.



Voltar ao início

## Contas de replicação do EdgeSync

As contas de replicação do EdgeSync (ESRA) são uma parte importante da segurança do EdgeSync. A autenticação e a autorização da ESRA são o mecanismo usado para ajudar a proteger a conexão entre um servidor de Transporte de Borda e um servidor de Caixa de Correio.

A ESBRA contida no arquivo de Inscrição de Borda é usada para estabelecer uma conexão LDAP segura durante a sincronização inicial. Depois que o arquivo de Inscrição de Borda é importado para um servidor de Caixa de Correio no site do Active Directory no qual o servidor de Transporte de Borda está sendo inscrito, contas ESRA adicionais são criadas no Active Directory para cada par de servidores de Transporte de Borda-Caixa de Correio. Durante a sincronização inicial, as credenciais de ESRA recém-criadas são replicadas para o AD LDS. Essas credenciais de ESRA são usadas para ajudar a proteger sessões de sincronização posteriores.

A cada conta de replicação do EdgeSync são atribuídas as propriedades mostradas na tabela a seguir.

### Propriedades de Ms-Exch-EdgeSyncCredential

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome de propriedade</th>
<th>Tipo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>Cadeia de caracteres</p></td>
<td><p>O servidor de Transporte de Borda que aceitará essas credenciais.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>String</p></td>
<td><p>O servidor de Caixa de Correio que apresenta estas credenciais. Esse valor ficará vazio se a credencial for a credencial de inicialização.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Quando começar a usar essa credencial.</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Quando parar de usar essa credencial.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>String</p></td>
<td><p>O nome de usuário usado para autenticar.</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>Byte</p></td>
<td><p>A senha usada para autenticação. A senha é criptografada usando <strong>ms-Exch-EdgeSync-Certificate</strong>.</p></td>
</tr>
</tbody>
</table>


As seções a seguir descrevem como as credenciais de ESRA são provisionadas e usadas durante o processo de sincronização do EdgeSync.

## Configurar a conta de replicação de inicialização do EdgeSync

Quando o cmdlet **New-EdgeSubscription** é executado no servidor de Transporte de Borda, a ESBRA é configurada da seguinte maneira:

  - Um certificado auto-assinado (Edge-Cert) é criado no servidor de Transporte de Borda. A chave privada é armazenada no repositório do computador local e a chave pública é gravada no arquivo de Inscrição de Borda.

  - A conta ESBRA é criada no AD LDS, e as credenciais são gravadas no arquivo de Inscrição de Borda.

  - É possível exportar o arquivo de Inscrição de Borda copiando-o para mídia removível (como o Servidor de Borda não está em seu Active Directory, você não poderá usar uma pasta compartilhada para exportar o arquivo). O arquivo agora está pronto para ser importado para um servidor de Caixa de Correio.

## Provisionar contas de replicação do EdgeSync no Active Directory

Quando o arquivo de Inscrição de Borda é importado em um servidor de Caixa de Correio, as seguintes etapas ocorrem para estabelecer um registro da Inscrição de Borda no Active Directory e para provisionar credenciais ESRA adicionais.

1.  Um objeto de configuração de servidor de Transporte de Borda é criado no Active Directory. O certificado Edge-Cert é gravado nesse objeto como um atributo.

2.  Todos os servidores de Caixa de Correio no site do Active Directory inscrito recebem uma notificação do Active Directory de que uma nova Inscrição de Borda foi registrada. Logo que a notificação é recebida, cada servidor de Caixa de Correio recupera a conta ESRA.Edge e a criptografa usando a chave pública Edge-Cert. A conta ESRA.Edge criptografada é gravada no objeto de configuração do servidor de Transporte de Borda.

3.  Cada servidor de Caixa de Correio cria um certificado autoassinado (TransportService-Cert). A chave privada é mantida no repositório do computador local e a chave pública é armazenada no objeto de configuração do servidor de Caixa de Correio no Active Directory.

4.  Cada servidor de Caixa de Correio criptografa a conta ESRA.Edge usando a chave pública de seu próprio certificado TransportService e, depois, a armazena em seu próprio objeto de configuração.

5.  Cada servidor de Caixa de Correio gera uma ESRA para cada objeto de configuração de servidor de Transporte de Borda existente no Active Directory (ESRA.edge.*NomeCaixaCorreio.nº*).
    
    Exemplo: ESRA.edge.Exemplo.0
    
    A senha de ESRA.Edge é gerada por um gerador de números aleatórios e é criptografada usando a chave pública do certificado TransportService-Cert. A senha gerada tem o tamanho máximo permitido para o Windows Server.

6.  Cada conta ESRA.edge.*NomeCaixaCorreio.nº* é criptografada usando a chave pública do certificado Edge-Cert e é armazenada no objeto de configuração do servidor de Transporte de Borda no Active Directory.

As seções a seguir explicam como essas contas são usadas durante o processo de sincronização do EdgeSync.

Voltar ao início

## Autenticar a replicação inicial

A conta ESBRA é usada somente durante o estabelecimento da sincronização inicial. Durante a primeira sessão de sincronização do EdgeSync, as contas ESRA adicionais, ESRA.edge.*NomeCaixaCorreio.nº*, são replicadas para o AD LDS. Essas contas são usadas para autenticar sessões de sincronização do EdgeSync posteriores.

O servidor de Caixa de Correio que executa a replicação inicial é determinado aleatoriamente. O primeiro servidor de Caixa de Correio no site do Active Directory a executar uma verificação de topologia e a descobrir a Inscrição de Borda executa a replicação inicial. Como a descoberta é baseada no tempo da verificação de topologia, qualquer servidor de Caixa de Correio no site pode realizar a replicação inicial.

O EdgeSync inicia uma sessão segura de LDAP do servidor de Caixa de Correio para o servidor de Transporte de Borda. O servidor de Transporte de Borda apresenta seu certificado autoassinado e o servidor de Caixa de Correio verifica se o certificado corresponde ao certificado armazenado no objeto de configuração do servidor de Transporte de Borda no Active Directory. Depois que a identidade do servidor de Transporte de Borda for verificada, o servidor de Caixa de Correio fornecerá as credenciais da conta ESRA.edge.*NomeCaixaCorreio.nº* para o servidor de Transporte de Borda. O servidor de Transporte de Borda verifica as credenciais em relação à conta armazenada no AD LDS.

Depois, o serviço EdgeSync no servidor de Caixa de Correio envia por push os dados de topologia, configuração e destinatário do Active Directory para o AD LDS. A alteração no objeto de configuração do servidor de Transporte de Borda no Active Directory é replicada para o AD LDS. O AD LDS recebe as entradas ESRA.edge.*NomeCaixaCorreio.nº* recém-adicionadas, e o Serviço de Credencial do Microsoft Exchange cria a conta correspondente do AD LDS. Essas contas estão agora disponíveis para autenticar sessões de sincronização do EdgeSync posteriormente agendadas.

## Serviço de Credencial do Microsoft Exchange

O Serviço de Credencial do Microsoft Exchange é parte do processo de Inscrição de Borda. O Serviço de Credencial é executado somente no servidor de Transporte de Borda. Esse serviço cria as contas ESRA recíprocas no AD LDS para que um servidor de Caixa de Correio possa ser autenticado em um servidor de Transporte de Borda para executar a sincronização do EdgeSync. O EdgeSync não se comunica diretamente com o Serviço de Credencial do Microsoft Exchange. O Serviço de Credencial do Microsoft Exchange se comunica com o AD LDS e instala as credenciais de ESRA sempre que o servidor de Caixa de Correio as atualiza.

Voltar ao início

## Autenticar sessões de sincronização agendadas

Depois que a sincronização EdgeSync inicial for concluída, a programação de sincronização do EdgeSync será estabelecida e todos os dados que foram alterados no Active Directory serão atualizados regularmente no AD LDS. Um servidor de Caixa de Correio inicia uma sessão LDAP segura com a instância do AD LDS no servidor de Transporte de Borda. O AD LDS comprova sua identidade com esse servidor de Caixa de Correio apresentando seu certificado autoassinado. O servidor de Caixa de Correio apresenta suas credenciais de ESRA.Edge para o AD LDS. A senha de ESRA.Edge é criptografada usando a chave pública do certificado autoassinado do servidor de Caixa de Correio. Somente aquele servidor de Caixa de Correio específico pode usar aquelas credenciais para autenticação no AD LDS.

Voltar ao início

## Renovar contas de replicação do EdgeSync

A senha para a conta ESRA deve ser compatível com a diretiva de senha do servidor local. Para evitar que o processo de renovação de senha cause falha de autenticação temporária, uma segunda conta ESRA.Edge é criada sete dias antes que a primeira conta ESRA.Edge expire, com um tempo de efetivação de três dias antes do primeiro período de expiração da ESRA. Assim que a segunda conta ESRA.Edge é efetivada, o EdgeSync para de usar a primeira conta e começa a usar a segunda. Quando o período de expiração da primeira conta é alcançado, essas credenciais de ESRA são excluídas. Esse processo de renovação continuará até que a Inscrição de Borda seja removida.

Voltar ao início

