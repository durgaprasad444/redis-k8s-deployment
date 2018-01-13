# Yet another Redis docker image

Most of this image is a copy of

https://github.com/kubernetes/examples/tree/master/staging/storage/redis

I just rebased it on Ubuntu Xenial

# Testing

You can test locally with Docker running:
docker run -d --env MASTER=true -p 6379:6379 zioproto/redis

Then just run redis-cli on your host
