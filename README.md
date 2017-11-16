
## Context

This repository holds the code for the OpenFaaS function to do style transfer.
You ideally should read along the blog post on http://jmkhael.io/ 

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
![Original](/artist/input/faas-community.jpg?raw=true "Original Vespa and Faas") | ![Styled](/styled/faas-community-varied-6.jpg?raw=true "Varied style 6")


The stylized image were generated using:

```
curl -X POST -H X-style-name:varied -H X-style-index:24 \
  --data-binary @artist/input/vespa-faas.jpg \
  "http://localhost:8080/function/artist" > styled/vespa-faas-varied-24.jpg
```  

```
curl -X POST -H X-style-name:varied -H X-style-index:6 \
  --data-binary @artist/input/faas-community.jpg \
  "http://localhost:8080/function/artist" > styled/faas-community-varied-6.jpg
```

you can also use the accompanying script `paint.sh`

usage:
```
./paint.sh path_to_image_file style style_index
```

style can be monet or varied. style_index from 0 to 9 for monet, and from 0 to 30 for varied.
> try them all, and see what you like!

```
./paint.sh artist/input/tree.jpg varied 24
./paint.sh artist/input/tree.jpg monet 2
```

Explore some more outputs under [styled folder](styled) to get a better idea, or check the blog post.
