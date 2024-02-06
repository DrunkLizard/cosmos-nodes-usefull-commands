# cosmos-nodes-usefull-commands
hey hey

Servis Yönetimi
Logları Kontrol Et: journalctl -fu ()d -o cat

Servisi Başlat: systemctl start ()d

Servisi Durdur: systemctl stop ()d

Servisi Yeniden Başlat: systemctl restart ()d

Node Bilgileri
Senkronizasyon Bilgisi: ()d status 2>&1 | jq .SyncInfo

Validator Bilgisi: ()d status 2>&1 | jq .ValidatorInfo

Node Bilgisi: ()d status 2>&1 | jq .NodeInfo

Node ID Göser: ()d tendermint show-node-id

Cüzdan İşlemleri
Cüzdanları Listele: ()d keys list
 Cüzdan ekle: ()d keys add <wallet-ismi>
Mnemonic kullanarak cüzdanı kurtar: ()d keys add $WALLET --recover

Cüzdan Silme: ()d keys delete $WALLET

Cüzdan Bakiyesi Sorgulama: ()d query bank balances $WALLET_ADDRESS

Cüzdandan Cüzdana Bakiye Transferi: ()d tx bank send $WALLET_ADDRESS <TO_WALLET_ADDRESS> 10000000u()

Oylama:  ()d tx gov vote 1 yes --from $WALLET --chain-id=$CHAIN_ID

Stake, Delegasyon ve Ödüller
Delegate İşlemi: ()d tx staking delegate $VALOPER_ADDRESS 10000000u() --from=$WALLET --chain-id=$CHAIN_ID --gas=auto

Payını doğrulayıcıdan başka bir doğrulayıcıya yeniden devretme: ()d tx staking redelegate <srcValidatorAddress> <destValidatorAddress> 10000000u() --from=$WALLET --chain-id=$CHAIN_ID --gas=auto

Tüm ödülleri çek: ()d tx distribution withdraw-all-rewards --from=$WALLET --chain-id=$CHAIN_ID --gas=auto

Komisyon ile ödülleri geri çekin: ()d tx distribution withdraw-rewards $VALOPER_ADDRESS --from=$WALLET --commission --chain-id=$CHAIN_ID

Doğrulayıcı Yönetimi
Validatör İsmini Değiştir: 
()d tx staking edit-validator \
--moniker=NEWNODENAME \
--chain-id=$CHAIN_ID \
--from=$WALLET

Hapisten Kurtul(Unjail): 
()d tx slashing unjail \
	--broadcast-mode=block \
	--from=$WALLET \
	--chain-id=$CHAIN_ID \
	--gas=auto

Node Tamamen Silmek: 

sudo systemctl stop ()d && \
sudo systemctl disable ()d && \
rm /etc/systemd/system/()d.service && \
sudo systemctl daemon-reload && \
cd $HOME && \
rm -rf .() ()-chain && \
rm -rf $(which ()d)
