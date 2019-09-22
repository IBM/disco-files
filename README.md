# discovery-files
A simple tool to send files into Watson Discovery, with simple retry.

![Book cover of "The Disco Files"](discofilescover.jpg)

## Requirements

This tool runs on a recent release of Python 3. We tested on Python 3.7.
With [Homebrew](https://brew.sh) on macOS, this will install Python 3.7:

```bash
brew install python3
```

One external library is needed: the Watson Developer Cloud SDK for Python.
This code was tested with SDK 3.2.0 and should work any 3.x release.

```bash
pip3 install ibm-watson
```

## Command line

```bash
./discofiles.py -h
usage: discofiles.py [-h] [-json JSON] [-collection_id COLLECTION_ID]
                     path [path ...]

Send files into Watson Discovery

positional arguments:
  path                  File or directory of files to send to Discovery

optional arguments:
  -h, --help            show this help message and exit
  -json JSON            JSON file containing Discovery service credentials;
                        default: "credentials.json"
  -collection_id COLLECTION_ID
                        Discovery collection_id; defaults to an existing
                        collection, when there is only one.
```

## Example runs

```bash
$ time ./discofiles.py ~/irs-pdf-en
Ignored 0 file(s), because they were found in collection.
Ingesting 1978 file(s).
Failing because it is HTTPSConnectionPool(host='gateway.watsonplatform.net', port=443): Max retries exceeded with url: /discovery/api/v1/environments/9ba5af06-4d03-4b0d-836a-cbe4b0a6f48e/collections/975b556e-f02f-4fb1-85b6-52a3bf88045a/documents?version=2017-09-01 (Caused by NewConnectionError('<urllib3.connection.VerifiedHTTPSConnection object at 0x11470e518>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known',))
Failing because it is HTTPSConnectionPool(host='gateway.watsonplatform.net', port=443): Max retries exceeded with url: /discovery/api/v1/environments/9ba5af06-4d03-4b0d-836a-cbe4b0a6f48e/collections/975b556e-f02f-4fb1-85b6-52a3bf88045a/documents?version=2017-09-01 (Caused by NewConnectionError('<urllib3.connection.VerifiedHTTPSConnection object at 0x114724550>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known',))
Failing because it is Error: Request must specify either a "metadata" or "file" part, Code: 400
Failing because it is HTTPSConnectionPool(host='gateway.watsonplatform.net', port=443): Max retries exceeded with url: /discovery/api/v1/environments/9ba5af06-4d03-4b0d-836a-cbe4b0a6f48e/collections/975b556e-f02f-4fb1-85b6-52a3bf88045a/documents?version=2017-09-01 (Caused by NewConnectionError('<urllib3.connection.VerifiedHTTPSConnection object at 0x115caa128>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known',))

real	10m21.783s
user	3m19.183s
sys	0m42.440s
$ time ./discofiles.py ~/irs-pdf-en
Ignored 1944 file(s), because they were found in collection.
Ingesting 34 file(s).

real	0m21.795s
user	0m2.202s
sys	0m0.724s
$ time ./discofiles.py ~/irs-pdf-en
Ignored 1974 file(s), because they were found in collection.
Ingesting 4 file(s).

real	0m8.049s
user	0m0.784s
sys	0m0.250s
```
