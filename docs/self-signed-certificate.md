# Self-signed Certificate

- [Certificates for localhost](https://letsencrypt.org/docs/certificates-for-localhost/)
- GitHub: [jsha/minica](https://github.com/jsha/minica)

## Install

First, install the [Go tools](https://golang.org/dl/) and set up your $GOPATH. Then, run:

```bash
go get github.com/jsha/minica
```

---

## Certificate

```bash
minica -domains example.localhost -ca-cert rootca.pem -ca-key rootca.key.pem
```

### Chained

```bash
cat example.localhost/cert.pem rootca.pem > chained.pem
```

### Result

- RootCA Cert: [rootca.pem](/certs/self-signed/rootca.pem)
- RootCA Key: [rootca.key.pem](/certs/self-signed/rootca.key.pem)
- Cert: [cert.pem](/certs/self-signed/example.localhost/cert.pem)
- Key: [key.pem](/certs/self-signed/example.localhost/key.pem)
- Chained Cert: [chained.pem](/certs/self-signed/chained.pem)

```bash
certs/self-signed/
├── example.localhost/
│   ├── cert.pem
│   └── key.pem
├── chained.pem
├── rootca.key.pem
└── rootca.pem
```

---

## Keychain Access

1. Open Keychain Access
2. Add `rootca.pem`, `cert.pem`
3. Set `When using this certificate` to `Always Trust`

## /etc/hosts

Add:

```bash
127.0.0.1 example.localhost
```
