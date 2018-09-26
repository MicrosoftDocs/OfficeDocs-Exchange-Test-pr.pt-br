---
title: 'Atualizar UM do Exchange 2010 para UM do Exchange 2013: Exchange 2013 Help'
TOCTitle: Atualizar UM do Exchange 2010 para UM do Exchange 2013
ms:assetid: 01aa5dab-689b-4738-afab-0d2f11a60b39
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn169226(v=EXCHG.150)
ms:contentKeyID: 54651958
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualizar UM do Exchange 2010 para UM do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Quando você está atualizando uma organização do Microsoft Exchange 2010 com Unificação de Mensagens (UM) para Exchange 2013 com Unificação de Mensagens, há etapas necessárias e outras que já foram executadas como parte de sua implantação do Exchange 2010 UM. Dependendo de seu ambiente de telefonia e dos componentes de UM criados e configurados para suportar a Unificação de Mensagens no Exchange 2010, talvez seja necessário implantar equipamentos de telefonia adicionais, incluindo gateways VoIP (Voz sobre IP), IP PBXs (Private Branch eXchanges) ou PBXs tradicionais ou habilitados para SIP e, em seguida, criar e configurar quaisquer componentes UM adicionais que serão necessários para o Exchange 2013 UM.

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 45-90 minutos.

  - Verifique se você tem as permissões apropriadas na organização do Exchange 2010 e do Exchange 2013 para criar e configurar todos os componentes necessários.

  - Verifique se você implantou e configurou corretamente seus componentes de telefonia, incluindo gateways VoIP e PBXs, IP PBXs ou PBXs habilitados para SIP (Protocolo de Iniciação de Sessão).

  - Verifique se instalou e configurou corretamente os servidores de Acesso para Cliente executando o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange (Roteador de Chamadas de UM) e os servidores de Caixa de Correio executando o serviço de Unificação de Mensagens (UM) do Microsoft Exchange. Para saber mais sobre serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).
    

    > [!WARNING]  
    > Você deve implantar ao menos um servidor de Caixa de Correio do Exchange 2013 em sua organização antes de configurar os gateways de VoIP ou PBXs IP para enviar o SIP de UM e tráfego de RTP aos servidores de Acesso para Cliente do Exchange 2013.



  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Como fazer isso?

## Etapa 1: Baixar e instalar os pacotes de idioma de UM necessários

Pacotes de idioma de UM permitem que chamadores e usuários do Outlook Voice Access interajam com o sistema de caixa postal em vários idiomas. Depois de instalar um idioma adicional em um servidor de Caixa de Correio do Exchange 2013, os chamadores e os usuários do Outlook Voice Access poderão ouvir as mensagens de email e interagir com o sistema de caixa postal nesse idioma. No entanto, para disponibilizar o idioma a todas as chamadas de entrada, é necessário instalar os pacotes de idioma de UM exigidos em todos os servidores de Caixa de Correio do Exchange 2013. Isso ocorre porque todo servidor de Caixa de Correio do Exchange 2013 pode atender às chamadas de entrada para Unificação de Mensagens.

Por padrão, quando você instala um servidor de Caixa de Correio do Exchange 2013, o pacote de idioma Inglês dos EUA (en-US) é instalado. Essa é a única opção de idioma disponível para o seu plano de discagem, a menos que você instale outro pacote de idioma de UM. (O Inglês (Estados Unidos) não poderá ser removido, a menos que você remova o servidor de Caixa de Correio do computador.) Depois de instalar um pacote de idiomas de UM em um servidor de Caixa de Correio do Exchange 2013, o idioma associado ao pacote de idiomas também será listado como uma opção disponível ao configurar o idioma padrão para o plano de discagem. Por padrão, como um atendedor automático de UM é vinculado a um plano de discagem de UM quando o atendedor automático é criado, ele usa a configuração de idioma padrão do plano de discagem de UM vinculado. Entretanto, essa definição pode ser alterada após a criação de um atendedor automático de UM.


> [!NOTE]  
> Se Inglês (Estados Unidos) for o único idioma que você desejar oferecer para seu plano de discagem, ignore esta etapa e vá para a etapa 2.



Você pode adicionar os pacotes de idiomas de Unificação de MENSAGENS usando o comando setup.exe ou executando o programa de instalação do *\<UMLanguagePack\>*.exe depois de baixar o pacote de idiomas de Unificação de MENSAGENS do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obter mais informações, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md).

Esse exemplo usa setup.exe para instalar o pacote de idioma de UM japonês (ja-JP).

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

## Etapa 2: Mova a caixa de correio do sistema Exchange 2010 usada para saudações personalizadas, anúncios, menus e prompts de UM para o Exchange 2013

As saudações personalizadas, anúncios, menus e prompts são usados pelos planos de discagem e atendedores automáticos de Unificação de Mensagens. A caixa de correio do sistema chamada {e0dc1c29-89c3-4034-b678-e6c29d823ed9} é criada quando o Exchange 2010 ou o Exchange 2013 é instalado e usada para dar suporte a recursos como Aprovação de Mensagem e Pesquisa em Várias Caixas de Correio. Essa caixa de correio do sistema também é usada para armazenar saudações personalizadas, anúncios, menus e prompts do plano de discagem e do atendedor automático. Se a caixa de correio do sistema não existir, você poderá usar o comando **Setup /PrepareAD** para criar uma.

Por padrão, as caixas de correio do sistema não são visíveis no Centro de administração do Exchange (EAC). Você pode obter uma lista das caixas de correio do sistema executando uma das seguintes opções:

Esse comando retorna uma lista com todas as caixas de correio do sistema.

```powershell
Get-Mailbox -Arbitration
```

Esse comando retorna uma lista das caixas de correio do sistema e suas propriedades ou configurações individuais.

```powershell
Get-Mailbox -Arbitration |fl
```

Ao usar essa caixa de correio do sistema, as saudações personalizadas, anúncios, menus e prompts podem ser armazenados em backup e restaurados juntamente com outras caixas de correio em um banco de dados. Isso reduz a quantidade de recursos necessária. O armazenamento de saudações personalizadas, anúncios, menus e prompts em uma caixa de correio do sistema remove quaisquer inconsistências possíveis que possam ter ocorrido. Para saber mais sobre movimentações de caixas de correio, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Opcional: Exporte e importe manualmente saudações personalizadas, anúncios, menus e prompts do plano de discagem e do atendedor automático

Pode haver situações em que a caixa de correio do sistema Exchange 2010 tenha sido mudada e você ainda precisa exportar e importar as saudações personalizadas, anúncios, menus e prompts que são usadas com planos de discagem e atendedores automáticos do UM a partir da caixa de correio do sistema Exchange 2010 para a caixa de correio do sistema Exchange 2013. A caixa de correio do sistema nas duas versões é chamada de {e0dc1c29-89c3-4034-b678-e6c29d823ed9}.

As saudações personalizadas, anúncios, menus e prompts são arquivos de áudio (no formato .wav ou .wma) usados pela UM para as seguintes finalidades:

  - Em planos de discagem de UM, os arquivos de áudio são usados para saudações de boas-vindas personalizadas e anúncios informativos. Eles são reproduzidos quando os usuários do Outlook Voice Access ligam para um número do Outlook Voice Access.

  - Em atendedores automáticos de UM, os arquivos de áudio são usados para saudações personalizadas para horários comerciais e não comerciais, anúncios informativos, prompts de menu e menus de navegação. Eles são reproduzidos quando os chamadores ligam para um número de atendimento automático de UM.

