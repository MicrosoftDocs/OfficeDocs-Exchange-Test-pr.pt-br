---
title: 'Configurar substituições de disponibilidade gerenciada: Exchange 2013 Help'
TOCTitle: Configurar substituições de disponibilidade gerenciada
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59890401
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar substituições de disponibilidade gerenciada

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013 SP1_

_**Tópico modificado em:** 2015-11-30_

A disponibilidade gerenciada executa investigação contínua para detectar possíveis problemas com os componentes do Exchange ou suas respectivas dependências, e isso realiza ações de recuperação para garantir que a experiência do usuário final não seja impactada devido a algum problema com qualquer desses componentes. Entretanto, pode haver cenários em que as configurações predefinidas não sejam adequadas ao ambiente. Sondas, monitores e respondentes da disponibilidade gerenciada podem ser personalizados com a criação de uma substituição.

Existem dois tipos de substituições: global e local. Como seus nomes sugerem, uma substituição local está disponível somente no servidor no qual ele é criado e uma substituição global é usada para aplicar uma substituição para vários servidores. Os dois tipos de substituição podem ser criados por um período específico ou para uma versão específica de Exchange, mas não ambos ao mesmo tempo.


> [!NOTE]
> Quando você criar uma substituição, ele não entrarão em vigor imediatamente. Microsoft Exchange serviço de gerenciamento de integridade verifica a cada 10 minutos para que as alterações de configuração e carrega as alterações na configuração detectado. Se você não quiser esperar, você pode reiniciar o serviço.



Para obter tarefas adicionais de gerenciamento, relacionadas à disponibilidade gerenciada, consulte [Gerenciar conjuntos de integridade e a integridade do servidor](manage-health-sets-and-server-health-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Substitui o Shell de Gerenciamento do Exchange para criar um local de uso

Para criar uma substituição local por um período específico, use a seguinte sintaxe.

```powershell
Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>
```

Para criar uma substituição local para uma versão específica de Exchange, use a seguinte sintaxe.

```powershell
Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>
```


> [!NOTE]
> Quando você cria a substituição, os valores usados no parâmetro <EM>Identity</EM> diferenciam maiúsculas de minúsculas.



Este exemplo adiciona uma substituição local que desabilita o Respondente `ActiveDirectoryConnectivityConfigDCServerReboot` no servidor denominado EXCH03 por 20 dias.

```powershell
Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00
```


## Como saber se funcionou?

Para verificar se você criou com êxito uma substituição local, use o cmdlet **Get-ServerMonitoringOverride** para exibir a lista de substituições locais:

```powershell
Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List
```

a substituição deve aparecer na lista.

## Substitui o Shell de Gerenciamento do Exchange para remover um local de uso

Para remover uma substituição local, use a seguinte sintaxe.

```powershell
Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>
```

Este exemplo remove a substituição de local existente do Respondente `ActiveDirectoryConnectivityConfigDCServerReboot` a Exchange conjunto de integridade do servidor EXCH01.

```powershell
Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled
```

## Como verifico se isso funcionou?

Para verificar se você removeu com êxito uma substituição local, use o cmdlet **Get-ServerMonitoringOverride** para exibir a lista de substituições locais:

```powershell
Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List
```

a substituição removida não deve estar na lista.

## Use o Shell de Gerenciamento do Exchange para criar global substitui

Para criar uma substituição global por um período específico, use a seguinte sintaxe.

```powershell
Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>
```

Para criar uma substituição global para uma versão específica de Exchange, use a seguinte sintaxe.

```powershell
Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>
```

> [!NOTE]
> Quando você cria a substituição, os valores usados no parâmetro <EM>Identity</EM> diferenciam maiúsculas de minúsculas.



Este exemplo adiciona uma substituição global que desabilita a investigação `OnPremisesInboundProxy` por 30 dias.

```powershell
Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00
```

Este exemplo adiciona uma substituição global que desabilita o Respondente `StorageLogicalDriveSpaceEscalate` para todos os servidores executando a versão de Exchange 15.01.0225.042.

```powershell
Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"
```

## Como saber se funcionou?

Para verificar se você criou com êxito uma substituição global, use o cmdlet **Get-GlobalMonitoringOverride** para exibir a lista de substituições globais:

```powershell
Get-GlobalMonitoringOverride
```

a substituição deve aparecer na lista.

## Use o Shell de Gerenciamento do Exchange para remover global substitui

Para remover uma substituição global, use a seguinte sintaxe.

```powershell
Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>
```

Este exemplo remove a substituição global existente da propriedade `ExtensionAttributes` da sonda `OnPremisesInboundProxy` no conjunto de integridade `FrontEndTransport` .

```powershell
Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes
```

## Como verifico se isso funcionou?

Para verificar se você removeu com êxito uma substituição global, use o cmdlet **Get-GlobalMonitoringOverride** para exibir a lista de substituições globais:

```powershell
Get-GlobalMonitoringOverride
```

a substituição removida não deve estar na lista.

