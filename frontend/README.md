# Frontend

https://github.com/bmpi-dev/logseq

```bash
cd ~/logseq
git clone https://github.com/bmpi-dev/logseq
git apply logseq.xyz.patch # use this patch apply changes
```

Finally, build release package:

```bash
yarn
yarn release # it's better to compile in your local computer and upload to server, cause it's hard to build in a 1GB/vCPU server😂
mv ./static ./public && rm -r ./public/workspaces # make sure to delete the old ./public/static directory
mv ./public/* /var/www/html # nginx static file for `asset.logseq.xyz`
```
