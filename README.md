# wehi-cbioportal-instance-schemaspy
Repo to share the output from schemaspy illustrating the cbioportal back-end database schematic.

## Getting the SchemaSpy output for cBioPortal Backend

The instructions assumes the docker compose setup from [the wehi-cbioportal-instance repo](https://github.com/WEHI-ResearchComputing/wehi-cbioportal-instance). Perform the instructions on the same machine that the cBioPortal instance is setup on.

### Getting the SchemaSpy Docker container

```bash
docker pull schemaspy/schemaspy
```

### Setting up the output folder

```bash
cd /where/ever
mkdir schemaspyoutputs
chmod 777 schemaspyoutputs
```

### Execute SchemaSpy

```bash
docker run \
    --network cbioportal-docker-compose_cbio-net \
    -v $(pwd -P)/schemaspyoutput:/output \
    schemaspy/schemaspy \
        -s cbioportal \
        -t mysql \
        -host cbioportal-database \
        -port 3306 \
        -u cbio_user \
        -p somepassword \
        -db cbioportal \
        -connprops 'useSSL\=false'
```

The files will be located in ./schemaspyoutput.

## Updating This Repo

```bash
mv schemaspyoutput/* /path/to/this/repo/docs
git add docs
git commit -m "your message"
git push
```
