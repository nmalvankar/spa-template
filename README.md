Create the build configs
- Build Config for Application
- Build Config for Builder Image
- Build Config for Application Templates

```
oc process -f .openshift/templates/build.yml -p=APPLICATION_NAME=basic-spa -p NAMESPACE=jenkins -p=SOURCE_REPOSITORY_URL="https://github.com/nmalvankar/spa-template.git" -p=APPLICATION_SOURCE_REPO="https://github.com/nmalvankar/spa-template.git" -p=APPLICATION_BUILDER_SOURCE_REPO=https://github.com/nmalvankar/proxy-http.git -p=IMAGE_STREAM_TAG_NAME=basic-spa-builder:latest | oc apply -f-
```

Create the application deployment

```
oc process -f .openshift/templates/deployment.yml -p=APPLICATION_NAME=basic-spa -p NAMESPACE=jenkins -p=READINESS_PATH="/" -p=READINESS_RESPONSE="Apache HTTP server"  | oc apply -f-
```
