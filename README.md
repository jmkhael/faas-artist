
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

## Style transfer

#### Generates Monet style

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

you can also use the accompanying script `pastiche.sh`

usage:
```
./pastiche.sh path_to_image_file style style_index
```

style can be monet or varied. style_index from 0 to 9 for monet, and from 0 to 30 for varied.
> try them all, and see what you like!

```
./pastiche.sh artist/input/tree.jpg varied 24
./pastiche.sh artist/input/tree.jpg monet 2
```

### Multi-style transfer

We can also apply a multi-style blending several styles of a given model together, based on weights. e.g.: `{1:0.3, 10:0.5, 24:0.2}` to tell the artist to use style 1, style 2 and style 24 in the proportions `30% - 50% - 20%`.


```
curl -X POST -H X-style-name:varied -H X-which-styles:'{1:0.2,10:0.3,24:0.5}' \
  --data-binary @artist/input/meme-test.jpg \
  "http://localhost:8080/function/artist" > styled/meme-test-varied-1-10-24.jpg
```

Explore some more outputs under [styled folder](styled) or in this [album](https://photos.app.goo.gl/MCNnnrmlCSBwR9xH3) to get a better idea, or check the blog post.
