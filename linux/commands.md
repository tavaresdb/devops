# Comandos

## Conexão via SSH
```bash
ssh user@hostname.domain.com -i ~/.ssh/private_key
```

## Transferência de arquivos via SCP
```bash
scp -i ~/.ssh/private_key user@hostname.domain.com:/home/user/archive.txt .
scp -i ~/.ssh/private_key archive.txt user@other-hostname.domain.com:/home/user/
```

## Compactação de arquivo
```bash
tar -czvf archive.tar.gz archive.txt
```

## Descompactação de arquivo
```bash
tar -xzvf archive.tar.gz
```

## Identifica as permissões concedidas ao arquivo ou pasta
```bash
stat --format '%a' dir/
stat --format '%a' content.txt
```

## Localiza e remove arquivos criados há mais de 180 dias
```bash
find /tmp/backup -mtime +180 -type f -exec ls '{}' \;
find /tmp/backup -mtime +180 -type f -exec rm -fv '{}' \;
```

## Persistindo variáveis de ambiente
```bash
mkdir infraclass
touch infraclass/config
echo INFRACLASS_REGION=[YOUR_REGION] >> ~/infraclass/config
echo INFRACLASS_PROJECT_ID=[YOUR_PROJECT_ID] >> ~/infraclass/config
cat ~/infraclass/config
echo $INFRACLASS_REGION
echo $INFRACLASS_PROJECT_ID
vi .profile
..
source infraclass/config
:wq
```

# Visualiza o conteúdo do arquivo de certificado x509 em um formato legível
```bash
openssl x509 -in server.pem -text
```