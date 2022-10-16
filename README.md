# cosmos-nodes-usefull-commands
hey hey

Servis Yönetimi
Logları Kontrol Et:journalctl -fu seid -o cat

Servisi Başlat:systemctl start seid

Servisi Durdur:systemctl stop seid

Servisi Yeniden Başlat:systemctl restart seid

Node Bilgileri
Senkronizasyon Bilgisi:seid status 2>&1 | jq .SyncInfo

Validator Bilgisi:seid status 2>&1 | jq .ValidatorInfo

Node Bilgisi:seid status 2>&1 | jq .NodeInfo

Node ID Göser:seid tendermint show-node-id

Cüzdan İşlemleri
Cüzdanları Listele:seid keys list

Mnemonic kullanarak cüzdanı kurtar:seid keys add $WALLET --recover

Cüzdan Silme:seid keys delete $WALLET

Cüzdan Bakiyesi Sorgulama:seid query bank balances $WALLET_ADDRESS

Cüzdandan Cüzdana Bakiye Transferi:seid tx bank send $WALLET_ADDRESS <TO_WALLET_ADDRESS> 10000000usei

Oylama: seid tx gov vote 1 yes --from $WALLET --chain-id=$CHAIN_ID

Stake, Delegasyon ve Ödüller
Delegate İşlemi:seid tx staking delegate $VALOPER_ADDRESS 10000000usei --from=$WALLET --chain-id=$CHAIN_ID --gas=auto

Payını doğrulayıcıdan başka bir doğrulayıcıya yeniden devretme:seid tx staking redelegate <srcValidatorAddress> <destValidatorAddress> 10000000usei --from=$WALLET --chain-id=$CHAIN_ID --gas=auto

Tüm ödülleri çek:seid tx distribution withdraw-all-rewards --from=$WALLET --chain-id=$CHAIN_ID --gas=auto

Komisyon ile ödülleri geri çekin:seid tx distribution withdraw-rewards $VALOPER_ADDRESS --from=$WALLET --commission --chain-id=$CHAIN_ID

Doğrulayıcı Yönetimi
Validatör İsmini Değiştir:
seid tx staking edit-validator \
--moniker=NEWNODENAME \
--chain-id=$CHAIN_ID \
--from=$WALLET

Hapisten Kurtul(Unjail):
seid tx slashing unjail \
	--broadcast-mode=block \
	--from=$WALLET \
	--chain-id=$CHAIN_ID \
	--gas=auto

Node Tamamen Silmek:

sudo systemctl stop seid && \
sudo systemctl disable seid && \
rm /etc/systemd/system/seid.service && \
sudo systemctl daemon-reload && \
cd $HOME && \
rm -rf .sei sei-chain && \
rm -rf $(which seid)
