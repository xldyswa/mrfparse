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

## detailed features
- pipeline:Parse in-network MRF files. Input is a single MRF JSON file. Output is a parquet fileset.

```bsah
Usage:
  mrfparse pipeline [flags]

Flags:
  -h, --help              help for pipeline
  -i, --input string      Input path to JSON MRF file. Can be a local, HTTP, S3, or GCS path. Supports GZIPed files.
  -o, --output string     Output path for parsed MRF fileset in parquet format
  -p, --planid int        The planid acquired from the index file (default -1)
  -s, --services string   Path to a CSV file containing a list of CPT/HCPCS service codes to filter on
  ```
- parse:Parse in-network MRF files. Expects split NDJSON files as input.

```bsah
Usage:
  mrfparse parse [flags]
  
Flags:
  -h, --help              help for parse
  -i, --input string      input path to NDJSON files
  -o, --output string     output path for parsed MRF files in parquet format
  -p, --planid int        the planid acquired from the index file (default -1)
  -s, --services string   path to a CSV file containing a list of CPT/HCPCS service codes to filter on
  ```

- split:Split JSON files.
  
```bsah
Usage:
  mrfparse split [flags]

Flags:
  -h, --help            help for split
  -i, --input string    input path to JSON file.
  -o, --output string   output path for split NDJSON files
      --overwrite       overwrite contents of output path if it exists
  ```
  




