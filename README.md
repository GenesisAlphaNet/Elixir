# Elixir

### Donanım: En az 8 GB RAM ve 100 GB Disk gereklidir.
### İşletim sistemi : Ubuntu
### Servis Sağlayıcısı olarak Hetzner önerilir.
### Yeni bir metamask cüzdanı açmanız önerilir.

 

## Docker kurulum: "bütün kodlar tek seferde"

    sudo apt-get update
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

## Docker kurulum devam:

    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

## Validator config dosyasını indirme 
    wget https://files.elixir.finance/validator.env
    nano validator.env

### Açılan düzenleme ekranında ("tırnaklar olmadan")

##### STRATEGY_EXECUTOR_DISPLAY_NAME="validator isminiz"
##### STRATEGY_EXECUTOR_BENEFICIARY= "puanın gelmesini istediğiniz cüzdanın adresi"
##### SIGNER_PRIVATE_KEY= "oluşturduğunuz cüzdanın private keyi"

## Örneğin
##### STRATEGY_EXECUTOR_DISPLAY_NAME=GenesisAlpha
##### STRATEGY_EXECUTOR_BENEFICIARY=0xgenesis
##### SIGNER_PRIVATE_KEY=private_key_0

####  Şeklinde düzenleyip ctrl + o , enter , ctrl + x ile çıkabilirsiniz.

## Screen kurulumu:
    
    apt install screen
    screen -R elixir

## Elixir reposunu çekme:
    docker pull elixirprotocol/validator:v3

## Validatoru çalıştırma :
    docker run -d \
      --env-file validator.env \
      --name elixir \
      --restart unless-stopped \
      elixirprotocol/validator:v3

#### Validator şuan ayakta.

#### Şimdi [Elixir](https://testnet-3.elixir.xyz/)'in adresine gidip mock mint edip state edip kendi validatörümüze delegete edelim.

####  Aşağıdaki adımları izleyerek kendi validator'ünüze stake edebilirsiniz. (4. adımda açılan kutucuğa kendi validator public key'inizi girin.)
![elixir](https://github.com/user-attachments/assets/2f1b0f76-c09d-4c05-97a9-49b23faf0e1e)


