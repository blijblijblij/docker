# Docker Image for Vertica

The image is available in Docker registry at https://registry.hub.docker.com/u/sumitchawla/vertica/

Base OS is Ubuntu 14.04.

## Usage:
You can either pull the image from Docker Registry using following command:

```bash
docker pull sumitchawla/vertica
```

Or, build your own image using following command. Download the Vertica DEB package from https://my.vertica.com and put it in this folder as "vertica.deb".
Then run:
```bash
docker build -t sumitchawla/vertica .
```

### To run without a persistent datastore
```bash
docker run -p 5433:5433  sumitchawla/vertica
```

### To run with a persistent datastore
```bash
docker run -p 5433:5433 -d -v /path/to/vertica_data:/home/dbadmin/docker sumitchawla/vertica
```
### Connection Parameters
 Default DB Name - docker
 
 Default User - dbadmin
 
 Default Password (NO PASSWORD) - 