Ao exportar e importar saudações personalizadas, anúncios, menus e prompts do Exchange 2010 para o Exchange 2013, é necessário usar os cmdlets **Export-UMPrompt** e **Import-UMPrompt**. Não é possível usar o EAC para exportar ou importar prompts personalizados. Em um servidor do Exchange 2010, use o cmdlet **Export-UMPrompt** para exportar o plano de discagem do Exchange 2010 e os prompts do atendedor automático. Depois de exportar os prompts, é possível importá-los para o servidor de Caixa de Correio do Exchange 2013. Quando você executa o cmdlet **Export-UMPrompt** de seu servidor do Exchange 2010, o comando executa uma pesquisa de GUID ou de identificador de objeto para o plano de discagem ou atendedor automático no Active Directory e a consulta para determinar se há quaisquer saudações personalizadas, anúncios, menus ou prompts. Se houver, as saudações personalizadas, anúncios, menus ou prompts serão salvos no diretório especificado. Depois de exportar todas as saudações personalizadas, anúncios, menus e prompts, use o cmdlet **Import-UMPrompt** para importar os prompts para a caixa de correio de seu sistema do Exchange 2013.

Este exemplo exporta a saudação de boas-vindas do plano de discagem da UM `MyUMDialPlan` e a salva como o arquivo `welcomegreeting.wav`.

```powershell
$prompt = Export-UMPrompt -PromptFileName "customgreeting.wav" -UMDialPlan MyUMDialPlan
set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte
```

Este exemplo importa o arquivo de saudação de boas-vindas `welcomegreeting.wav` de d:\\UMPrompts para o plano de discagem da UM `MyUMDialPlan`.

```powershell
[byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c
```

Este exemplo exporta uma saudação personalizada para o atendedor automático da UM `MyUMAutoAttendant` e a salva como o arquivo `welcomegreetingbackup.wav`.

```powershell
Export-UMPrompt -PromptFileName "welcomegreeting.wav" -UMAutoAttendant MyUMAutoAttendant
set-content -Path "e:\UMPromptsBackup\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte
```

Este exemplo importa o arquivo de saudação de boas-vindas `welcomegreeting.wav` de d:\\UMPrompts para o atendedor automático de UM `MyUMAutoAttendant`.

```powershell
[byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c
```

