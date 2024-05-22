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
