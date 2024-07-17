# pyroprompts-client

[PyroPrompts](https://pyroprompts.com) client for python! PyroPrompts is a platform enabling easier exchange and automation of AI Prompts, Snippets and Workflows. This client library assists in token management and abstracts the HTTP requests to make it easy to interact with the system.

Learn more at [https://pyroprompts.com](https://pyroprompts.com).

## Install

```bash
pip install pyroprompts-client
```

## Docs

### PyroPromptsClient

Create an instance of the `PyroPromptsClient` class with your credentials and then you may issue commands with that client instance.

_Note_: Might raise a `pyroprompts_client.PyroPromptsError` if PyroPrompts rejects the request

_Note_: Might raise a `pyroprompts_client.PyroPromptsTimeoutError` if the request times out

#### init
```python
from pyroprompts_client import PyroPromptsClient,
client = PyroPromptsClient(
    client_id="1234",
    client_secret="567890",
)
```

#### workflow_trigger
[see documentation](https://pyroprompts.com/documentation#oauth2-api-token-integration)

```python
# get all project snippets
client.workflow_trigger({
    "account_id": "YOUR_ACCOUNT_ID",
    "workflow_id": "WORKFLOW_ID",
    "workflow_form_params": {"param_1": "value_1"}
})
```

#### get_workflow_executions
[see documentation](https://pyroprompts.com/documentation#oauth2-api-token-integration)

```python
# get all project snippets
client.get_workflow_executions({
    "workflow_id": "abcd-1234-cdfg-abcdefg"
})
```

which returns:
```
{
    "count":1,
    "next":null,
    "previous":null,
    "results":[
        {
            "id":"1a7bae4f-f121-432b-b44e-abcdefg",
            "status":"complete",
            "status_message":null,
            "created_date":"2024-07-03T15:51:08.905236Z",
            "workflow_id":"ca00d56b-79bc-42b1-8e99-abcdefg",
            "result":"The response is in here",
            "form_params":null
        }
    ]
}
```

#### get_project_snippets
[see documentation](https://pyroprompts.com/documentation#oauth2-api-token-integration)

```python
# get all project snippets
client.get_project_snippets()
# pass some filters as a dict of query parameters (see documentation)
client.get_project_snippets({
    "project_id": "1234-56-78-9012",
    "created_date__gt": "2023-01-01",
    "limit": 1,
})
```

which returns:
```
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": "3d1daced-ce1d-4232-9b39-abcdefg",
            "name": "Snippet1",
            "description": null,
            "content": "Content of Snippet1",
            "project_id": "e95d56f8-72d1-4b13-bc5d-abcdefg",
            "deleted": 0,
            "created_by": "454517f4-a97e-45a7-8088-abcdefg",
            "created_date": "2024-07-03T15:38:14.387627Z",
            "updated_date": "2024-07-03T15:38:14.387645Z"
        },
        {
            "id": "f54049ee-266f-4fd7-a2f6-abcdefg",
            "name": "Snippet2",
            "description": null,
            "content": "Content of Snippet2",
            "project_id": "e95d56f8-72d1-4b13-bc5d-abcdefg",
            "deleted": 0,
            "created_by": "454517f4-a97e-45a7-8088-abcdefg",
            "created_date": "2024-07-03T15:45:49.697119Z",
            "updated_date": "2024-07-03T15:51:04.722434Z"
        },
        
    ]
}
```

#### logging
To get visibility into logged events, override the log method and log however your app needs to log:
```python
class CustomPyroPromptsClass(PyroPromptsClient):
    def log(self, level, msg, **log_variables):
        print(f"[{level}] {msg}", log_variables)
        

client = CustomPyroPromptsClass(client_id, client_secret)
```

## Example
```python
from pyroprompts import PyroPromptsClient, PyroPromptsError, PyroPromptsTimeoutError

my_client = PyroPromptsClient("1234", "56-789")
try:
    results = my_client.get_project_snippets()
    print(results)
except PyroPromptsError:
    print("PyroPrompts failure")
except PyroPromptsTimeoutError:
    print("PyroPrompts timed out")
```

## Common Commands:

Black Formatting
```bash
$ black pyroprompts_client --config pyroprompts_client.toml
```

Build
```bash
$ python3 setup.py sdist
```

Pypi Distribution
```bash
$ python3 -m twine upload dist/*
```

## License

PyroPrompts Client is [MIT licensed](./LICENSE).
