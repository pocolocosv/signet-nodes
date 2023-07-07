# LND - signet
1. run `docker compose up -d`
1. run `docker ps` and get bitcoin core and lnd container names
1. wait bitcoin core sync `docker logs <bitcoin core container name>`
1. run `docker exec -it <lnd container name> lncli create` follow the steps and create a new seed
1. run `docker exec -it <lnd container name> lncli -n signet getinfo` and validate uris, it should show something like:
```
"uris": [
    "03c6966e5859818274954e82faa698f595dd75f94cf1a315a0b6c99297463ee3c8@zpelysqtvey3ywzg37hjpdl4xcae45epcnunstn7toqofpze6mm7jfyd.onion:9735"
],
```
1. create a new address`docker exec -it <lnd container name> lncli -n signet newaddress p2tr`
1. use a faucet to send coins to the generated address
1. wait and validate wallet balance `docker exec -it <lnd container name> lncli -n signet walletbalance`
1. restart the environment `docker compose down` and then `docker compose up -d`. Use `docker ps` and wait the status `healthy` for tor container 
1. unlock the wallet `docker exec -it <lnd container name> lncli -n signet unlock`
1. validate wallet balance `docker exec -it <lnd container name> lncli -n signet walletbalance` (should return the previous balance)
