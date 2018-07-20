---
title: 'Políticas de caixa de correio para dispositivos móveis: Exchange 2013 Help'
TOCTitle: Políticas de caixa de correio para dispositivos móveis
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 50486139
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Políticas de caixa de correio para dispositivos móveis

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-06-16_

No MicrosoftExchange Server 2013, você pode criar políticas de caixa de correio para dispositivos móveis para aplicar um conjunto comum de políticas ou configurações de segurança a um conjunto de usuários. Depois de implantar o Exchange ActiveSync em sua organização do Exchange 2013, você pode criar novas políticas de caixa de correio para dispositivos móveis ou modificar as políticas existentes. Quando você instala o Exchange 2013, uma política padrão de caixa de correio para dispositivos móveis é criada. Essa política padrão de caixa de correio para dispositivos móveis é atribuída automaticamente a todos os usuários.


> [!IMPORTANT]
> Os telefones celulares com Windows Phone 7 suportam apenas um subconjunto de todas as configurações de diretiva de caixa de correio do Exchange ActiveSync. Para uma lista completa, consulte Windows Phone 7 Synchronization.




> [!WARNING]
> Não há suporte para o leitor de impressão digital do iOS7 como uma senha de dispositivo. Mesmo que o leitor de impressão digital esteja habilitado para proteger o dispositivo iOS7, ainda será necessário criar e inserir uma senha se as políticas de caixa de correio para dispositivos móveis assim exigirem.



## Visão geral de políticas de caixa de correio para dispositivos móveis

Você pode usar políticas de caixa de correio para dispositivos móveis para gerenciar várias configurações diferentes. Eles incluem:

  - Exigir uma senha

  - Especificar o comprimento mínimo da senha

  - Exigir um número ou caractere especial na senha

  - Determinar por quanto tempo um dispositivo pode ficar inativo antes de se exigir que o usuário digite uma senha novamente

  - Apagar um dispositivo após um determinado número de falhas em tentativas de senha

Para obter mais informações sobre todas as configurações que podem ser definidas, consulte Configurações de política para dispositivos móveis.

## Gerenciando políticas de caixa de correio do Exchange ActiveSync

As políticas de caixa de correio para dispositivos móveis podem ser criadas no Centro de Administração do Exchange (EAC) ou no Shell de Gerenciamento do Exchange. Se você criar uma política no EAC, poderá definir apenas um subconjunto das configurações disponíveis. Você pode configurar o restante das configurações usando o Shell.

## Sincronização do Windows Phone 7

Se sua organização possuir telefones celulares com o Windows Phone 7, esses telefones terão problemas de sincronização se certas propriedades de diretiva de caixa de correio do Exchange ActiveSync estiverem configuradas. Para permitir que telefones celulares com Windows Phone 7 sincronizem com uma caixa de correio do Exchange, defina a propriedade **AllowNonProvisionableDevices** como verdadeira ou apenas configure as seguintes propriedades de diretiva de caixa de correio do Exchange ActiveSync:

  - AllowSimplePassword

  - BlockInternetSharing

  - BlockRemoteDesktop

  - DisableDesktopSync

  - DisableIrDA

  - DisableRemovableStorage

  - DeviceWipeThreshold

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - PasswordExpiration

  - PasswordHistory

  - PasswordRequired

## Configurações de política de caixa de correio do dispositivo móvel

A tabela a seguir resume as configurações que podem ser especificadas usando políticas de caixa de correio para dispositivos móveis.

