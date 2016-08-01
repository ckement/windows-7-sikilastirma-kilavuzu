## Windows 7 Sıkılaştırma

Bu projede windows 7 sıkılaştırma adımları anlatılacaktır.

Sıkılaştırma adımları bu repository'nin Wiki kısmında anlatılmaktadır. Windows 7'nin sıkılaştırma adımları çoğunlukla Yerel Grup İlkesi Düzenleyicisi aracılığıyla (gpedit.msc) yapılmaktadır.

Code kısmında da Powershell ile bu sıkılaştırma adımlarının yapılıp yapılmadığıyla ilgili bazı script'ler mevcuttur. Bu scriptlerin çalışması için RSAT araçlarının yüklü olması gerekmektedir (http://www.microsoft.com/download/en/details.aspx?id=7887). Bu konu ile ilgili daha ayrıntılı bilgi için: (http://newdelhipowershellusergroup.blogspot.nl/2012/07/enable-group-policy-powershell-module.html)

Windows'un Yerel Grup İlkeleri ile ilgili powershell "cmdlet"leri kullanılarak ilgili konfigürasyonların yapılıp yapılmadığını kontrol eden bir script yazılamamıştır. Bu işlevi görmese de powershell ile Yerel Grup İlkelerini yöneten bir scripting yöntemi anlatılmıştır.

Ayrıca, bilgisayarda ilk defa bir powershell scripti çalıştırılıyorsa, öncelikle terminal (cmd.exe) yönetici olarak çalıştırılır. Ardından: "powershell set-executionpolicy remotesigned" komutu girilir. Aksi takdirde scriptler güvenlik gereği bu bilgisayar tarafından çalıştırılmayacaktır.

