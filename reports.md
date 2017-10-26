# Reports

## Aeroo Reports

### Docker container for aeroo reports service

```
docker run --detach --publish=8989:8989 --name aeroo_docs --restart=always adhoc/aeroo-docs
```

### Aeroo Python dependences

```
pip install http://launchpad.net/aeroolib/trunk/1.0.0/+download/aeroolib.tar.gz
pip install genshi==0.6.1
pip install pycups
```

## Reports using py3o.fusion Server

py3o.fusion is a server that exposes as a web service a way to render an ODT file into different formats. It is a server that converts native LibreOffice files to supported targets.

```
wget https://bitbucket.org/xcgd/py3o.fusion/raw/76dcb04477c4ddcaa303db94ae340561c2da75a9/docker-compose.yml
docker-compose up
```
