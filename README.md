```
faas-cli build -f artist.yml
faas-cli deploy -f artist.yml
```

```
curl -X POST -H X-style-name:monet -H X-style-index:1 --data-binary @../faas-stylist/input/blizzard.jpg "http://localhost:8080/function/artist" > out_monet_1.jpg
```

```
curl -X POST -H X-style-name:varied -H X-style-index:24 --data-binary @../faas-stylist/input/blizzard.jpg "http://localhost:8080/function/artist" > out_varied_24.jpg
```