Para saber mais sobre os prompts personalizados para UM, consulte:

  - [Importar e exportar saudações personalizadas, anúncios, menus e prompts](import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md)

  - [Import-UMPrompt](https://technet.microsoft.com/pt-br/library/dd876899\(v=exchg.150\))

  - [Export-UMPrompt](https://technet.microsoft.com/pt-br/library/dd876882\(v=exchg.150\))

  - [Saudações e prompts de idiomas de Unificação de MENSAGENS](um-languages-prompts-and-greetings-exchange-2013-help.md)

## Etapa 4: Exportar e importar certificados

Se você estiver usando planos de discagem SIP Protegido ou Protegidos em sua organização do Exchange 2010, será necessário exportar e importar os certificados que foram usados para seus servidores de Caixa de Correio e de Acesso para Cliente do Exchange 2013. O TLS mútuo (Mutual Transport Layer Security) é usado para criptografar dados enviados entre seus servidores do Exchange 2013 e os gateways VoIP, IP PBXs e PBXs habilitados para SIP. Os certificados vinculam a identidade do proprietário do certificado a um par de chaves eletrônicas (públicas e privadas) que são usadas para criptografar e assinar digitalmente as informações. Você pode usar um dos seguintes certificados para os serviços UM e Roteador de Chamadas de UM:

  - Um certificado autoassinado (Exchange)

  - Um certificado PKI (infraestrutura de chave pública) interno

  - Um certificado comercial de terceiros

Por padrão, quando você instala o Exchange 2013, dois certificados autoassinados são criados: **Microsoft Exchange Server Auth Certificate** e **Microsoft Exchange**. O certificado autoassinado do **Microsoft Exchange** pode ser usado para UM a fim de criptografar dados, mas você precisa atribuir o certificado aos serviços de UM e de Roteador de chamadas de UM. Esse certificado autoassinado pode ser copiado e importado nos gateways VoIP, IP PBXs e PBXs habilitados para SIP. No entanto, ele não pode ser usado quando você está integrando UM com o Microsoft Lync Server.

Para habilitar a UM a fim de criptografar dados enviados entre seus servidores do Exchange 2013 e gateways VoIP, IP PBXs e PBXs habilitadospara SIP, você precisa fazer o seguinte:

  - Use um certificado de UM autoassinado existente, crie um novo certificado do Exchange autoassinado, envie uma solicitação de certificado a uma autoridade de certificação interna a fim de obter um certificado PKI ou compre um certificado comercial de terceiro que você possa usar para TLS mútuo entre seus servidores de caixa de Correio do Exchange 2013 e de Acesso para Cliente e os gateways VoIP, IP PBXs e PBXs habilitado para SIP.
    
    Crie um certificado autoassinado do Exchange usando o EAC, da seguinte maneira:
    
    1.  No EAC, navegue até **Servidores** \> **Certificados** e depois clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").
    
    2.  Na página **Novo certificado do Exchange**, escolha **Criar um certificado autoassinado** e selecione **Avançar**.
    
    3.  Insira um nome amigável para o certificado e selecione **Avançar**.
    
    4.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para selecionar os servidores do Exchange aos quais você deseja aplicar este certificado e selecione **Avançar**.
    
    5.  Especifique os domínios que você deseja incluir em seu certificado e selecione **Avançar**. Se você quiser adicionar um domínio para um serviço, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    6.  Verifique se os domínios incluídos estão corretos e selecione **Concluir**.
    

    > [!IMPORTANT]  
    > Ao usar o EAC para criar um certificado, você não receberá uma solicitação para habilitar os serviços para o certificado. Após a criação do certificado, você poderá usar o EAC para habilitar os serviços. Para obter mais informações sobre como habilitar um certificado para os serviços, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM</A>.

    
    Crie um certificado autoassinado do Exchange executando o seguinte comando no Shell.
    
    ```powershell
    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    ```
    

    > [!NOTE]  
    > Se você especificar os serviços que deseja habilitar usando o parâmetro <EM>Services</EM>, você receberá uma solicitação para habilitar os serviços para o certificado que você criou. Nesse exemplo, você receberá uma solicitação para habilitar o certificado para os serviços Unificação de Mensagens e Roteador de Chamada para Unificação de Mensagens. Para obter mais informações sobre como habilitar um certificado para os serviços, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM</A>.

  - Importe o certificado que será usado em todos os servidores de Caixa de Correio e Acesso para Cliente do Exchange 2013 em sua organização. Se você usar o certificado autoassinado do Exchange 2013, será necessário copiar o certificado, importá-lo nos gateways VoIP, IP PBXs ou PBXs habilitado para SIP. Se você usar o certificado autoassinado a partir do Exchange 2010, o SAN (Nome Alternativo da Entidade) deverá conter os nomes de computador de todos os servidores do Exchange 2013. Se você tiver servidores de Unificação de Mensagens do Exchange 2010 em sua organização, poderá usar o certificado autoassinado do Exchange 2013, mas será necessário adicionar os nomes de computadores dos servidores de UM do Exchange 2010 para o SAN no certificado do Exchange 2013.

  - Habilite ou atribua o certificado a ser usado aos serviços UM e Roteador de Chamadas de UM nos servidores de Acesso para Cliente e de Caixa de Correio em sua organização.
    
    Habilite o serviço de UM e o serviço Roteador de Chamadas de UM em todos os servidores do Exchange 2013 a usar o certificado autoassinado do Exchange usando o EAC, da seguinte maneira:
    
    1.  No EAC, navegue até **Servidores** \> **Certificados**, selecione o certificado no qual você deseja habilitar os serviços e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    2.  Na página **Procedimento**, selecione **Serviços**, **Unificação de Mensagens** e selecione **roteador de chamadas de Unificação de Mensagens**.
    
    Habilite um certificado autoassinado do Exchange executando o seguinte comando no Shell.
    
    ```powershell
    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'
    ```

  - Configure quaisquer planos de discagem de UM novos ou existentes como SIP Protegido ou Protegido.

  - Configure o modo de inicialização de UM como TLS ou Duplo nos servidores de Acesso para Cliente e Caixa de Correio em sua organização.

  - Crie e configure Gateways IP da UM novos ou existentes com um nome de domínio totalmente qualificado (FQDN).

  - Configure a porta de escuta nos gateways IP da UM para usar a porta TLS 5061.

  - Reinicie o serviço Roteador de Chamadas de UM em todos os servidores de Acesso para Cliente do Exchange 2013 e reinicie o serviço UM em todos os servidores de Caixa de Correio do Exchange 2013. Para saber mais sobre serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

## Etapa 5: Configurar o modo de inicialização de UM em todos os servidores de Acesso para Cliente Exchange 2013

Se você estiver usando planos de discagem SIP Protegido ou Protegido, configure o modo de inicialização de UM em seus servidores de Acesso para Cliente do Exchange 2013. É possível especificar o modo de inicialização de UM para o serviço de Roteador de Chamada de UM em um servidor de Acesso para Cliente do Exchange 2013 usando o EAC ou o Shell de Gerenciamento do Exchange. Por padrão, o servidor de Acesso para Cliente será iniciado em modo TCP, mas se você estiver usando o protocolo TLS para criptografar tráfego VoIP, será preciso configurar o servidor de Acesso para Cliente para que use o modo TLS ou Duplo. Recomendamos que todos os servidores de Acesso para Cliente do Exchange 2013 seja configurado para usar Duplo como o modo de inicialização de UM. Isso porque todos os servidores de Acesso para Cliente do Exchange 2013 podem atender às chamadas recebidas para todos os planos de discagem de UM, e esses planos de discagem podem ter configurações de segurança diferentes. Se o modo de inicialização de UM for alterado, será necessário reiniciar o serviço Roteador de Chamadas de UM para que as alterações tenham efeito. Para saber mais sobre serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

Configure o modo de inicialização de UM em um servidor de Acesso para Cliente do Exchange 2013 usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor do Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Roteador de Chamadas de UM** \> **modo de inicialização de UM**, selecione uma das seguintes opções na lista suspensa:
    
      - **TCP**   Use essa opção se não estiver usando mTLS e se estiver usando somente planos de discagem Desprotegidos.
    
      - **TLS**   Use essa opção se você estiver usando mTLS e estiver usando apenas planos de discagem SIP Protegido ou Protegido.
    
      - **DUAL**   Use essa opção se você estiver usando mTLS e estiver usando planos de discagem Não protegido, SIP Protegido ou Protegido.

5.  Depois de selecionar o modo de inicialização de UM, clique em **Salvar**.

Configure o modo de inicialização de UM em um servidor de Acesso para Cliente do Exchange 2013 executando o seguinte comando no Shell.

```powershell
Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual
```

## Etapa 6: Configurar o modo de inicialização de UM em todos os servidores de Caixa de Correio Exchange 2013

Se você estiver usando planos de discagem SIP Protegido ou Protegido, configure o modo de inicialização de UM em seus servidores de Caixa de Correio do Exchange 2013. É possível especificar o modo de inicialização de UM para o serviço UM em um servidor de Caixa de Correio do Exchange 2013 usando o EAC ou o Shell. Por padrão, o servidor de Caixa de Correio do Exchange 2013 iniciará no modo TCP, mas se você estiver usando o protocolo TLS para criptografar tráfego VoIP, será preciso configurar o servidor de Caixa de Correio do Exchange 2013 para usar o modo TLS ou Duplo. Recomendamos que todos os servidores de Caixa de Correio do Exchange 2013 seja configurado para usar Duplo como o modo de inicialização de UM. Isso porque todos os servidores de Caixa de Correio do Exchange 2013 podem atender às chamadas recebidas para todos os planos de discagem de UM, e esses planos de discagem podem ter configurações de segurança diferentes. Se o modo de inicialização de UM for alterado, será necessário reiniciar o serviço UM para que as alterações tenham efeito. Para saber mais sobre serviços de UM, consulte [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md).

Configure o modo de inicialização de UM em um servidor de Caixa de Correio do Exchange 2013 usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor do Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Serviço de UM** \> **modo de inicialização de UM**, selecione uma das seguintes opções na lista suspensa:
    
      - **TCP**   Use essa opção se não estiver usando mTLS e se estiver usando somente planos de discagem Desprotegidos.
    
      - **TLS**   Use essa opção se você estiver usando mTLS e estiver usando apenas planos de discagem SIP Protegido ou Protegido.
    
      - **DUAL**   Use essa opção se você estiver usando mTLS e estiver usando planos de discagem Não protegido, SIP Protegido ou Protegido.

5.  Depois de selecionar o modo de inicialização de UM, clique em **Salvar**.

Configure o modo de inicialização de UM em um servidor de Caixa de Correio do Exchange 2013 executando o seguinte comando no Shell.

```powershell
Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual
```

## Etapa 7: Criar ou configurar planos de discagem de UM existentes

Dependendo de sua implantação existente do Exchange 2010, você pode precisar criar novos planos de discagem UM ou configurar seus planos de discagem existentes. Um plano de discagem de UM representa um conjunto de PBXs ou IP PBXs tradicionais ou habilitados para SIP que compartilham números de ramais de usuários comuns. Todos os ramais de usuários hospedados em PBXs ou IP PBXs tradicionais ou habilitados para SIP dentro de um plano de discagem contêm o mesmo número de dígitos. Os usuários podem discar para outros ramais telefônicos sem a necessidade de acrescentar um número especial ao ramal ou discar o número completo do telefone.

Os planos de discagem de UM são usados na Unificação de Mensagens do para garantir que os ramais de telefone do usuário sejam exclusivos. Em algumas redes de telefonia, há vários PBXs ou IP PBXs. Nessas redes de telefonia, pode haver dois usuários com o mesmo ramal telefônico. Os planos de discagem da UM resolvem esta situação. Colocar os dois usuários em dois planos de discagem de UM separados torna seus ramais exclusivos. Para obter mais informações, consulte [Planos de discagem de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-dial-plans).

Se for necessário, crie um plano de discagem UM usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM** e clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Novo Plano de Discagem de UM**, preencha as seguintes caixas:
    
      - **Nome**   Digite o nome do plano de discagem. O nome plano de discagem de UM é obrigatório e deve ser exclusivo. Porém, o nome digitado é usado apenas para exibição no EAC e no Shell. O comprimento máximo de nome de plano de discagem de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Embora a caixa para o nome do plano de discagem possa aceitar 64 caracteres, esse nome não pode ter mais de 49 caracteres. Se você tentar criar um nome de plano de discagem com mais de 49 caracteres, receberá uma mensagem de erro. A mensagem mostrará que a política de caixa de correio de UM não pode ser gerada, pois o nome do plano de discagem de UM é muito longo. Isso ocorre porque, quando você cria um plano de discagem, uma política de caixa de correio de UM padrão chamada **Política Padrão** de *\<DialPlanName\>* também é criada. Quando os 15 caracteres na política padrão são adicionados ao nome do plano de discagem, o total de caracteres excede o limite. O parâmetro *name* tanto para o plano de discagem de UM quanto para a política de caixa de correio de UM pode ter 64 caracteres. Contudo, se o nome do plano de discagem tiver mais de 49 caracteres, o nome da diretiva de caixa de correio de UM padrão terá mais de 64 caracteres, não sendo permitido pelo sistema.
    
      - **Comprimento do ramal (dígitos)**   Insira o número de dígitos para números de ramal no plano de discagem. O número de dígitos em números de ramal baseia-se no plano de discagem de telefonia criado em um PBX. Por exemplo, se um usuário associado a um plano de discagem de telefonia discar um ramal com quatro dígitos para chamar outro usuário do mesmo plano de discagem de telefonia, selecione 4 como o número de dígitos do ramal.
        
        Essa é uma caixa necessária que tem um intervalo de valor de 1 a 20. O tamanho de ramal normalmente varia de 3 a 7 números. Se o ambiente de telefonia existente incluir números de ramais, será preciso especificar um número de dígitos que corresponda ao número de dígitos nesses ramais.
        
        Ao criar um plano de discagem de ramal telefônico, você é obrigado a inserir um número de ramal para o usuário, se ele estiver vinculado a um plano de discagem de ramal telefônico. Um número de ramal é também necessário com planos de discagem de Session Initiation Protocol (SIP) ou planos de discagem E.164 quando um usuário habilitado para UM é vinculado a um plano de discagem URI SIP ou E.164. O número de ramal é usado pelos usuários do Outlook Voice Access quando eles acessam sua caixa de correio do Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Segurança UI\_VoIP)
    
      - **Código de País/Região**   Use essa caixa para digitar o código numérico do país/região usado para chamadas de saída. Esse número precederá automaticamente o número de telefone discado. Essa caixa aceita de 1 a 4 dígitos. Por exemplo, nos Estados Unidos, o código de país/região é 1. No Reino Unido, é 44.

3.  Clique em **Salvar**.

Se for necessário, você pode criar um plano de discagem de UM executando o seguinte comando no Shell.

```powershell
New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured
```

Se for necessário, você pode configurar um plano de discagem de UM existente usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  No modo de exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**. Use as opções de configuração para exibir configurações de plano de discagem específicos e para habilitar ou desabilitar os recursos.

Se for necessário, você pode configurar um plano de discagem de UM existente usando o Shell:

```powershell
Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured
```

Quando você implantou a Unificação de Mensagens do Exchange 2010, precisou adicionar um servidor de Unificação de Mensagens a um plano de discagem UM para poder responder às chamadas recebidas. Isso não é mais necessário. No Exchange 2013, os servidores de Acesso para Cliente e de Caixa de Correio não podem ser vinculados a um ramal telefônico ou plano de discagem E.164, mas precisa estar vinculado a planos de discagem URI do SIP. Os servidores de Acesso para Cliente e de Caixa de Correio responderão todas as chamadas de entrada de todos os tipos de planos de discagem.

## Etapa 8: Criar ou configurar gateways IP de UM existentes

Dependendo de sua implantação existente do Exchange 2010, talvez seja necessário criar novos gateways IP da UM ou configurar seus planos de discagem existentes. Se você estiver usando planos de discagem SIP Protegido ou Protegido, será necessário criar um gateway IP da UM com um FQDN e usar o Shell para configurá-lo a fim de escutar na porta 5061. Para gateways IP da UM existentes, verifique se eles estão configurados com um FQDN e se estão escutando na porta 5061. Se o gateway IP de UM não usar um FQDN, use o EAC ou o Shell para alterar o endereço. Se o gateway IP da UM não usar a porta 5061, use o Shell para alterar a porta. Você pode ver as configurações de um gateway IP da UM usando o cmdlet **Get-UMIPGateway**.

Um gateway IP de UM representa um gateway físico de Voz sobre IP (VoIP), IP PBX ou PBX habilitado para SIP. Antes que um gateway VoIP, PBX IP ou PBX habilitado para SIP possa ser usado para responder chamadas de entrada e enviar chamadas de saída para usuários de correio de voz, um gateway IP da UM deve ser criado no serviço de diretório.

A combinação do objeto de gateway IP de UM e um objeto de grupo de busca de UM estabelece um vínculo entre um gateway VoIP, um IP PBX ou PBX habilitado para SIP e um plano de discagem de UM. Ao criar vários grupos de busca da UM, você pode associar um gateway IP da UM único com vários planos de discagem da UM. Para obter mais informações, consulte [Gateways IP de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways).

Se for necessário, crie um gateway IP da UM usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Unificação de Mensagens** \> **gateways IP da UM** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página do **Novo Gateway IP da UM**, insira as seguintes informações:
    
      - **Nome**   Use essa caixa para especificar um nome exclusivo para o gateway IP de UM. Esse é um nome de exibição que aparece no EAC. Se você precisar alterar o nome de exibição do gateway IP de UM depois da sua criação, primeiro exclua o gateway IP de UM existente e depois crie outro com o nome apropriado. O nome do gateway IP de UM é necessário, mas é usado apenas para fins de exibição. Como sua organização pode usar vários gateways IP de UM, recomendamos que você use nomes significativos para eles. O comprimento máximo de um nome de gateway IP de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Endereço**   Você pode configurar um gateway IP da UM com um endereço IPv4 ou IPv6 ou um FQDN. Use essa caixa para especificar o endereço IP ou FQDN configurado no gateway VoIP, PBX IP ou PBX habilitado para SIP. Essa caixa aceita somente FQDNs válidos e formatados corretamente.
        
        Você pode digitar caracteres alfanuméricos. Há suporte para FQDNs, endereços IPv6 e endereços IPv4. Se você quiser usar TLS mútua entre um gateway de IP da UM e um plano de discagem funcionando no modo SIP seguro ou Seguro, você deverá configurar o gateway IP da UM com um FQDN. Você também deve configurá-lo para escutar na porta 5061 e verificar se gateways VoIP ou PBXs IP também foram configurados para escutar solicitações de TLS mútuas na porta 5061. Para configurar um gateway IP da UM, execute o seguinte comando no Shell: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Se você usar um FQDN, você também deve se certificar que configurou corretamente um registro de host DNS para o gateway VoIP, PBX IP ou PBX habilitado para SIP de modo que o nome do host seja resolvido corretamente para um endereço IP. Se você utilizar um FQDN em vez de um endereço IP, e a configuração DNS para o gateway IP de UM for alterada, será necessário desabilitar e, em seguida, habilitar o gateway IP de UM para garantir que as informações de configuração do gateway IP de UM sejam atualizadas corretamente.
    
      - **Plano de Discagem da UM**   Clique no botão **Procurar** para selecionar o plano de discagem da UM que deseja associar ao gateway IP da UM. Quando você seleciona um plano de discagem de UM para associar a um gateway IP de UM, um número coletivo padrão de UM é também criado e associado ao plano de discagem de UM selecionado. Se você não selecionar um plano de discagem de UM, deverá criar manualmente um grupo de busca de UM e depois associar esse grupo de busca de UM ao gateway IP de UM que você criou.

3.  Clique em **Salvar**.

Se for necessário, crie um gateway IP da UM executando o seguinte comando:

```powershell
New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"
```

Para configurar um gateway IP da UM usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **gateways IP da UM** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Gateway IP da UM**, clique em **Configurar**. Use as opções de configuração para exibir configurações de gateway IP da UM específicos e para habilitar ou desabilitar os recursos.

Para configurar um gateway IP da UM existente no Shell, executando o seguinte comando no Shell.

```powershell
Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false
```

## Etapa 9: Criar um grupo de busca de UM

Dependendo de sua implantação existente do Exchange 2010, talvez seja necessário criar novos grupos de busca da UM. Um grupo de busca de telefonia fornece uma maneira de distribuir chamadas telefônicas a partir de um único número para diversos ramais ou números de telefone. Na Unificação de Mensagens, um grupo de busca de UM é uma representação lógica de um grupo de busca de telefonia e vincula um gateway IP de UM a um plano de discagem de UM.

Você precisa ter pelo menos um grupo de busca de UM para cada grupo de busca de PBX IP ou PBX. Quando você concluir o procedimento a seguir, um grupo de busca de UM será criado por padrão. Se você tiver mais de um grupo de busca de PBX IP ou PBX, precisará criar grupos de busca de UM adicionais. Para saber mais sobre grupos de busca de UM, consulte [Grupos de busca de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups).

Se for necessário, crie um grupo de busca de UM usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem da UM**, em **Grupos de Busca de UM**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página do **Novo Grupo de Busca de UM**, insira as seguintes informações:
    
      - **Nome**   Use essa caixa para criar o nome de exibição do grupo de busca de UM. Um nome para o grupo de busca de UM é necessário e deve ser exclusivo, mas é usado apenas para fins de exibição no EAC e no Shell. Se você precisar alterar o nome de exibição do grupo de busca depois da sua criação, primeiro exclua o grupo de busca existente e depois crie outro grupo de busca com o nome apropriado. Se a sua organização usa vários grupos de busca, convém usar nomes significativos para eles. O comprimento máximo do nome do grupo de busca de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Gateway IP de UM**   Use esta caixa para selecionar um gateway IP da UM. Este campo mostra o nome do gateway IP da UM que será vinculado ao grupo de busca do UM. Para vincular um gateway IP da UM ao grupo de busca de UM, clique em **Procurar**.
    
      - **Identificador Piloto**   Use esta caixa para especificar uma cadeia de caracteres que identifique exclusivamente o identificador piloto configurado no PBX ou no PBX IP. É possível usar um número de ramal ou um URI (Uniform Resource Identifier) SIP nessa caixa. Caracteres alfanuméricos são aceitos nesta caixa. Para PBXs herdados, é usado um valor numérico com identificador piloto. No entanto, alguns PBXs IP e PBXs habilitados para SIP podem usar URIs SIP.

4.  Clique em **Salvar**.

Se for necessário, você pode criar um grupo de busca de UM executando o seguinte comando no Shell.

```powershell
New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway
```


> [!TIP]  
> Não é possível configurar ou alterar as configurações de um grupo de busca de UM. Se você quiser alterar as configurações de um grupo de busca de UM, é necessário excluí-lo e adicionar um novo grupo de busca de UM com as configurações corretas.



## Etapa 10: Criar ou configurar atendedores automáticos de UM

Dependendo de sua implantação existente do Exchange 2010, talvez seja necessário criar novos atendedores automáticos da UM. Você pode usar atendedores automáticos de UM para criar um sistema de menus de voz que permita aos chamadores externos e internos navegar pelo sistema de menus do atendedor automático de UM para localizar pessoas e fazer ou transferir chamadas para usuários ou departamentos da empresa. Para obter mais informações, consulte [Responder e rotear as chamadas de entrada automaticamente](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls).

Em implantações menores, você pode querer implantar a UM para que os chamadores possam deixar mensagens de caixa postal para os usuários. Nessas implantações, não é necessário criar um atendedor automático. Entretanto, na maioria dos casos, usar atendedores automáticos é muito útil para chamadores externos que ligarem para a sua organização.

Se for necessário, crie um atendedor automático da UM usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Selecione um plano de discagem de UM no qual você deseja adicionar o atendedor automático e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem da UM**, em **Atendedores automáticos da UM**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Novo Atendedor Automático da UM**, preencha os seguintes campos:
    
      - **Nome**   Use essa caixa para criar o nome de exibição do atendedor automático de UM. O nome do atendedor automático de UM é necessário e deve ser exclusivo. Porém, ele é usado apenas para fins de exibição no EAC e no Shell. Se você precisar alterar o nome de exibição do atendedor automático depois da sua criação, primeiro exclua o atendedor automático de UM existente e depois crie outro atendedor com o nome apropriado. Se a sua organização usa vários atendedores automáticos de UM, convém usar nomes significativos para eles. O tamanho máximo do nome do atendedor automático de UM é 64 caracteres e pode incluir espaços.
        
        Embora seja possível usar espaços ao dar um nome para um novo atendedor automático de UM, se você integrar a Unificação de Mensagens ao Lync Server, o nome do atendedor automático não poderá incluir espaços. Sendo assim, se você criar um atendedor automático com espaços no nome de exibição e estiver fazendo a integração com o Lync Server, primeiro exclua o atendedor automático e depois crie outro que não inclua espaços no nome de exibição.
    
      - **Criar este atendedor automático como habilitado**   Marque esta caixa de seleção para permitir que o atendedor automático atenda chamadas de entrada quando você concluir a criação do atendedor automático da UM. Por padrão, o novo atendedor automático é criado como desabilitado. Se você decidir criar o atendedor automático da UM como desabilitado, você pode usar o EAC ou o Shell para habilitar o atendedor automático após concluir sua criação.
    
      - **Configurar o atendedor automático para responder a comandos de voz**   Marque essa caixa de seleção para habilitar o atendedor automático de UM para voz. Se o atendedor automático for habilitado para fala, os chamadores poderão responder aos prompts do sistema ou a prompts personalizados usados pelo atendedor automático de UM usando entradas de discagem por tom ou voz. Por padrão, quando um atendedor automático é criado, não está habilitado para fala. Para que os chamadores usem um atendedor automático habilitado para fala em um idioma diferente do Inglês dos EUA (en-US), é necessário instalar o pacote de idioma da UM apropriado e configurar as propriedades do atendedor automático para usar esse idioma. O pacote de idioma da UM en-US é instalado por padrão quando você instala um servidor de Caixa de Correio do Exchange 2013.
    
      - **Números de acesso**   Digite os números de ramal ou de telefone que os chamadores utilizarão para acessar o atendedor automático. Digite um número de ramal ou telefone na caixa e clique em **Adicionar** para adicionar o número à lista. A quantidade de dígitos no número de ramal ou telefone fornecido não precisa corresponder à quantidade de dígitos para um número de ramal configurado no plano de discagem de UM associado. Isso acontece porque atendedores automáticos de UM podem fazer chamadas diretas.
        
        O número do ramal ou os números de acesso que você pode inserir são ilimitados. Entretanto, você pode criar um novo atendedor automático sem listar um número de ramal ou de telefone. Não é obrigatório fornecer um número de ramal ou telefone. É possível editar ou remover um número de ramal ou identificador piloto existente. Para editar um número de ramal ou telefone existente, clique no botão **Editar**. Para remover da lista um número de ramal ou telefone existente, clique no botão **Remover**.

4.  Clique em **Salvar**.

Se for necessário, você pode criar um atendedor automático de UM executando o seguinte comando no Shell.

```powershell
New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled
```

Se for necessário, você pode configurar um atendedor automático existente usando o EAC, da seguinte maneira:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **plano de discagem de UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM que você deseja exibir ou configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Use as opções de configuração para exibir configurações específicas do atendedor automático e para habilitar ou desabilitar os recursos.

Se for necessário, você pode configurar um atendedor automático de UM existente executando o seguinte comando no Shell.

```powershell
Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true
```

## Etapa 11: Criar ou configurar políticas de caixa de correio de UM

Dependendo de sua implantação existente do Exchange 2010, talvez seja necessário criar novas políticas de caixa de correio da UM ou configurar políticas de caixa de correio da UM existentes. As diretivas de caixa de correio de UM são necessárias quando os usuários são habilitados para a Unificação de Mensagens. A caixa de correio de cada usuário habilitado para UM deve estar vinculada a uma única diretiva de caixa de correio de UM. Depois de criar uma política de caixa de correio de UM, você vincula uma ou mais caixas de correio habilitadas para UM à política de caixa de correio de UM. Isso permite controlar as configurações de segurança de PIN, como o número mínimo de dígitos em um PIN ou o número máximo de tentativas de logon para os usuários habilitados para UM que estão vinculados à política de caixa de correio de UM. Para obter mais informações, consulte [políticas de caixa de correio de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies).

Se for necessário, crie uma política de caixa de correio de UM usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. No modo de exibição de lista, selecione o plano de discagem de UM que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, clique em **Adicionar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Nova Política de Caixa de Correio da UM** , na caixa **Nome**, digite o nome da política de caixa de correio da UM.
    

    > [!NOTE]  
    > Use essa caixa para especificar um nome exclusivo para a política de caixa de correio de UM. Esse é um nome de exibição que aparece no EAC. Se for necessário alterar o nome de exibição da diretiva de caixa de correio de UM depois que ela foi criada, primeiro você deverá excluir a diretiva de caixa de correio de UM existente e, em seguida, criar outra diretiva de caixa de correio de UM com o nome adequado. Não é possível excluir uma política de caixa de correio da UM se houver usuários habilitados para UM associados a ela. O nome da política de caixa de correio da UM é obrigatório, mas é usado apenas para fins de exibição. Como a sua organização pode utilizar várias políticas de caixa de correio de UM, recomendamos que você use nomes significativos para elas. O comprimento máximo para um nome de política de caixa de correio de UM é de 64 caracteres e pode conter espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  Clique em **Salvar**.
    

    > [!NOTE]  
    > Quando você salva a política de caixa de correio de UM, todas as configurações padrão, incluindo as políticas de PIN, os recursos de caixa postal e as configurações de Caixa Postal Protegida, são habilitadas. Se você quiser personalizar ou alterar quaisquer configurações padrão da política de caixa de correio de UM recém-criada, use o cmdlet <STRONG>Set-UMMailbox</STRONG> ou o EAC.



Se for necessário, você pode criar uma política de caixa de correio de UM executando o seguinte comando no Shell.

```powershell
New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan
```

Se for necessário, você pode configurar uma política de caixa de correio de UM existente usando o EAC:

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página do **plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja exibir ou configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Use as opções de configuração para exibir configurações específicas da política de caixa de correio de UM e para habilitar ou desabilitar os recursos.

Se for necessário, você pode configurar uma política de caixa de correio de UM existente executando o seguinte comando no Shell.

```powershell
Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."
```

## Etapa 12: Mover caixas de correio habilitadas para UM existentes para o Exchange 2013

Na Unificação de Mensagens do Exchange 2010, depois de você permitir que os usuários dentro da organização usem correio de voz, um conjunto padrão de propriedades de UM é aplicado ao usuário, para que ele possa usar os recursos de UM. Saiba mais em [Caixa postal para usuários](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users).

Durante o processo de atualização, haverá um período durante o qual você terá caixas de correio habilitadas para UM nos servidores de Caixa de Correio do Exchange 2010 e nos servidores de Caixa de Correio do Exchange 2013. No entanto, se você estiver movendo todos os usuários habilitados para UM para os servidores de Caixa de Correio do Exchange 2013, será necessário usar o EAC ou o cmdlet **New-MoveRequest** no Shell a partir de um servidor do Exchange 2013 a fim de reter todas as propriedades e configurações, incluindo o PIN do usuário.

Uma solicitação de movimentação é o processo de mover uma caixa de correio de um banco de dados de caixa de correio para outro. Uma solicitação de movimentação local é uma movimentação de caixa de correio que ocorre dentro de uma única floresta. Para obter mais informações sobre movimentos de caixas de correio, consulte:

  - [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\))

  - [Gerenciando solicitações de movimentação](https://go.microsoft.com/fwlink/p/?linkid=296352)

Para mover uma caixa de correio do Exchange 2010 para um servidor de Caixa de Correio do Exchange 2013 usando o EAC:

1.  No EAC, clique em **Destinatários** \> **Migração** e clique em **Adicionar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione o usuário que deseja mover, clique em **OK** e em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione que opções você deseja para a caixa de correio de arquivo e para a localização do banco de dados da caixa de correio e clique em **Nova**.

Para mover uma caixa de correio do Exchange 2010 para um servidor de Caixa de Correio do Exchange 2013 usando o Shell, execute o seguinte comando.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"
```

## Etapa 13: Habilitar novos usuários para UM ou definir configurações para um usuário habilitado para UM existente

Um usuário deve ter uma caixa de correio antes de poder ser habilitado para Unificação de Mensagens. Mas, por padrão, um usuário que tenha uma caixa de correio não está habilitado para UM. Depois que o usuário for habilitado para UM, você poderá gerenciar, modificar e configurar as propriedades de UM e de caixa postal do usuário. É possível habilitar um usuário para UM usando o EAC ou o Shell. Saiba mais em [Caixa postal para usuários](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users).

Quando você habilita um usuário para UM, é necessário definir pelo menos um número de extensão que a UM usará quando o correio de voz for enviado à caixa de correio do usuário e para permitir que o usuário use o Outlook Voice Access. Depois de habilitar o usuário para UM, você poderá adicionar números de ramal secundários à caixa de correio do usuário, modificar ou removê-los configurando o endereço de proxy da Unificação de Mensagens do Exchange (EUM) na caixa de correio do usuário, ou adicionar ou remover os ramais adicionais ou secundários do usuário no EAC. Para adicionar, modificar ou remover números de ramal, números E.164 ou endereços SIP, consulte [Procedimentos do usuário habilitado para email de voz](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

Para habilitar um usuário para Unificação de Mensagens usando o EAC:

1.  No EAC, clique em **Destinatários**.

2.  No modo de exibição de lista, selecione o usuário cuja caixa de correio deseja habilitar para a Unificação de Mensagens.

3.  No painel Detalhes, em **Telefone e Recursos de Voz**, clique em **Habilitar**.

4.  Na página **Habilitar caixa de correio de UM**, clique no botão **Procurar** ao lado de **Política de caixa de correio de UM**, localize a política de caixa de correio de UM, para atribuir o usuário a partir da lista, e clique em **OK**.

5.  Na página **Habilitar caixa de correio de UM**, preencha as seguintes caixas:
    
      - **Endereço SIP ou número E.164**   Insira o endereço SIP ou número E.164 para o usuário. Essas opções só estarão disponíveis se o usuário que você habilitar para Unificação de Mensagens estiver atribuído a uma política de caixa de correio de UM vinculada a um URI SIP ou a um plano de discagem E.164. A opção de adicionar um endereço SIP ou número E.164 para um usuário não estará disponível se o usuário estiver associado a um plano de discagem de ramal de telefone. Quando você atribui o usuário a uma política de caixa de correio da UM vinculada a um plano de discagem E.164 ou SIP URI, você deve ainda inserir também um número de ramal para o usuário. Esse número de ramal é usado quando o usuário acessa sua caixa de correio usando o Outlook Voice Access. A quantidade de dígitos configurada para esta caixa precisa ser igual à quantidade de dígitos configurada no plano de discagem URI SIP ou E.164.
    
      - **Número do ramal**   Digite o número do ramal do usuário que você está habilitando para UM.
        
        Você deve fornecer um número de ramal válido para o usuário, e esse número deve ter o número de dígitos especificado no plano de discagem. Você só pode digitar caracteres numéricos ou dígitos de 1 a 20. O número de ramal típico tem de 3 a 7 dígitos. O número de dígitos do ramal é definido no plano de discagem vinculado à política de caixa de correio de UM atribuída ao usuário.
    
      - Em **Configurações de PIN**, preencha o seguinte:
        
          - **Gerar PIN automaticamente**   Clique neste botão para gerar automaticamente um PIN para o usuário habilitado para UM a ser utilizado para acesso à caixa postal por meio do Outlook Voice Access. Essa é a configuração padrão. Quando você clicar nesse botão, um PIN será gerado automaticamente com base nas políticas de PIN configuradas na política de caixa de correio da UM atribuída ao usuário. Recomendamos o uso dessa configuração para ajudar a proteger o PIN do usuário. O PIN é enviado ao usuário na mensagem de boas-vindas que ele recebe após ter habilitado a UM. Por padrão, ele terá que alterar esse PIN quando entrar pela primeira vez em sua caixa de correio para verificar seu correio de voz.
        
          - **Digite um PIN**   Clique neste botão para manualmente especificar um PIN que o usuário utilizará para acessar o sistema de caixa postal. O PIN deve estar em conformidade com as configurações de política de PIN definidas na política de caixa de correio de UM associada a este usuário habilitado para UM. Por exemplo, se a política de caixa de correio da UM estiver configurada para aceitar somente PINs que contenham sete ou mais dígitos, o PIN digitado nessa caixa deverá ter pelo menos sete dígitos.
        
          - **Exigir que o usuário redefina seu PIN na primeira vez que entrar**   Marque esta caixa de seleção para forçar o usuário a redefinir seu PIN de caixa postal quando acessar o sistema de caixa postal a partir de um telefone usando o Outlook Voice Access pela primeira vez. Será solicitado que o usuário insira um PIN mais familiar a ele. É uma prática recomendada de segurança forçar usuários habilitados para UM a alterar seus PINs quando entram pela primeira vez para proteção contra acesso não autorizado a dados e Caixa de Entrada. Esta caixa de seleção é marcada por padrão.

6.  Na página **Habilitar caixa de correio de UM**, examine as configurações. Clique em **Concluir** para habilitar o usuário para a Unificação de Mensagens. Clique em **Voltar** para fazer alterações na configuração.

Para habilitar um usuário para Unificação de Mensagens usando o Shell, execute o seguinte comando.

```powershell
Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true
```

Se for necessário, você poderá configurar um usuário que foi habilitado para UM usando o EAC:

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na visualização de lista, selecione a caixa de correio para a qual você quer mudar a política de caixa de correio da UM.

3.  No painel de detalhes, em **Telefone e Características de Voz** \> **Unificação de Mensagens**, clique em **Ver detalhes**.

4.  Na página **Caixa de Correio de UM**, clique em **Configurações de caixa de correio de UM** para exibir ou alterar as propriedades de UM para um usuário habilitado para UM existente:
    
      - **Status do PIN**   Esta caixa somente para exibição mostra o status da caixa de correio do usuário. Por padrão, quando um usuário está habilitado para UM, o status do PIN é apresentado como **Não bloqueado**. Porém, se o usuário especificar várias vezes um PIN incorreto do Outlook Voice Access, o status será apresentado como **Bloqueado**.
    
      - **Política de caixa de correio de UM**   Esta caixa mostra o nome da política de caixa de correio de UM associada ao usuário habilitado para UM. Você pode clicar em **Procurar** para localizar e especificar a política de caixa de correio de UM a ser associada a essa caixa de correio de UM.
    
      - **Ramal pessoal do operador**   Use esta caixa para especificar o número do ramal de operador para o usuário. Por padrão, o número do ramal não está configurado. O tamanho do número do ramal pode ser de 1 a 20 caracteres. Isso permite que as chamadas de entrada para o usuário habilitado para UM sejam encaminhadas ao número de ramal especificado nessa caixa.
        
        Você pode configurar outros tipos de números de ramal d operador em planos de discagem e atendedores automáticos. Porém, esses ramais geralmente são destinados a recepcionistas ou operadores em toda a empresa. A configuração do ramal pessoal do operador poderá ser usada quando um assistente administrativo ou pessoal atender chamadas de entrada para um usuário específico.

5.  Na página **Caixa de Correio de UM**, em **Outras extensões**, você pode adicionar, alterar e exibir números de ramal para o usuário.
    
      - Para adicionar um número de ramal, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na página **Adicionar outra extensão**, use **Procurar** para selecionar o plano de discagem de UM e digite o número do ramal na caixa **Número do ramal**.
    
      - Para remover um número de ramal, selecione o número que deseja remover e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

6.  Se fizer alterações, clique em **Salvar**.

Se for necessário, você pode configurar um usuário que foi habilitado para UM no Shell executando o seguinte comando.

```powershell
Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail
```

## Etapa 14: Configurar seus gateways VoIP, IP PBXs e PBXs habilitados para SIP para enviar todas as chamadas de entrada aos servidores de Acesso para Cliente Exchange 2013

Quando os servidores de Acesso para Cliente e de Caixa de Correio do Exchange 2013 estiverem instalados, eles serão habilitados automaticamente, para que possam responder a chamadas de voz de entrada e de saída e rotear mensagens de caixa postal para os destinatários desejados. Quando você estiver instalando seus servidores de Acesso para Cliente e Caixa Postal do Exchange 2013 e implantando a Unificação de Mensagens, não precisará vincular ou adicionar servidores de Acesso para Cliente ou de Caixa de Correio do Exchange 2013 a planos de discagem de UM. Os servidores de Acesso para Cliente e Caixa de Correio do Exchange 2013 atendem a todas as chamadas de entrada e usam planos de discagem de UM para localizar usuários.

O servidor de Acesso para Cliente do Exchange 2013 é o ponto de entrada para quaisquer chamadas de entrada ou solicitações de protocolo SIP para Unificação de Mensagens. O serviço que lida com as solicitações SIP em um servidor de Acesso para Cliente do Exchange 2013 é o serviço Roteador de Chamadas de UM e é executado em cada servidor de Acesso para Cliente do Exchange 2013 em sua organização.

Ao atualizar para UM do Exchange 2013, você já deve ter instalado e configurado gateways VoIP simples ou múltiplos para se conectar aos PBXs em sua rede telefônica ou instalado e configurado PBXs habilitados para SIP ou PBXs IP.

A última etapa no processo de atualização para UM do Exchange 2013 é configurar os gateways VoIP, PBXs IP ou PBXs habilitados para SIP para enviar chamadas de entrada—incluindo chamadores que desejam deixar um correio de voz para um usuário, chamadas de usuários habilitados para UM para o Outlook Voice Access e chamadas de chamadores que discam para um atendedor automático de UM—para seus servidores de Acesso para Cliente do Exchange 2013. Todas essas chamadas são recebidas primeiro pelo seu gateway VoIP, PBX IP ou PBX habilitado para SIP e encaminhadas para os servidores de Acesso para Cliente do Exchange 2013 em sua organização do Exchange 2013. Para obter mais informações, consulte os seguintes recursos:

  -  [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md)

  -  [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

  -  [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)

## Etapa 15: Desabilitar o atendimento de chamadas em um servidor de Unificação de Mensagens do Exchange 2010

É possível desativar o atendimento de chamadas desativando a UM em um servidor de Unificação de Mensagens do Exchange 2010 ou removendo o servidor de UM de um plano de discagem. Quando você desabilita a UM, impede que o servidor de UM atenda às chamadas de entrada. Você pode optar por desconectar todas as chamadas imediatamente ou aguardar até que as chamadas existentes sejam processadas antes de desabilitar o servidor de Unificação de Mensagens. Convém desabilitar o atendimento de chamada antes de remover o servidor de um plano de discagem de modo que ele termine de processar quaisquer chamadas de entrada.

Para desabilitar a Unificação de Mensagens em um servidor de UM do Exchange 2010 usando o Console de Gerenciamento do Exchange:

1.  Na árvore do console do EMC, navegue até **Configuração do Servidor** \> **Unificação de Mensagens**.

2.  No painel de resultados, selecione o servidor de Unificação de Mensagens a ser desabilitado.

3.  No painel de ação, clique em um dos seguintes:
    
      - Ao selecionar a opção **Desabilitar Imediatamente**, o servidor de Unificação de Mensagens desconecta todas as chamadas conectadas ao servidor de Unificação de Mensagens.
    
      - Ao selecionar a opção **Desabilitar depois de concluir chamadas**, o servidor de Unificação de Mensagens não aceitará novas chamadas e não será desabilitado até que todas as chamadas tenham sido processadas.

4.  Na caixa de diálogo de confirmação, clique em **Sim** para continuar.

Para desabilitar a Unificação de Mensagens em um servidor de UM do Exchange 2010 usando o Shell, execute o seguinte comando:

```powershell
Disable-UMServer -Identity MyUMServer -Immediate $true
```


> [!TIP]  
> É possível usar o cmdlet <STRONG>Disable-UMServer</STRONG> de um servidor de UM do Exchange 2010 ou o cmdlet <STRONG>Disable-UMService</STRONG> de um servidor de Caixa de Correio do Exchange 2013 para desabilitar o atendimento de chamada.



## Etapa 16: Remova um servidor de Unificação de Mensagem do Exchange 2010 de um plano de discagem

Para processar chamadas, um servidor de UM do Exchange 2010 deve ser adicionado a pelo menos um plano de discagem de UM. Um servidor de UM pode ser adicionado a vários planos de discagem de UM. Você pode remover um servidor de UM do Exchange 2010 de um plano de discagem da UM. Quando você remove um servidor de UM de um plano de discagem da UM, o servidor de UM não responde mais a chamadas nem processa chamadas de UM para usuários habilitados para UM.

Para remover um servidor de UM do Exchange 2010 de um plano de discagem usando o Console de Gerenciamento do Exchange:

1.  Na árvore do console do EMC, navegue até **Configuração do Servidor** \> **Unificação de Mensagens**.

2.  No painel de resultados, selecione o servidor de Unificação de Mensagens.

3.  No painel de ações, clique em **Propriedades**.

4.  Na guia **Configurações do UM**, na seção **Planos de Discagem Associados**, clique em **Remover**.

5.  Na caixa de diálogo de confirmação, clique em **Sim** para confirmar a exclusão do servidor Exchange 2010 de UM plano de discagem.

6.  Clique em **OK** para fechar a janela de propriedades.

Para remover um servidor de UM do Exchange 2010 de um plano de discagem usando o Shell, execute o seguinte comando.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMServer -id MyUMServer
$s.dialplans-=$dp.identity
Set-UMServer -id MyUMServer -dialplans:$s.dialplans
```

Neste exemplo, existem três planos de discagem de URI SIP: SipDP1, SipDP2 e SipDP3. Este exemplo remove o servidor de UM chamado `MyUMServer` do plano de discagem SipDP3.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2
```

Neste exemplo, existem dois planos de discagem de URI SIP: SipDP1 e SipDP2. Este exemplo remove o servidor de UM chamado `MyUMServer` do plano de discagem SipDP2.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1
```


> [!TIP]  
> É possível usar o cmdlet <STRONG>Set-UMServer</STRONG> no Shell em um servidor de Unificação de Mensagens do Exchange 2010 ou o cmdlet <STRONG>Set-UMService</STRONG> em um servidor de Caixa de Correio do Exchange 2013 para remover um servidor de UM do Exchange 2010 de um ou vários planos de discagem. Por exemplo, para remover um servidor de UM de todos os planos de discagem, execute o seguinte comando: <CODE>Set-UMServer -identity MyUMServer -DialPlans $null</CODE>



## Como saber se funcionou?

Depois de configurar a Unificação de Mensagens, verifique o seguinte para garantir que esteja funcionando corretamente:

  - Um usuário que você habilitou para caixa postal pode entrar no Outlook Web App ou no Outlook e ver uma Mensagem de Boas-vindas para Unificação de Mensagens.

  - Os usuários da UM podem receber mensagens de voz.

  - Os usuários da UM podem ligar para um número do Outlook Voice Access e ouvir emails, itens de calendário e caixa postal.

  - A UM está roteando chamadas de fora de sua organização, e você pode fazer uma chamada.