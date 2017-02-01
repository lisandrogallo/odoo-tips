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
pip install geopy==0.95.1
```
