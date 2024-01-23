# How to use this project
## Notes of caution
- Make sure your go version is above 1.19  `go version`

##   Build and Usage
Enter the main directory 
```bash
cd mrfparse
```

Use the `Makefile` to build the binary or container. 

- Build the binary
```bash
make 
```
The following examples illustrate using the binary from a command line. 

Parse a gzipped MRF file hosted on a payer's website and output the parquet dataset to the local filesystem. `/tmp/out`
```bash
./out/bin/mrfparse pipeline -i https://mrf.healthsparq.com/aetnacvs-egress.nophi.kyruushsq.com/prd/mrf/AETNACVS_I/AFEHBPFI/2024-01-05/inNetworkRates/2024-01-05_8e0af629-6cc4-4e56-a55e-11f5cb66e752_Aetna-Life-Insurance-Company.json.gz
                            -o /tmp/out
                            -s data/tic_500_shoppable_services.csv
                            -p 99
```

- Build the container
```bash
make docker-build
```

Parse a gzipped MRF file hosted on a payer's website and output the parquet dataset to the local filesystem. ( In a Docker container, mount the $(pwd) directory from the host system to the /mrfparse directory in the container, and allow read and write operations on that directory.)
```bash
docker run -it -v "$(pwd):/mrfparse:rw" mrfparse pipeline -i https://mrf.healthsparq.com/aetnacvs-egress.nophi.kyruushsq.com/prd/mrf/AETNACVS_I/AFEHBPFI/2024-01-05/inNetworkRates/2024-01-05_8e0af629-6cc4-4e56-a55e-11f5cb66e752_Aetna-Life-Insurance-Company.json.gz
                                                          -o /tmp/out
                                                          -s data/tic_500_shoppable_services.csv
                                                          -p 99
```







