[<img src='https://user-images.githubusercontent.com/83868103/216377361-e56f8cff-7e4a-472d-85b0-015da3e95288.png' alt='discord'  width='49.7%'>](https://github.com/romanv1812/Jackal/blob/main/data/mainnet_guide.md)
[<img src='https://user-images.githubusercontent.com/83868103/216376966-053d9180-0723-4a8a-b77d-ee793dbc727e.png' alt='discord'  width='49.7%'>](https://restake.app/jackal/jklvaloper1qg9pjld3c26svc06u8r3k4cmjlaqg88jkald0p/stake)
[<img src='https://user-images.githubusercontent.com/83868103/216319382-71371073-ea4e-4fc9-bbb2-803cf43e553b.png' alt='discord'  width='100%'>](https://linktr.ee/jackal_protocol)
```python
Services status  🟢
```
```YAML
RPC:      http://65.109.85.170:53657 # Pruning: custom 100\10\100 Indexer kv
gRPC:     http://65.109.85.170:36090
gRPC Web: http://65.109.85.170:36091
API:      http://65.109.85.170:28317
peer:     2bb49680d595628991383323806db3fa53d15eb5@65.109.85.170:53656
seed:     3402bc832e2c1635a245b1301f0737b5f46f0ebd@65.109.85.170:11256
```
#
```python
Available RPCs UPD at 09:41 UTC ⏳ 23.04.23 🗓️ 
```
```YAML
INDEXER: 🟢 HEIGHT: 2475224 MONIKER: nkbblocks
RPC=65.109.61.114:37657

INDEXER: 🟢 HEIGHT: 2475224 MONIKER: jackal-private-rpc-hetzner
RPC=95.217.46.214:26657

INDEXER: 🟢 HEIGHT: 2451328 MONIKER: cyb
RPC=65.108.41.172:29957

INDEXER: 🔴 HEIGHT: 2475224 MONIKER: MantiCore
RPC=65.108.124.219:30657

INDEXER: 🟢 HEIGHT: 2475224 MONIKER: Vagif
RPC=65.109.116.50:27657

INDEXER: 🟢 HEIGHT: 2475224 MONIKER: kiwi
RPC=198.7.61.46:26657

```
#
```python
Shapshot UPD at 09:30 UTC ⏳ 23.04.23 🗓️ on HIGHT: 2475128 Size: 223G
```
```YAML
http://65.109.85.170:8001/jackal-db.tar.lz4 # Pruning: custom 100\10\100 Indexer kv
```
#
```python
INDEXER: 🔴 HEIGHT: 2475224 MONIKER: leafwind.tw
RPC=165.232.173.74:26657

Addrbook UPD at 09:41 UTC ⏳ 23.04.23 🗓️ 
```
```YAML
http://65.109.85.170:8001/addrbook.json
```
#
INDEXER: 🔴 HEIGHT: 2475224 MONIKER: moodman
RPC=65.109.65.210:32657

```python
Live Peers UPD at 09:41 UTC ⏳ 23.04.23 🗓️  Number Of Active Peers: = 8
```
```YAML
75d91291c734764a16dca870f51e3f34cb4a1309@65.109.61.114:37656,4cc343781bfeebbee21290c006d166a3b2d2006f@95.217.46.214:26656,80cc4b90a546a138a480642dd5ce0fcf65ba2d8c@65.108.41.172:29956,db9c7d34cd04e155b3eed730f68fc9315245cf5c@65.108.124.219:30656,2b7f02456898efbbb9da462b9b3e80ba12ff2f7c@65.109.116.50:27656,7d07a94348e20b698e0ebc264a8fe6f64128368c@198.7.61.46:26656,f460d33619705cb145d88631115a0b5581515060@165.232.173.74:26656,c5b43622ecd7413dd41905f6f8f5b5befd299ced@65.109.65.210:32656
```
---
# HOW TO USE?
```python
RECOVERY FROM STATE-SYNC
```
```bash
sudo systemctl stop canined && \
canined tendermint unsafe-reset-all --home $HOME/.canine
RPC=http://65.109.85.170:53657
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH
peer="2bb49680d595628991383323806db3fa53d15eb5@65.109.85.170:53656"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peer\"/" $HOME/.canine/config/config.toml
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
wget -O $HOME/.canine/config/addrbook.json http://65.109.85.170:8001/addrbook.json
sudo systemctl restart canined && journalctl -u canined -f -o cat
INDEXER: 🟢 HEIGHT: 2475224 MONIKER: lesnik_utsa_rpc
INDEXER: 🟢 HEIGHT: 2475224 MONIKER: MMS
RPC=65.108.6.45:60857

RPC=65.108.237.233:30657

```
INDEXER: 🟢 HEIGHT: 2475224 MONIKER: nkbblocks
RPC=65.21.139.150:37657

```python
DOWNLOAD ADDRBOOK
```
```bash
curl -s http://65.109.85.170:8001/addrbook.json > $HOME/.canine/config/addrbook.json
```
#
```python
RECOVERY FROM SNAPSHOT
```
```bash
sudo systemctl stop canined
rm -rf $HOME/.canine/data; \
mkdir -p $HOME/.canine/data; \
cd $HOME/.canine/data
wget -O -  http://65.109.85.170:8001/jackal-db.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.canine
sudo systemctl start canined; \
sudo journalctl -u canined -f
```
---
INDEXER: 🔴 HEIGHT: 2475224 MONIKER: moodman
RPC=65.109.65.210:32657

INDEXER: 🟢 HEIGHT: 2475224 MONIKER: AlxVoy
RPC=144.76.97.251:36157

INDEXER: 🟢 HEIGHT: 2475224 MONIKER: node
RPC=65.108.75.107:18657

INDEXER: 🔴 HEIGHT: 2475224 MONIKER: landeros
INDEXER: 🟢 HEIGHT: 2475224 MONIKER: jklnode
RPC=213.239.207.175:41657
RPC=141.95.47.216:26657


INDEXER: 🔴 HEIGHT: 2475224 MONIKER: DEA3D34D288B3241A63AB5631482EACD
INDEXER: 🔴 HEIGHT: 2475224 MONIKER: BRAND-jackal-main
RPC=116.202.36.240:10757
RPC=65.109.24.188:17557


INDEXER: 🟢 HEIGHT: 2475224 MONIKER: node
RPC=65.108.141.109:18657

