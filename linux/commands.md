# Comandos

## Identifica as permissões concedidas ao arquivo ou pasta
```bash
stat --format '%a' dir/
stat --format '%a' content.txt
```

## Localiza e remove arquivos criados há mais de 180 dias
```bash
find /tmp/backup -mtime +180 -type f -exec ls '{}' \;
find /tmp/backup -mtime +180 -type f -exec rm -fv '{}' \;4
```

## Persistindo variáveis de ambiente
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