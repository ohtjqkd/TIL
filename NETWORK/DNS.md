# DNS

## Local DNS 구축
VPC 내부에 있는 특정 서버에 domain을 설정하고 싶을 때, local DNS를 구축해야 한다.

### 1. DNS 서버 설치
```bash
sudo apt-get update
sudo apt-get install bind9
```

### 2. DNS 설정
```bash
sudo vi /etc/bind/named.conf.local
```

```conf
zone "example.com" {
    type master;
    file "/etc/bind/db.example.com";
};
```

```bash
sudo vi /etc/bind/db.example.com
```

```conf
$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      ns1.example.com.
@       IN      A
ns1     IN      A
```

### 3. DNS 서버 재시작
```bash
sudo systemctl restart bind9
```

### 4. DNS 서버 테스트
```bash
nslookup example.com
```

## 참고
- [How to Setup a Local DNS Server on Ubuntu 20.04](https://www.tecmint.com/setup-local-dns-using-bind9-on-ubuntu/)
- [How to Configure BIND DNS Server on Ubuntu](https://linuxhint.com/configure_bind_dns_server_ubuntu/)

## HOSTS and RESOLV.CONF

내부 DNS를 구축하던 도중 인증서 관련 이슈로 인해 지체되어 `RESOLV.CONF`와 `HOSTS` 파일에 대해 먼저 정리해보려 한다.

### HOSTS

`/etc/hosts` 파일은 IP 주소와 도메인 이름을 매핑하는데 사용된다. 이 파일은 DNS 서버보다 먼저 검색되기 때문에, 로컬 네트워크에서 사용되는 호스트 이름을 설정할 때 유용하다.

```bash
sudo vi /etc/hosts
```
```conf
## /etc/hosts
127.0.0.1       localhost
127.0.1.1       my-host

127.0.0.2       some.domain.com

...
```
위와 같이 ip 주소와 도메인 이름을 매핑해주면 된다.