### Configurações de política de caixa de correio do dispositivo móvel

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Permitir Bluetooth</p></td>
<td><p>Esta configuração especifica se um dispositivo móvel permite conexões Bluetooth. As opções disponíveis são Disable, HandsfreeOnly e Allow. O valor padrão é Allow. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir Navegador</p></td>
<td><p>Esta configuração indica se o Pocket Internet Explorer é permitido no dispositivo móvel. Esta configuração não afeta navegadores de terceiros instalados no dispositivo móvel. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Câmera</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel da câmera pode ser utilizado. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir Email do Consumidor</p></td>
<td><p>Esta configuração especifica se o usuário do dispositivo móvel pode configurar uma conta de email pessoal (POP3 ou IMAP4) no dispositivo móvel. O valor padrão é <code>$true</code>. Essa configuração não controlam o acesso às contas de email que está usando programas de email do dispositivo móvel do terceiro. A licença de acesso para cliente Enterprise Exchange é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Sincronização da Área de Trabalho</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel pode ser sincronizado com um computador através de um cabo, Bluetooth ou conexão IrDA. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir Gerenciamento de Dispositivo Externo</p></td>
<td><p>Esta configuração especifica se um programa de gerenciamento de dispositivo externo tem permissão para gerenciar o dispositivo móvel.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Email em HTML</p></td>
<td><p>Esta configuração especifica se o email sincronizado com o dispositivo móvel pode estar no formato HTML. Se esta configuração for definida como <code>$false</code>, todos os emails serão convertidos para texto sem formatação.</p></td>
</tr>
<tr class="even">
<td><p>Permitir Compartilhamento da Internet</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel pode ser utilizado como um modem para um desktop ou computador portátil. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>Esta configuração especifica se as conexões infravermelho são permitidas para e do dispositivo móvel. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir Atualização de OTA Móvel</p></td>
<td><p>Esta configuração especifica se as configurações de política de caixa de correio para dispositivos móveis podem ser enviadas ao dispositivo móvel por uma conexão de dados de celular. O valor padrão é <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir dispositivos não provisionáveis</p></td>
<td><p>Esta configuração especifica se os dispositivos móveis que podem não suportar o aplicativo de todas as configurações de diretiva são permitidos para se conectar ao Exchange 2013 usando Exchange ActiveSync. Permitindo que os dispositivos móveis não provisionáveis tem implicações de segurança. Por exemplo, alguns dispositivos não provisionáveis não podem ser capazes de implementar requisitos de senha de uma organização.</p></td>
</tr>
<tr class="even">
<td><p>Permitir POPIMAPEmail</p></td>
<td><p>Essa configuração especifica se o usuário pode configurar um POP3 ou uma conta de email IMAP4 no dispositivo móvel. O valor padrão é <code>$true</code>. Essa configuração não controlam o acesso por programas de email de terceiros.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Área de Trabalho Remota</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel pode iniciar uma conexão de área de trabalho remota. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir senha simples</p></td>
<td><p>Esta configuração habilita ou desabilita a capacidade de utilizar senhas simples, como 1111 ou 1234. O valor padrão é <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir negociação de algoritmo de criptografia S/MIME</p></td>
<td><p>Esta configuração especifica se o aplicativo de mensagens no dispositivo móvel pode negociar o algoritmo de criptografia se um certificado do destinatário não suportar o algoritmo de criptografia especificado.</p></td>
</tr>
<tr class="even">
<td><p>Permitir certificados de software S/MIME</p></td>
<td><p>Esta configuração especifica se certificados de software S/MIME são permitidos no dispositivo móvel.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir cartão de armazenamento</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel pode acessar informações armazenadas em um cartão de armazenamento. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir mensagem de texto</p></td>
<td><p>Esta configuração especifica se mensagens de texto são permitidas a partir do dispositivo móvel. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir aplicativos não assinados</p></td>
<td><p>Esta configuração especifica se aplicativos não assinados podem ser instalados no dispositivo móvel. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Permitir pacotes de instalação não assinados</p></td>
<td><p>Esta configuração especifica se um pacote de instalação não assinado pode ser executado no dispositivo móvel. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Wi-Fi</p></td>
<td><p>Esta configuração especifica se o acesso à Internet sem fio é permitido no dispositivo móvel. O valor padrão é <code>$true</code>. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Senha alfanumérica necessária</p></td>
<td><p>Esta configuração exige que a senha contenha caracteres numéricos e não-numéricos. O valor padrão é <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Lista de aplicativos aprovados</p></td>
<td><p>Esta configuração armazena uma lista de aplicativos aprovados que podem ser executados no dispositivo móvel. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
<tr class="even">
<td><p>Anexos habilitados</p></td>
<td><p>Esta configuração permite que anexos sejam baixados para o dispositivo móvel. O valor padrão é <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Criptografia de dispositivo habilitada</p></td>
<td><p>Esta configuração permite criptografia no dispositivo móvel. Nem todos os dispositivos móveis podem aplicar criptografia. Para obter mais informações, consulte a documentação do sistema operacional do dispositivo e do dispositivo móvel.</p></td>
</tr>
<tr class="even">
<td><p>Intervalo de atualização da política do dispositivo</p></td>
<td><p>Esta configuração especifica com que frequência a política de caixa de correio para dispositivos móveis é enviada do servidor para o dispositivo móvel.</p></td>
</tr>
<tr class="odd">
<td><p>IRM habilitado</p></td>
<td><p>Esta configuração especifica se o Gerenciamento de Direitos de Informação (IRM) está habilitado no dispositivo móvel.</p></td>
</tr>
<tr class="even">
<td><p>Tamanho máximo do anexo</p></td>
<td><p>Esta configuração controla o tamanho máximo de anexos que podem ser baixados para o dispositivo móvel. O valor padrão é Unlimited.</p></td>
</tr>
<tr class="odd">
<td><p>Filtro de duração máxima do calendário</p></td>
<td><p>Esta configuração especifica o intervalo máximo de dias de calendário que podem ser sincronizados com o dispositivo móvel. Os seguintes valores são aceitos:</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>TrêsDias</p></li>
<li><p>OneWeek</p></li>
<li><p>DuasSemanas</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Filtro de duração máxima de email</p></td>
<td><p>Esta configuração especifica o número máximo de dias para que itens de email sejam sincronizados com o dispositivo móvel. Os seguintes valores são aceitos:</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>TrêsDias</p></li>
<li><p>OneWeek</p></li>
<li><p>DuasSemanas</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Tamanho máximo para truncamento do corpo do email</p></td>
<td><p>Esta configuração especifica o tamanho máximo a partir do qual mensagens de email são truncadas quando sincronizadas com o dispositivo móvel. O valor está em quilobytes (KB).</p></td>
</tr>
<tr class="even">
<td><p>Tamanho máximo para truncamento do corpo em HTML do email</p></td>
<td><p>Esta configuração especifica o tamanho máximo a partir do qual mensagens de email em HTML são truncadas quando sincronizadas com o dispositivo móvel. O valor está em quilobytes (KB).</p></td>
</tr>
<tr class="odd">
<td><p>Tempo de inatividade máximo para bloqueio</p></td>
<td><p>Este valor especifica o período em que o dispositivo móvel pode ficar inativo antes que a senha seja solicitada para reativá-lo. Insira qualquer intervalo entre 30 segundos e 1 hora. O valor padrão é 15 minutos.</p></td>
</tr>
<tr class="even">
<td><p>Máximo de tentativas fracassadas de senha</p></td>
<td><p>Esta configuração especifica quantas tentativas um usuário pode fazer para inserir a senha correta do dispositivo móvel. É possível inserir qualquer número entre 4 e 16. O valor padrão é 8.</p></td>
</tr>
<tr class="odd">
<td><p>Mínimo de caracteres complexos na senha</p></td>
<td><p>Esta configuração especifica o número de conjuntos de caracteres que são necessários na senha do dispositivo móvel. Os conjuntos de caracteres são:</p>
<ul>
<li><p>Letras minúsculas.</p></li>
<li><p>Letras maiúsculas.</p></li>
<li><p>Dígitos 0 a 9.</p></li>
<li><p>Caracteres especiais (por exemplo, exclamação).</p></li>
</ul>
<p>É possível digitar qualquer número entre 1 e 4. O valor padrão é 1.</p>
<p>Para os dispositivos Windows Phone 8, esta configuração especifica o número de conjuntos de caracteres que são necessários na senha. Por exemplo, o valor 3 requer pelo menos um caractere de qualquer três dos conjuntos de caracteres.</p>
<p>Para os dispositivos Windows Phone 10, essa configuração especifica os seguintes requisitos de complexidade de senha:</p>
<ol>
<li><p>Dígitos.</p></li>
<li><p>Dígitos letras maiúsculas e minúsculas.</p></li>
<li><p>Letras maiúsculas, minúsculas e dígitos.</p></li>
<li><p>Dígitos, letras minúsculas, letras maiúsculas e caracteres especiais.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Tamanho mínimo da senha</p></td>
<td><p>Esta configuração especifica o número mínimo de caracteres da senha do dispositivo móvel. É possível digitar qualquer número entre 1 e 16. O valor padrão é 4.</p></td>
</tr>
<tr class="odd">
<td><p>Senha habilitada</p></td>
<td><p>Esta configuração habilita a senha do dispositivo móvel.</p></td>
</tr>
<tr class="even">
<td><p>Expiração da senha</p></td>
<td><p>Esta configuração permite que o administrador configure um período após o qual uma senha de dispositivo móvel deve ser alterada.</p></td>
</tr>
<tr class="odd">
<td><p>Histórico da senha</p></td>
<td><p>Esta configuração especifica o número de senhas antigas que podem ser armazenadas em uma caixa de correio do usuário. Um usuário não pode reutilizar uma senha armazenada.</p></td>
</tr>
<tr class="even">
<td><p>Recuperação de senha habilitada</p></td>
<td><p>Quando essa configuração está habilitada, o dispositivo móvel gera uma senha de recuperação que é enviada ao servidor. Se o usuário esquecer a senha do dispositivo móvel, a senha de recuperação poderá ser utilizada para destravar o dispositivo móvel e permitir que o usuário crie uma nova senha para ele.</p></td>
</tr>
<tr class="odd">
<td><p>Exigir Criptografia do Dispositivo</p></td>
<td><p>Esta configuração especifica se a criptografia do dispositivo é necessária. Se configurada como <code>$true</code>, o dispositivo móvel deve poder dar suporte e implementar criptografia para sincronização com o servidor.</p></td>
</tr>
<tr class="even">
<td><p>Exigir mensagens S/MIME criptografadas</p></td>
<td><p>Esta configuração especifica se as mensagens S/MIME devem ser criptografadas. O valor padrão é <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Exigir algoritmo de criptografia S/MIME</p></td>
<td><p>Esta configuração especifica qual algoritmo obrigatório deve ser usado ao criptografar mensagens S/MIME.</p></td>
</tr>
<tr class="even">
<td><p>Exigir sincronização manual durante o roaming</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel deve ser sincronizado manualmente enquanto estiver em roaming. Permitir sincronização automática em roaming frequentemente leva a custos de dados maiores que os esperados para o plano de dados do dispositivo móvel.</p></td>
</tr>
<tr class="odd">
<td><p>Exigir algoritmo S/MIME assinado</p></td>
<td><p>Esta configuração especifica qual algoritmo obrigatório deve ser usado ao assinar uma mensagem.</p></td>
</tr>
<tr class="even">
<td><p>Exigir mensagens S/MIME assinadas</p></td>
<td><p>Esta configuração especifica se o dispositivo móvel deve enviar mensagens S/MIME assinadas.</p></td>
</tr>
<tr class="odd">
<td><p>Exigir criptografia do cartão de armazenamento</p></td>
<td><p>Esta configuração especifica se o cartão de armazenamento deve ser criptografado. Nem todos os sistemas operacionais dos dispositivos móveis suportam criptografia de cartão de repositório. Para obter mais informações, consulte a documentação do dispositivo móvel e do sistema operacional do dispositivo.</p></td>
</tr>
<tr class="even">
<td><p>Lista de aplicativos InROM não aprovados</p></td>
<td><p>Esta configuração especifica uma lista de aplicativos que não podem ser executados em ROM. A Licença de Acesso para Cliente do Exchange Enterprise é necessária para alterar os valores dessa configuração.</p></td>
</tr>
</tbody>
</table>

