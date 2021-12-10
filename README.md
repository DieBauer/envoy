# Let's Play with Envoy

<https://www.envoyproxy.io/docs/envoy/latest/start/install#install-envoy-on-ubuntu-linux>

```text
az group create --name envoy-01-group --location westeurope
```

```text
az vm create \
  --resource-group envoy-01-group \
  --name vm-01 \
  --image UbuntuLTS \
  --admin-username radicel \
  --generate-ssh-keys \
  --public-ip-sku Standard
```

```text
az vm show --resource-group envoy-01-group --name vm-01 --show-details | jq .publicIps
```

```text
ssh radicel@20.73.33.79
```

```text
sudo apt update
sudo apt install -y apt-transport-https gnupg2 curl lsb-release
curl -sL 'https://deb.dl.getenvoy.io/public/gpg.8115BA8E629CC074.key' | sudo gpg --dearmor -o /usr/share/keyrings/getenvoy-keyring.gpg
echo a077cb587a1b622e03aa4bf2f3689de14658a9497a9af2c427bba5f4cc3c4723 /usr/share/keyrings/getenvoy-keyring.gpg | sha256sum --check
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/getenvoy-keyring.gpg] https://deb.dl.getenvoy.io/public/deb/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/getenvoy.list
sudo apt update
sudo apt install -y getenvoy-envoy
```

```text
radicel@vm-01:~$ envoy --version

envoy  version: d362e791eb9e4efa8d87f6d878740e72dc8330ac/1.18.2/clean-getenvoy-76c310e-envoy/RELEASE/BoringSSL
```

```text
curl https://www.envoyproxy.io/docs/envoy/v1.18.2/_downloads/92dcb9714fb6bc288d042029b34c0de4/envoy-demo.yaml -o envoy-demo.yaml
```

```text
curl -v localhost:10000
```

<https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/intro/terminology>