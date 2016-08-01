# Powershell ile Yerel Grup İlkeleri Nasıl Yönetilir
## Yerel Grup İlkesi Objelerini Powershell kullanarak yönetme
Sadece Windows'un Grup İlkeleri Cmdlet'leri kullanılarak Yerel Grup İlkelerini yönetmek bir hayli zor diyebiliriz.
Bu konuda işimizi en çok kolaylaştıran çalışmalardan biri [Dave Wyatt](https://twitter.com/msh_dave)'ın [PolicyFileEditor](https://github.com/dlwyatt/PolicyFileEditor) adlı modülü. Bu modül ile Yerel Grup İlkeleri düzenlenebilir ve hazır ilke şablonlarından ilkeler alınabilir. Bu kılavuzun referansı [link](http://brandonpadgett.com/powershell/Local-gpo-powershell/)te bulunmaktadır.

*PolicyFileEditor*'ü kullanmak için öncelikle modifiye edeceğimiz ilkelerin dizinini belirtmemiz gerekiyor. Yerel grup ilkeleri için bu linkler aşağıdaki gibidir:

```powershell
$MachineDir = "$env:windir\system32\GroupPolicy\Machine\registry.pol"
$UserDir = "$env:windir\system32\GroupPolicy\User\registry.pol"
```

*Set-PolicyFileEntry* komutu kullanılarak bir ilke düzenlenebilir. Bu komutun çalışması için ilgili ilke dosyasının dizini verilmelidir. Ayrıca bu komut *-Key* değerini ister. Bu değer bizim değiştireceğimiz *Registry*'nin dizinidir. Daha sonra ilgili ilkenin adı, girilecek değer ve bu değerin tipi yazılır. Bir örnek üzerinden bu komut daha iyi anlaşılabilir:

```powershell
$RegPath = 'Software\Policies\Microsoft\Windows\Control Panel\Desktop'
$RegName = 'ScreenSaverIsSecure'
$RegData = '1'
$RegType = 'String'

Set-PolicyFileEntry -Path $UserDir -Key $RegPath -ValueName $RegName -Data $RegData -Type $RegType
```

Bu modülü tek bir *Registry* değeri için kullanmayı öğrendik. Tüm registry değerlerini ise *Get-PolicyFileEntry* komutunu *-All* parametresi ile kullanarak elde edebiliriz. Sonrasında bu değerleri *Export-Clixml* komutu ile dışa aktarabiliriz. Böylece bu dışa aktardığımız xml üzerinden ilkeleri düzenleyebilir, sonrasında da *Import-Clixml* ile düzenlediğimiz xml'i içe aktararabiliriz.

*Import-Clixml* ile xml'i içe aktarma ve ilkelerimizi buna göre güncelleme ile ilgili örnek bir kod aşağıdadır:

```powershell
Import-Module -name "PolicyFileEditor"
$UserDir = "$env:windir\system32\GroupPolicy\User\registry.pol"
$UserPols = Import-Clixml -Path 'C:\UserPol.xml'

foreach ($UserPol in $UserPols)
{
    $UserPol | Set-PolicyFileEntry -Path $UserDir
}
```





