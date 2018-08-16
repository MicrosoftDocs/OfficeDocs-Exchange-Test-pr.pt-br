---
title: 'Configuração clonada do servidor de transporte de borda: Exchange 2013 Help'
TOCTitle: Configuração clonada do servidor de transporte de borda
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61183351
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuração clonada do servidor de transporte de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Os servidores de Transporte de Borda armazenam suas informações de configuração no Lightweight Directory Services (AD LDS) do Active Directory. Você pode instalar mais de um servidor de Transporte de Borda na rede de perímetro e usar um round robin de DNS para ajudar a balancear o tráfego de rede entre os servidores de Transporte de Borda. Round robin é um mecanismo simples usado por servidores de DNS para compartilhar e distribuir cargas de recursos de rede.

Para garantir que todos os servidores de Transporte de Borda usem as mesmas informações de configuração, use os scripts de configuração clonada fornecidos para duplicar a configuração do seu servidor de origem em um servidor de destino.

A *configuração clonada* é usada para implantar novos servidores de Transporte de Borda baseados em um servidor de origem configurado. As informações de configuração do servidor de origem são duplicadas e, depois, exportadas para um arquivo XML. O arquivo XML é então importado para o servidor de destino.

Este tópico fornece uma visão geral do processo de configuração clonado. Para etapas detalhadas sobre a configuração dos servidores de Transporte de Borda com o uso da configuração clonada, consulte [Configurar o servidor de transporte de borda usando configuração clonada](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md).

**Sumário**

Cloned configuration and EdgeSync

Cloned configuration process

Transport configuration information

## Configuração clonada e EdgeSync

Execute o processo EdgeSync depois de importar a configuração clonada. Para executar tarefas de pesquisa de destinatários e de segurança de mensagens, o servidor de Transporte de Borda exige dados que residem no Active Directory. O *EdgeSync* é uma coleção de processos que são executados em um servidor de Caixa de Correio do Exchange 2013 para estabelecer uma replicação unidirecional de informações de destinatários e de configuração do Active Directory para a instância do AD LDS em um servidor de Transporte de Borda. O EdgeSync copia somente as informações necessárias para o servidor de Transporte de Borda executar tarefas antispam e as informações sobre a configuração do conector necessárias para habilitar todo o fluxo de mensagens. O EdgeSync executa atualizações agendadas para que as informações no AD LDS permaneçam atuais.

A configuração clonada não duplica as configurações de Inscrição de Borda de um servidor. Os certificados usados pelo EdgeSync não são clonados. Você deve executar o processo do EdgeSync separadamente para cada servidor de Transporte de Borda. O EdgeSync substitui todas as configurações inclusas em informações de configuração clonadas e em informações de replicação do EdgeSync. Essas configurações incluem conectores de envio, conectores de recebimento, domínios aceitos e domínios remotos.

## Processo de configuração clonada

O processo de configuração clonado consiste em três etapas:

1.  Exporte a configuração do servidor de origem.
    
    Execute o script ExportEdgeConfig.ps1 (localizado em %CaminhoInstalaçãoExchange%Scripts) para exportar as informações de configuração do servidor de origem para um arquivo XML intermediário.

2.  Validar a configuração no servidor de destino.
    
    Execute o script ImportEdgeConfig.ps1 (localizado em %CaminhoInstalaçãoExchange%Scripts). Este script analisa as informações existentes no arquivo XML intermediário para verificar se as configurações exportadas são válidas para o servidor de destino e cria um arquivo de resposta. O arquivo de resposta especifica as informações específicas do servidor usadas na importação da configuração para o servidor de destino. O arquivo de resposta contém entradas para cada configuração do servidor de origem que não é válida para o servidor de destino. Você pode modificar essas configurações para que elas sejam válidas no servidor de destino. Se todas as configurações forem válidas, o arquivo de resposta não conterá entradas.

3.  Importar a configuração no servidor de destino.
    
    O script ImportEdgeConfig.ps1 usa o arquivo XML intermediário e o arquivo de resposta para clonar uma configuração existente ou restaurar o servidor para uma configuração específica.

## Etapa 1: Exportar a configuração do servidor de origem

Após instalar e configurar a função de servidor de Transporte de Borda, execute o script ExportEdgeConfig.ps1 (localizado em %CaminhoInstalaçãoExchange%Scripts). Este script recupera as informações de configuração do servidor de origem e armazena as informações em um arquivo XML intermediário.

