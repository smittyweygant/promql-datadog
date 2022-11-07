PromQL to Datadog
=================

This script reads recently generated metrics from a Prometheus API Endpoint and imports them into DataDog

Requirements
------------

* Python 3.9+
* install python package dependencies
* have a datadog account and access to an api key
* have created a temporal observability endpoint with a CA
* have client certs signed by the CA uploaded to temporal

To install the required dependencies run:

```bash
python3 -m pip install requests
python3 -m pip install tenacity
python3 -m pip install datadog_api_client
```

Usage
-----

Running the script (either as an executable or with `python3 promql-to-dd.py`) will print out information about dependencies, and the `-h` cli argument can be used to see usage and command line options.

Either ENV vars or cli args can be specified for any of the required inputs, and all inputs are required to be specified in one way or another.

Here is the help output:

```
usage: promql-to-dd.py [-h] --temporal-account TEMPORAL_ACCOUNT --metrics-client-cert METRICS_CLIENT_CERT --metrics-client-key METRICS_CLIENT_KEY --dd-site DD_SITE --dd-api-key DD_API_KEY

Export Prometheus API metrics and import into DataDog

options:
  -h, --help            show this help message and exit
  --temporal-account TEMPORAL_ACCOUNT
  --metrics-client-cert METRICS_CLIENT_CERT
  --metrics-client-key METRICS_CLIENT_KEY
  --dd-site DD_SITE
  --dd-api-key DD_API_KEY
```

The env var names are the same as the `ALL_CAPS` names of the cli arg values, and cli args take precedence.

Example
-------

Here's an example, of setting up an environment and running the script:

```bash
# set up python virtual environment
python3 -m venv venv
. venv/bin/activate

# install deps
python3 -m pip install requests
python3 -m pip install tenacity
python3 -m pip install datadog_api_client

# set up environment
export TEMPORAL_ACCOUNT=acctcode
export METRICS_CLIENT_CERT=/path/to/cert
export METRICS_CLIENT_KEY=/path/to/key
export DD_SITE=datadog.api.endpoint.domain
export DD_API_KEY=123apikey321

# run the script
python3 promql-to-dd.py
```
