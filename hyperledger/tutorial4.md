
# Chạy lại Business Network

```sh
export FABRIC_VERSION=hlfv11
./startFabric.sh

composer network install --card PeerAdmin@hlfv1 --archiveFile mynetwork@0.0.2.bna

composer network start --networkName mynetwork --networkVersion 0.0.2 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

```