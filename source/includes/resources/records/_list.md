### List

List all open access records if no `ACCESS_TOKEN` is provided. 
Otherwise it will add the records to which the authenticate user has access.

```python
import requests

response = requests.get(
    "/api/records", params={"q": "my title", "access_token": ACCESS_TOKEN}
)
print(response.json())
```

```shell
curl -i /api/records/?access_token=ACCESS_TOKEN
```

#### HTTP Request

`GET /api/records/`

#### Query arguments

| Parameter                   | Required | Description                                                                                                                    |
|:----------------------------|:---------|:-------------------------------------------------------------------------------------------------------------------------------|
| `q`</br>_string_            | optional | [Search query](https://help.zenodo.org/guides/search/) (using Elasticsearch query string syntax).                                                                         |
| `status`</br>_string_       | optional | Filter result based on deposit status (either ``draft`` or ``published``)                                                      |
| `sort`</br>_string_         | optional | Sort order (``bestmatch`` or ``mostrecent``). Prefix with minus to change form ascending to descending (e.g. ``-mostrecent``). |
| `page`</br>_integer_        | optional | Page number for pagination.                                                                                                    |
| `size`</br>_integer_        | optional | Number of results to return per page.                                                                                          |
| `communities`</br> _string_ | optional | Return records part of the specified communities. (Use of `community identifier`)                                              |
| `type`</br> _string_        | optional | Return records part of the specified type. (`Publication`, `Poster`, `Presentation`...)                                        |
| `subtype`</br> _string_     | optional | Return records part of the specified subtype. (`Journal article`, `Preprint`, `Proposal`...)                                   |
| `custom`</br> _string_      | optional | Return records part of the specified custom keywords. (Format `custom=[field_name]:field_value`)                               |

#### Header

Response format of the search can be requested by specifying it in the header.

| Accept                                    | Description       |
|:------------------------------------------|:------------------|
| `application/json`                        | JSON              |
| `application/ld+json`                     | JSON-LD           |
| `application/vnd.zenodo.v1+json`          | Zenodo            |
| `application/marcxml+xml`                 | Marc XML          |
| `application/x-bibtex`                    | Bibtex            |
| `application/x-datacite+xml`              | Datacite XML      |
| `application/x-dc+xml`                    | Dublin Core       |
| `application/dcat+xml`                    | DCAT XML          |
| `application/vnd.citationstyles.csl+json` | Citation JSON     |
| `application/vnd.geo+json`                | Geo-JSON          |
| `application/x-datacite-v41+xml`          | Datacite v4.1 XML |
| `text/x-bibliography`                     | Bibliography      |

#### Success Response

* **Code:** `200 OK`
* **Body**: an array of [record](#records) resources.

#### Error Response

See [HTTP status codes](#http-status-codes) (400 and 500 series errors) and
[error responses](#errors).

#### Search guide

Advanced search queries can as well be performed on Zenodo website through the search box. This is documented in the [search guide](https://help.zenodo.org/guides/search/)