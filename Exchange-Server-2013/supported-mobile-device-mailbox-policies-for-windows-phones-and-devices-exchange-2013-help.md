---
title: 'Suporte a políticas de caixa de correio de dispositivo móvel para Windows telefones e dispositivos: Exchange 2013 Help'
TOCTitle: Suporte a políticas de caixa de correio de dispositivo móvel para Windows telefones e dispositivos
ms:assetid: d76b1d4c-d1f6-4501-a7c9-854327aceda5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ983805(v=EXCHG.150)
ms:contentKeyID: 52058879
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suporte a políticas de caixa de correio de dispositivo móvel para Windows telefones e dispositivos

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Com a versão do Windows Phone 8, Windows 8 e Windows RT, há um número de dispositivos que suportam o Exchange ActiveSync e políticas de caixa de correio de dispositivo móvel. Cada sistema operacional do dispositivo oferece suporte a um conjunto específico de configurações de diretiva de caixa de correio de dispositivo móvel.

## Cliente do Windows e a matriz de compatibilidade do Exchange Server

As tabelas a seguir listam os parâmetros de política de caixa de correio de dispositivo móvel compatível para várias versões do Windows Phone, Windows 8, Windows RT e Exchange server.

## Parâmetros da política de suporte do Windows Phone 7

A tabela a seguir lista as configurações de diretiva de caixa de correio de dispositivo móvel para Windows Phone 7.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
</tr>
<tr class="even">
<td><p>MinPasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>PasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
<tr class="even">
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
</tr>
<tr class="even">
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
</tr>
<tr class="odd">
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
</tr>
<tr class="even">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
</tbody>
</table>


## Parâmetros da política de suporte do Windows Phone 8

A tabela a seguir lista as configurações de diretiva de caixa de correio de dispositivo móvel para o Windows Phone 8.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="even">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>N/D</p></td>
<td><p>IRMEnabled</p></td>
<td><p>IRMEnabled</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>


## Windows 8 e Windows RT parâmetros da política de suporte

A tabela a seguir lista as configurações de diretiva de caixa de correio de dispositivo móvel para Windows 8 e Windows RT.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="odd">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="even">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="odd">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>

