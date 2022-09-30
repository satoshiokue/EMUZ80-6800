# EMUZ80-6800

![MEZ6800](https://github.com/satoshiokue/EMUZ80-6800/blob/main/imgs/IMG_6800_proto.jpeg)  
6800 Single-Board Computer

電脳伝説さん(@vintagechips)のEMUZ80の信号を組み替え、MC68A00Pを動作させることができます。  
アドレスマップをSBC6800に準じることで同データパックのMikbugおよびVTLの操作を体験する目的で作成しました。  

SBC6800ルーズキット  
https://vintagechips.wordpress.com/2017/12/05/sbc6800ルーズキット/

「モトローラ6800伝説」を手元に用意することを強く推奨します。  
https://www.amazon.co.jp/dp/4899774729

MC68A00PとPIC18F47Q83の組み合わせで動作確認しています。

動作確認済みMPU  
MC68A00P  
EF6800P  

このソースコードはGazelleさんのEMUZ80用main_cpz.cを元に改変してGPLライセンスに基づいて公開するものです。

https://drive.google.com/drive/folders/1NaIIpzsUY3lptekcrJjwyvWTBNHIjUf1

## メザニンボード
https://github.com/satoshiokue/MEZ6800

## 回路図
https://github.com/satoshiokue/MEZ6800/blob/main/MEZ6800.pdf

## ファームウェア

EMUZ80で配布されているフォルダemuz80.X下のmain.cと置き換えて使用してください。
* emuz80_6800.c ソフトクロック

emuz80_6800.cはメモリアクセス・通信I/O処理の開始および完了でクロック信号を反転させてバスにアクセスします。  
PICはクロック信号のデューティー比を変化させながらMC68A00を動作させます。

## アドレスマップ
```
RAM   0x0000 - 0x1FFF
UART  0x8018   Control REGISTER
      0x8019   Data REGISTER
ROM   0xE000 - 0xFFFF
```
SBC6800に準じます

## 6800プログラムの格納
インテルHEXデータを配列データ化して配列rom[]に格納するとMC68A00で実行できます。インテルHEXデータを手作業で変換するのもいいかもしれません。

テキスト変換例
```
hex2bin -p 00 MIKBUG.HEX
xxd -i -c16 MIKBUG.bin > MIKBUG.txt
```

RAMにロードするデータも同様にモトローラSフォーマットを配列データ化して配列ram_data[]に格納することでEMUZ80がリセットされるとRAM領域にデータを設定してMC68A00を起動します。  
ファイルサイズが大きいBASICのロード時間を回避できます。

使用ツール例[E3V3A / hex2bin]  
https://github.com/E3V3A/hex2bin

## 謝辞
思い入れのあるCPUを動かすことのできるシンプルで美しいEMUZ80を開発された電脳伝説さんに感謝いたします。

そしてEMUZ80の世界を発展させている開発者の皆さんから刺激を受けて6800に挑戦しています。

## 参考）EMUZ80
EUMZ80はZ80CPUとPIC18F47Q43のDIP40ピンIC2つで構成されるシンプルなコンピュータです。

![EMUZ80](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_Z80.jpeg)

電脳伝説 - EMUZ80が完成  
https://vintagechips.wordpress.com/2022/03/05/emuz80_reference  
EMUZ80専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-051.html

## 参考）phemu6809
comonekoさん(@comoneko)さんがEMUZ80にMC6809を搭載できるようにする変換基板とファームウェアphemu6809を発表されました。

![phemu6809](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_6809.jpeg)

https://github.com/comoneko-nyaa/phemu6809conversionPCB  
phemu6809専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-056.html
