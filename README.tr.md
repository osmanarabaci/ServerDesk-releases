<div align="center">

<img src="docs/images/icon.png" width="128" height="128" alt="ServerDesk ikonu">

# ServerDesk

**Yönettiğin tüm sunucular için tek masa.**<br>
SSH, RDP, SFTP, veritabanları, Docker ve Kubernetes; macOS ve Windows için tek bir yerel uygulamada. Sırlar şifreli kasada, Production'da emniyet kemeri takılı.

[![Son sürüm](https://img.shields.io/github/v/release/osmanarabaci/ServerDesk-releases?label=s%C3%BCr%C3%BCm&color=0A84FF)](https://github.com/osmanarabaci/ServerDesk-releases/releases/latest)
![Platformlar](https://img.shields.io/badge/platformlar-macOS%20%C2%B7%20Windows-0A84FF)
![Otomatik güncelleme](https://img.shields.io/badge/g%C3%BCncelleme-otomatik-34C759)
[![Lisans: MIT](https://img.shields.io/badge/lisans-MIT-34C759)](LICENSE)

<br>

[![macOS için indir](https://img.shields.io/badge/macOS%20i%C3%A7in%20indir-Apple%20Silicon-1D1D1F?style=for-the-badge&logo=apple&logoColor=white)](https://github.com/osmanarabaci/ServerDesk-releases/releases/latest/download/ServerDesk-osx-arm64-Setup.pkg)
&nbsp;
[![Windows için indir](https://img.shields.io/badge/Windows%20i%C3%A7in%20indir-x64-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/osmanarabaci/ServerDesk-releases/releases/latest/download/ServerDesk-win-x64-Setup.exe)

[Özellikler](#özellikler) · [Güvenlik](#güvenlik) · [Kurulum](#kurulum) · [Tüm sürümler](https://github.com/osmanarabaci/ServerDesk-releases/releases) · [English](README.md)

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/images/servers-dark.png">
  <img src="docs/images/servers-light.png" alt="Sağlık değerleriyle ServerDesk sunucu envanteri" width="900">
</picture>

</div>

## Özellikler

| | |
|---|---|
| **Envanter** | Yüzlerce sunucu; gruplar, etiketler, favoriler, ortamlar (Production, Staging, Development, Test) ve anında arama. `~/.ssh/config` ya da CSV'den içe aktar, CSV'ye dışa aktar. |
| **Terminal** | Sekmelerde SSH oturumları, tam xterm terminali, bölünmüş görünüm ve kaydedip geri yükleyebileceğin workspace'ler. |
| **Uzak Masaüstü** | Paketle gelen FreeRDP ile yerleşik RDP oturumları. |
| **SFTP** | Sürükle-bırak destekli iki panelli dosya aktarımı. Her aktarım SHA-256 ve boyutla doğrulanır, çakışmalarda sorulur. |
| **Komut Merkezi** | Kayıtlı ve şablonlu komutları çalıştır, geçmişi tut, kritik komutları çalışmadan önce yakala. |
| **Sağlık** | SSH (Linux) ve WinRM (Windows) üzerinden ajansız CPU, RAM ve disk ölçümü; 24 saatlik geçmiş. |
| **Veritabanları** | SQL Server, PostgreSQL ve MySQL; doğrudan ya da SSH tüneliyle. Varsayılan olarak salt-okunur. |
| **Docker** | Herhangi bir SSH sunucusundaki container'lar: loglar, ayrıntılar, başlat, durdur, yeniden başlat, sil ve içeride kabuk. |
| **Kubernetes** | kubeconfig'deki context'ler: pod'lar, loglar, rollout restart, ölçekleme ve pod terminali. |
| **Hızlı kullanım** | Son bağlantılar, her sunucuda sağ tık menüsü, sekmeler, arama ve sunucu listesi için klavye kısayolları (<kbd>⌘/</kbd> hepsini gösterir). |

<table>
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="docs/images/dashboard-dark.png">
        <img src="docs/images/dashboard-light.png" alt="İlgi bekleyen sunucuları listeleyen pano">
      </picture>
      <p align="center"><b>Pano</b>: ilgi bekleyenler tek bakışta</p>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="docs/images/critical-dark.png">
        <img src="docs/images/critical-light.png" alt="Kritik komuttan önce sunucu adını soran onay">
      </picture>
      <p align="center"><b>Emniyet kemeri</b>: Production'da kritik komut için sunucu adını yaz</p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="docs/images/docker-dark.png">
        <img src="docs/images/docker-light.png" alt="Production sunucusundaki Docker container'ları ve logları">
      </picture>
      <p align="center"><b>Docker</b> SSH üzerinden, sunucuda ajan yok</p>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="docs/images/kubernetes-dark.png">
        <img src="docs/images/kubernetes-light.png" alt="Durum, yeniden başlatma ve loglarla Kubernetes pod'ları">
      </picture>
      <p align="center"><b>Kubernetes</b> doğrudan kubeconfig'den</p>
    </td>
  </tr>
</table>

## Güvenlik

- **Şifreli kasa.** Parolalar, SSH anahtarları ve passphrase'ler tek bir taşınabilir dosyada durur; Argon2id ile türetilen anahtar altında AES-256-GCM ile şifrelenir. Aynı kasa macOS'te ve Windows'ta açılır.
- **Kendiliğinden kilitlenir.** <kbd>⌘L</kbd> / <kbd>Ctrl+L</kbd> kasayı kilitler; bir süre işlem yapılmayınca, Mac uykuya geçince ya da ekran kilitlenince de kilitlenir. Kasa kilitliyken sır gerektiren hiçbir şey çalışmaz.
- **İlk kullanımda güven.** SSH host anahtarları, RDP sertifikaları ve veritabanı sertifikaları bir kez gösterilir ve kasaya sabitlenir. Değişen bir anahtar bağlantıyı durdurur ve nedenini söyler.
- **Production emniyet kemeri.** Kritik komutlar (`rm -rf`, `shutdown`, `systemctl restart`, `DROP`, …) ve Production sunucu, container ve cluster'lardaki yıkıcı işlemler önce sunucu adını yazmanı ister.
- **Varsayılan salt-okunur.** Veritabanı oturumları salt-okunur başlar; sen kapatana kadar değişiklikler geri alınır.

> [!NOTE]
> Bunlar uyarı ve hata azaltma katmanlarıdır; sunucuların kendi yetki denetiminin yerine geçmez.

## Kurulum

| Platform | Paket |
|---|---|
| macOS (Apple Silicon) | [`ServerDesk-osx-arm64-Setup.pkg`](https://github.com/osmanarabaci/ServerDesk-releases/releases/latest/download/ServerDesk-osx-arm64-Setup.pkg): `~/Applications` içine kurulur, yönetici parolası gerekmez |
| Windows 10/11 (x64) | [`ServerDesk-win-x64-Setup.exe`](https://github.com/osmanarabaci/ServerDesk-releases/releases/latest/download/ServerDesk-win-x64-Setup.exe) |

Taşınabilir `.zip` sürümleri her [sürüm sayfasında](https://github.com/osmanarabaci/ServerDesk-releases/releases/latest). Kurulduktan sonra ServerDesk bu sayfayı denetler ve kendini arka planda günceller; güncellemeler küçük delta paketlerdir.

> [!IMPORTANT]
> Paketler henüz kod imzalı değil. macOS'te `.pkg`'yi bir kez aç ve **Bitti**'yi seç (*Çöp Sepetine Taşı*'yı değil); ardından **Sistem Ayarları → Gizlilik ve Güvenlik**'te engellenen paketin yanındaki **Yine de Aç**'a bas. Windows'ta SmartScreen'de **Ek bilgi → Yine de çalıştır**'ı seç.

## Lisans

ServerDesk [MIT Lisansı](LICENSE) ile yayımlanır. Kurulum paketleri kendi lisanslarıyla gelen üçüncü taraf bileşenler içerir; liste her paketin içindeki `THIRD-PARTY-NOTICES` dosyasındadır. macOS paketi FreeRDP'nin Homebrew bağımlılıklarını içerir; bunların bir kısmı (ffmpeg, x264, x265) GPL lisanslıdır.

<sub>Ekran görüntülerindeki veriler uydurmadır.</sub>
