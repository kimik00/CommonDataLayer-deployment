
###  tested only on unix-like systems, ( gentoo, debian, HURD-6.1 )

###  First, install horust

```
cargo install horust
```

mind that horust currently does not create non-existing dirs and files default files, lets fix that
```
mkdir -p /etc/horust/services
```

we also need a softlink to your CDL repo create it in root of this repo, this process will be later automated
`ln -s /path/to/your/repo/CommonDataLayer cdl`

we need debug build present, (also, yes, debug, currently service files are made for debug only)
```
cd cdl
cargo build
```

services need some configuration first, basically you need to fix "user" field and set it to your user inside each service file
`user = "someuser"` to `user = "youruser"`

### Start infrastructure
navigate to infra and starting with logging output to console
```
docker-compose -f postgres.yml up
docker-compose -f kafka.yml up
```

alternatively start as daemons  only use when the deployment is stable on your setup
```
docker-compose -f postgres.yml -d up
docker-compose -f kafka.yml -d up
```

### Start Deployment

navigate to CommonDataLayer-deployment
```
horust --services-path bare/horust
```

and thats it
logs are placed in the same directory where you run the horust from
in case of problems with EONET or some other problem, good changes are
that its either missing exec or not existing directory

there are some docs about service files available here https://github.com/FedericoPonzi/Horust


