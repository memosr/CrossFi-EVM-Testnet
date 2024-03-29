<h1 align="center">CrossFi Testnet Setup - CrossFi Testnet Kurulumu
  
<br/><br>
![lava-network-testnet-rehberi](https://pbs.twimg.com/profile_banners/1681767569823334401/1698851466/1500x500)

## Sistem gereksinimleri:
NODE TİPİ - NODE TYPE | CPU     | RAM      | SSD     |
| ------------- | ------------- | ------------- | -------- |
| CrossFi | 4          | 16         | 300  |


## 1) Kurulum - Setup
```
sudo apt update && sudo apt upgrade -y
```

### From snapshot (fast) 

> Download binary - İkiliyi indir

```
wget https://github.com/crossfichain/crossfi-node/releases/download/v0.3.0-prebuild3/crossfi-node_0.3.0-prebuild3_linux_amd64.tar.gz && tar -xf crossfi-node_0.3.0-prebuild3_linux_amd64.tar.gz
```
> Download configs - Yapılandırmaları indirin

```
git clone https://github.com/crossfichain/testnet.git
```

> Start node - Node Başlat

```
./bin/crossfid start --home ./testnet
```

> Create Wallet - Cüzdan Oluştur

```
./bin/crossfid --home ./testnet keys add my_validator
```

###  Adding the wallet you created earlier- Daha önceden oluşturduğunuz cüzdanı eklemek

> Here, we will transfer the wallet you requested a token from when applying or by mail into the node - Burada, Başvuru yaparken veya maille token istediğiniz cüzdanı, node içine aktaracağız.

> Enter the words you received when opening the wallet - Cüzdanı açarken aldığınız kelimeleri girin

> It will ask you to set a password, set a password and that's it - Sizden şifre belirlemenizi isteyecek şifre belirleyin bu kadar

```
crossfid keys add $WALLET --recover
```

### Senkronizasyon Kontrolü

> When you get `false` output after the command, you can proceed with the Validator installation - Komut sonrasında `false` çıktısı aldığınızda Validator kurulumuna geçebilirsiniz

```
crossfid status 2>&1 | jq .SyncInfo
```

## 2) Validator Çalıştırma

> Write your Validator name in quotes where `moniker` is written - `moniker` yazan yere tırnaklar içinde Validator isminizi yazıyoruz

> You can write anything you want in quotes where it says `details` - `details` yazan yere tırnaklar içinde istediğiniz bir şey yazabilirsiniz

> You can add your twitter or github link where it says `website` - `website` yazan yere twitter yada github linkinizi ekleyebilirsiniz


```
crossfid tx staking create-validator \
--amount 9000000000000000000000mpx \
--from $WALLET \
--commission-rate 0.1 \
--commission-max-rate 0.2 \
--commission-max-change-rate 0.01 \
--min-self-delegation 1 \
--pubkey $(crossfid tendermint show-validator) \
--moniker "" \
--website "" \
--details "memosr Community" \
--chain-id crossfi-evm-testnet-1 \
--gas auto --gas-adjustment 1.5 --gas-prices 10000000000000mpx \
-y
```


## 3) Validator Bilgilerini Güncelleme

> You can update the information here to change your Validator Name and other changes - Buradaki bilgileri güncelleyerek Validator Adınızı ve diğer değişiklikleri yapabilirsiniz

```
crossfid tx staking edit-validator \
--new-moniker "YOUR_MONIKER_NAME" \
--identity "YOUR_KEYBASE_ID" \
--details "YOUR_DETAILS" \
--website "YOUR_WEBSITE_URL" \
--chain-id crossfi-evm-testnet-1 \
--commission-max-change-rate 0.01 \
--from cüzdanismi \
--gas auto --gas-adjustment 1.5 --gas-prices 10000000000000mpx \
-y
```