As informações a seguir são exportadas do servidor de origem e armazenadas no arquivo XML intermediário:

  - Informações relacionadas ao serviço de transporte e informações do caminho do arquivo de log:
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - Informações relacionadas ao agente de transporte, incluindo configurações de status e de prioridade de cada agente de transporte.

  - Todas as informações relacionadas ao conector de envio. Se algum Conector de envio estiver configurado para usar credenciais, a senha será gravada no arquivo XML intermediário como uma de cadeia de caracteres criptografada. Você pode usar o parâmetro *-key* com os scripts ImportEdgeConfig.ps1 e ExportEdgeConfig.ps1 para especificar a cadeia de caracteres de 32 bytes a ser usada para criptografar e descriptografar senhas. Se você não usar o parâmetro *-key*, uma chave de criptografia padrão será usada.

  - Informações relacionadas ao Conector de recebimento. Para alterar a associação da rede local e as propriedades da porta, você deve modificar as informações de configuração no arquivo de resposta criado na etapa de validação da configuração.

  - Configuração de domínio aceito.

  - Configuração de domínio remoto.

  - Definições de configuração de recursos antispam:
    
      - Informações sobre a Lista de Permissões de IP. Apenas as entradas da lista de permissões de IP que foram configuradas manualmente pelo administrador são exportadas.
    
      - Informações sobre a Lista de Bloqueios de IP.
    
      - Configuração do filtro de conteúdo.
    
      - Configuração do filtro de destinatários.
    
      - Entradas de reconfiguração de endereço.
    
      - Entradas do filtro de anexos.

Voltar ao início

## Etapa 2: Validar a configuração no servidor de destino

O servidor de destino é um servidor Exchange 2013 que tem uma instalação normal da função de servidor de Transporte de Borda. Primeiro, execute o script ImportEdgeConfig.ps1 (localizado em %CaminhoInstalaçãoExchange%Scripts) no servidor de destino para validar as informações existentes no arquivo XML intermediário e para criar o arquivo de resposta. O arquivo de resposta especifica as informações específicas do servidor usadas na importação da configuração para o servidor de destino. O arquivo de resposta contém entradas para cada configuração do servidor de origem que não é válida para o servidor de destino. Você pode modificar essas configurações para que elas sejam válidas para o servidor de destino. Se todas as configurações forem válidas, o arquivo de resposta não conterá entradas. O arquivo XML intermediário pode ser usado em diferentes servidores de destino. O arquivo de resposta é específico para um servidor de destino.

O script ImportEdgeConfig.ps1 (localizado em %CaminhoInstalaçãoExchange%Scripts) executa as seguintes tarefas:

  - Verifica se os caminhos de dados e os caminhos de logs podem ser criados no servidor de destino. Se os caminhos não puderem ser criados, um caminho em branco será inserido no arquivo de resposta.

  - Para cada Conector de envio no arquivo XML, o script adiciona uma entrada em branco para o endereço IP de origem no arquivo de resposta.

  - Para cada Conector de recebimento no arquivo XML, o script adiciona uma entrada em branco para as ligações de rede local no arquivo de resposta.

Você deverá modificar manualmente o arquivo de resposta para fornecer as seguintes informações sobre configurações específicas do servidor:

  - Preencha os caminhos de dados e de log. Se esses caminhos forem mantidos em branco no arquivo de resposta, os caminhos configurados no arquivo XML intermediário serão usados na próxima etapa quando você importar a configuração no servidor de destino.

  - Para cada entrada do Conector de envio, preencha o endereço IP de origem. Se este campo for deixado em branco, ocorrerá um erro na etapa de importação da configuração.

  - Para cada entrada do Conector de recebimento, preencha as ligações de rede local. Se as associações de rede local forem deixadas em branco, ocorrerá um erro na próxima etapa quando você tentar importar a configuração para o servidor de destino.

Voltar ao início

## Etapa 3: Importar a configuração para o servidor de destino

Você pode executar esta etapa em qualquer servidor de destino para clonar a configuração de um servidor de Transporte de Borda existente ou para restaurar o servidor para uma configuração específica. Execute o script ImportEdgeConfig.ps1 (localizado em %CaminhoInstalaçãoExchange%Scripts) para validar e importar a nova configuração. Depois de executar esse script, a configuração do servidor de destino corresponderá às configurações do arquivo XML intermediário e do arquivo de resposta.


> [!IMPORTANT]
> É uma prática recomendada fazer backup da configuração de servidor existente antes de executar o processo de importação de configuração, de modo que se a operação de clonagem falhar, você poderá restaurar o servidor ao seu estado estável anterior.



Esta etapa usa as informações específicas do servidor fornecidas no arquivo de resposta. Se uma configuração não for especificada no arquivo de resposta, os dados do arquivo XML intermediário serão usados. Antes de modificar a configuração, o script valida os dados do arquivo XML intermediário e do arquivo de resposta.

