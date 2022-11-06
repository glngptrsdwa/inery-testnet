update inery yg mau baru install bisa menggunakan snapshot dengan ketinggian block 951801

Sebelumnya cek block dulu:

a. Cek block sekarang

```
curl -sSL -X POST 'http://bis.blockchain-servers.world:8888/v1/chain/get_info' -H 'Accept: application/json' | jq -r '.head_block_num'

```
b. Cek block di nodesendiri
``` 
curl -sSL -X POST 'http://localhost:8888/v1/chain/get_info' -H 'Accept: application/json' | jq -r '.head_block_num'
```
Jika block di node sendiri masih dari block snapshot yaitu 951801 jauh bisa di lanjutkan:

1. Stop and clean data blockchain inery
```
cd $HOME/inery-node/inery.setup/master.node/
./stop.sh
pkill nodine
./clean.sh
```
2. Download dan extract snapshot
```
wget -O inery.tar.gz http://test-azero.jambulmerah.dev:80/inery.tar.gz && tar -xzvf inery.tar.gz
```
2. Rename shared memory to default
```
mv blockchain/data/blockchain/blocks/reversible/shared_memory.bak blockchain/data/blockchain/blocks/reversible/shared_memory.bin

mv blockchain/data/state/shared_memory.bak blockchain/data/state/shared_memory.bin
```
3. Start again
```
./start.sh
```

4. Cek log
```
tail -f blockchain/nodine.log
```

## tinggal tunggu block nya sync , kalo udah sync bisa lanjut ke step wallet
https://github.com/glngptrsdwa/inery-testnet#create-wallet