# jekyll-run

## Publish a new version of the image

Run the following command to build a new image and push it to GitHub Packages:

```shell
docker buildx build --push \
  --platform linux/amd64,linux/arm64 \
  --tag "ghcr.io/alexwlchan/jekyll-run:$VERSION" .
```

Don't forget to add an entry to the CHANGELOG!

## Add new dependencies

To update the `Gemfile.lock`:

```shell
docker run \
  --volume $(pwd):$(pwd) \
  --workdir $(pwd) \
  ruby:3.1-slim \
  bundle lock --update
```

You may need to update the Ruby image, depending on the RUby version defined in the Dockerfile.