A configuração de importação modifica as seguintes definições da configuração do servidor de destino:

  - A configuração do agente de transporte é modificada.

  - Os conectores existentes no servidor de destino são removidos e os conectores presentes no arquivo XML intermediário são adicionados.

  - Os domínios aceitos existentes são removidos e as entradas de domínio aceito do arquivo XML intermediário são adicionadas.

  - Os domínios remotos existentes são removidos e as entradas de domínio remoto do arquivo XML intermediário são adicionadas.

  - As entradas da Lista de Permissões de IP existentes são removidas e as entradas da Lista de Permissões de IP no arquivo intermediário de domínios remotos são adicionadas.

  - As entradas existentes da Lista de Bloqueios de IP são removidas e as entradas da Lista de Bloqueios de IP do arquivo intermediário de domínios remotos são adicionadas.

  - A seguinte configuração anti-spam é clonada no servidor de destino:
    
      - Configuração do filtro de conteúdo
    
      - Configuração do filtro de destinatários
    
      - Entradas de reconfiguração de endereço
    
      - Entradas do filtro de anexos

Voltar ao início

## Informações de configuração de transporte

As definições do objeto de configuração de transporte definem configurações de transporte de email para todo o servidor em um servidor de Transporte de Borda. Quando você importa o arquivo XML intermediário para o servidor de destino, todas as configurações do objeto de configuração de transporte, exceto o seguinte, são importadas:

  - Os nomes gerais e as datas de criação do arquivo XML exportado

  - Informações do conector de envio

  - Informações do conector de recebimento

  - Entradas do filtro de anexos

  - A entrada do atributo **MaxDumpsterSizePerStorageGroup**

Após a conclusão do processo de importação, você pode também definir as configurações usando o cmdlet **Set-TransportConfig**. Para obter mais informações, consulte [Set-TransportConfig](https://technet.microsoft.com/pt-br/library/bb124151\(v=exchg.150\)).

Os atributos na tabela a seguir estão associados ao objeto de configuração de transporte e aos valores padrão. Você pode configurar esse objeto tanto nos servidores de Caixa de Correio quanto nos servidores de Transporte de Borda. Entretanto, vários atributos só se aplicarão ao serviço de Transporte em servidores de Caixa de Correio do Exchange 2013. A configuração desses atributos em um servidor de Transporte de Borda não terá efeito.

### Valores padrão e atributos de configuração de transporte

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Descrição</th>
<th>Valor padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>Esse atributo especifica se categorias do Microsoft Outlook devem ser desmarcadas durante a conversão de conteúdo.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>Esse atributo especifica os códigos de notificação de status de entrega (DSN) que fazem com que a mensagem DSN seja copiada para o endereço de email do postmaster. Códigos DSN são inseridos no formato <em>x.y.z</em> e são separados por vírgulas.</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>Esse atributo especifica uma lista de endereços IP ou intervalos de endereços IP de servidores SMTP internos que devem ser ignorados pelo recurso de ID de remetente e de filtragem de conexão.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>Esse atributo especifica o endereço de email para o qual os relatórios de diário serão enviados se a caixa de correio de registro no diário não estiver disponível. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>Esse atributo especifica o tamanho máximo do dumpster de transporte de um servidor de Caixa de Correio. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>18 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>Esse atributo especifica por quanto tempo uma mensagem de email deverá permanecer no dumpster de transporte de um servidor de Caixa de Correio. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>Esse atributo especifica o tamanho máximo de mensagem que pode ser recebido pelos destinatários na organização. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>Esse atributo especifica o número máximo de destinatários permitidos em uma única mensagem de email. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>5,000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>Esse atributo especifica o tamanho máximo da mensagem que pode ser enviada pelos remetentes na organização. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>Esse atributo especifica os domínios remotos que usarão autenticação mútua de TLS (Transport Layer Security) por meio de conectores de recebimento configurados para oferecer suporte à Segurança de Domínio. Vários domínios podem ser separados por vírgulas. O caractere curinga (*) não tem suporte nos domínios listados nesse atributo.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>Esse atributo especifica os domínios remotos que usarão autenticação mútua de TLS quando forem enviados emails por meio de um conector de Envio configurado para oferecer suporte à Segurança de Domínio e ao espaço de endereçamento do domínio de destino. Vários domínios podem ser separados por vírgulas. O caractere curinga (*) não tem suporte nos domínios listados nesse atributo.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>O atributo verifica se clientes de email que estão enviando mensagens de caixas de correio em servidores de Caixa de Correio estão usando o envio de MAPI criptografado. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda. Os valores válidos para esse atributo são <code>$true</code> ou <code>$false</code>.</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>Esse atributo especifica se as mensagens de voz da Unificação de Mensagens serão registradas em diário pelo agente Registro no Diário. Esse atributo não se aplica à configuração de um servidor de Transporte de Borda.</p></td>
<td><p>Verdadeiro</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se o servidor de Transporte de Borda for inscrito na organização do Exchange posteriormente, o valor do atributo <STRONG>InternalSMTPServers</STRONG> será substituído durante o processo do EdgeSync. Para obter mais informações, consulte <A href="edge-subscriptions-exchange-2013-help.md">Inscrições de Borda</A>.



Voltar ao início

