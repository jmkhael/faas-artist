## Get faas-cli
```
curl -sSL https://cli.openfaas.com | sudo sh
```

## Build and deploy
```
faas-cli build -f artist.yml
faas-cli deploy -f artist.yml
```

## Profit!

### Generates Monet style

Original             |  Styled
:-------------------------:|:-------------------------:
![Original](/artist/input/blizzard.jpg?raw=true "Original Blizzard") | ![Styled](/styled/blizzard-styled-monet.jpg?raw=true "Monet style 1")

The stylized image was generated using:
```
curl -X POST -H X-style-name:monet -H X-style-index:1 \
  --data-binary @artist/input/blizzard.jpg \
  "http://localhost:8080/function/artist" > styled/blizzard-styled-monet.jpg
```

### Generates Varied style
Original             |  Styled
:-------------------------:|:-------------------------:
![Original](/artist/input/vespa-faas.jpg?raw=true "Original Vespa and Faas") | ![Styled](/styled/vespa-faas-varied-24.jpg?raw=true "Varied style 24")
![Original](/artist/input/faas-community.jpg?raw=true "Original Vespa and Faas") | ![Styled](/styled/faas-community-varied-6.jpg?raw=true "Varied style 24")
```
curl -X POST -H X-style-name:varied -H X-style-index:24 \
  --data-binary @artist/input/vespa-faas.jpg \
  "http://localhost:8080/function/artist" > styled/vespa-faas-varied-24.jpg
```  |  
```
curl -X POST -H X-style-name:varied -H X-style-index:24 \
  --data-binary @artist/input/faas-community.jpg \
  "http://localhost:8080/function/artist" > styled/faas-community-varied-6.jpg
```

The stylized image was generated using:
