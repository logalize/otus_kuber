# Helmfile
wget https://github.com/roboll/helmfile/releases/download/v0.138.7/helmfile_linux_amd64 \
chmod +x helmfile_linux_amd64 \
mv helmfile_linux_amd64 /usr/sbin/helmfile \
helm plugin install https://github.com/databus23/helm-diff

Показываем helmfile, объясняем, применяем

```
helmfile --environment develop apply
```