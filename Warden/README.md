# Update 0.3.2

```
systemctl stop wardend

cd $HOME/wardenprotocol
wget https://github.com/warden-protocol/wardenprotocol/releases/download/v0.3.2/wardend_Linux_x86_64.zip
unzip wardend_Linux_x86_64.zip
rm -rf wardend_Linux_x86_64.zip
chmod +x wardend
mv $HOME/wardenprotocol/wardend $(which wardend)
wardend version --long | grep -e version -e commit

curl -L https://buenavista-genesis.s3.eu-west-1.amazonaws.com/genesis.json.tar.xz | tar xJf -
mv genesis.json $HOME/.warden/config/genesis.json
```
## SNAP
```
wardend tendermint unsafe-reset-all --home $HOME/.warden
rm -fR $HOME/.warden/wasm
curl -L https://buenavista-genesis.s3.eu-west-1.amazonaws.com/warden-snaphot.tar.lz4 | lz4 -dc - | tar -xf - -C "$HOME/.warden"
systemctl restart wardend && journalctl -u wardend -f
```
## Consensus
```
cd && git clone https://github.com/Northa/consensus.git && cd consensus
python3 consensus.py
```
