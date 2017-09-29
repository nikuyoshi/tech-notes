+++
title = "Raspberry Pi"
+++

## Getting Started

[公式ページに載っていた動画](https://vimeo.com/90518800)通りに作業を進めた。 普通のLinuxのインストールなので特に難しいことはない。

1. SDカードフォーマッターでフォーマットする
   * https://www.sdcard.org/downloads/formatter_4/
2. NOOBSをダウンロード, unzipして中身をSDカードにぶちこむ
3. キーボード、マウス、ディスプレイに接続してインストールを進める

## OSインストール後

### 本体の設定

`sudo raspi-config` でRaspberry Piの本体の設定を変更した。

* Localisation Options ... 英語/日本語両方とも使えるように設定
* Update ... Raspberry Pi自体のアップデート
* Interfacing Options ... SSH/VNCサーバーの起動

`passwd` でpiユーザーのパスワード変更も忘れずに。

### ソフトウェア設定

インストールしたソフトウェアは以下の通り

```bash
sudo apt-get install vim
```

### WiFi設定

[ステルスSSIDを登録する方法](https://vimeo.com/90518800) を参考にセットアップした。 ステルス化してなければこの手順はスキップできる。

#### 実際叩いたコマンド

`vim` で設定変更しているファイルの詳細設定については次項に記載してある

```bash
pi@raspberrypi:~ $ cd /etc/network/
pi@raspberrypi:/etc/network $ ls -la
pi@raspberrypi:/etc/network $ sudo cp -p interfaces interfaces-2017-07-09
pi@raspberrypi:/etc/network $ vim interfaces
pi@raspberrypi:/etc/network $ cd /etc/wpa_supplicant
pi@raspberrypi:/etc/wpa_supplicant $ sudo cp -p wpa_supplicant.conf wpa_supplicant.conf-2017-07-09
pi@raspberrypi:/etc/wpa_supplicant $ ls -la
pi@raspberrypi:/etc/wpa_supplicant $ sudo vim wpa_supplicant.conf
pi@raspberrypi:/etc/wpa_supplicant $ sudo reboot
```

#### 設定ファイルの詳細

##### `/etc/network/interfaces`

```bash
# interfaces(5) file used by ifup(8) and ifdown(8)

# Please note that this file is written to be used with dhcpcd
# For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'

# Include files from /etc/network/interfaces.d:
source-directory /etc/network/interfaces.d

auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```

##### `/etc/wpa_supplicant/wpa_supplicant.conf`

以下のファイルを見て分かる通り、複数ある場合はnetworkの項目を追加していけばよい。

```bash
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
	ssid="put_your_hidden_ssid_here"
	scan_ssid=1
	psk="put_your_password_for_network_here"
	proto=RSN
	key_mgmt=WPA-PSK
	pairwise=CCMP
	group=CCMP
	auth_alg=OPEN
	priority=1
	id_str="raspi"
}
network={
	ssid="put_your_ssid_here"
	psk="put_your_password_for_network_here"
}
```

