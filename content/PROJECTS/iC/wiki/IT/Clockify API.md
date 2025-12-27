
[[ClickUp Structure|ClickUp]] integrations for time tracking does not really work. [[2023-11-08#ClickUp alternatives|ClickUp alternatives]] are not as good as we would like to. A viable option would be to export ClickUp every now and then and upload tasks to Clockify with an API. Then export clockify tracked times and assign them to corresponding ClickUp tasks. Or keep using clockify, but fill in the time to the clickup manually.

[Official clockify api](https://docs.clockify.me/)


```python
"""
conda activate env
pip install clockify-api-client

dokumentace neni, ale projdi models a poradis si: https://github.com/group-eluvia-com/clockify-api-client/tree/main/clockify_api_client/models
"""


from clockify_api_client.client import ClockifyAPIClient
from pprint import pprint


API_KEY = 'OGY1MTY4ZjAtNWVhNy00MzhhLTg5ZTQtMWY4ZWY0Mjk3NjIy'
API_URL = 'api.clockify.me/v1'
# WORKSPACE = "5db6bb6abb56233f954de44b"  # Personal
WORKSPACE = "5ced8029f15c98168229cd17"  # iC
PROJECT = "5ced91fcf15c98168229e127" # sw development


client = ClockifyAPIClient().build(API_KEY, API_URL)

# result = client.projects.get_projects(WORKSPACE)  # list projects in workspace

# result = client.workspaces.get_workspaces()  # list workspaces

result = client.tasks.get_tasks(WORKSPACE, PROJECT)  # get tasks that are in a project
pprint(result)
```
