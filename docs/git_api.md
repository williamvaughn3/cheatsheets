# GitLab API Queries for Project Variables

API Queries for Project Variables


```python
import requests

GLd_PAT = 'your_personal_access_token'
GL_URI = 'gitlab url here'

headers = {'Private-Token': GL_PAT}

def all_pjs():
    projects = []
    page = 1
    while True:
        resp = requests.get(f'{GL_URI}projects?page={page}', headers=headers)
        data = resp.json()
        if not data:
            break
        projects.extend(data)
        page += 1
    return projects

def get_project_variable(project_id, variable_key):
    resp = requests.get(f'{GL_URI}projects/{project_id}/variables/{variable_key}', headers=headers)
    if resp.status_code == 200:
        return resp.json()
    return None

projects = all_pjs()

for project in projects:
    project_id = project['id']
    # Replace 'ENTER_VAR_TO_QUERY_HERE' with your specific variable key
    variable = get_project_variable(project_id, 'ENTER_VAR_TO_QUERY_HERE')
    if variable:
        print(f"Project ID: {project_id}, Variable: {variable['key']} = {variable['value']}")

```

# Handling errors


When making requests to the GitLab API, handle authentication errors by checking the HTTP status code of the response

If the status code is 401...the request was not authenticated. 

Modify your code to handle this:

```python
def all_pjs():
    projects = []
    page = 1
    while True:
        resp = requests.get(f'{GL_URI}projects?page={page}', headers=headers)
        if resp.status_code == 401:
            raise Exception('Authentication failed. Please check your GitLab token.')
        data = resp.json()
        if not data:
            break
        projects.extend(data)
        page += 1
    return projects

def get_project_variable(project_id, variable_key):
    resp = requests.get(f'{GL_URI}projects/{project_id}/variables/{variable_key}', headers=headers)
    if resp.status_code == 401:
        raise Exception('Authentication failed. Please check your GitLab token.')
    if resp.status_code == 200:
        return resp.json()
    return None
```

Finally, we can define a main function to orchestrate the fetching of projects and their variables. This function will also parse the command line arguments and validate them. Here's the final code:


```python
import requests
import argparse
import re

GL_URI = 'gitlab url here'

def parse_args():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description='Fetch GitLab project variables.')
    parser.add_argument('--token', help='GitLab personal access token', required=True)
    parser.add_argument('--project_id', help='GitLab project ID', required=False, type=int)
    # Add more arguments as needed
    args = parser.parse_args()

    # TODO: Add input validation using regex here
    # Example: if not re.match("your-regex-pattern", args.token):
    #             raise ValueError("Invalid token format")

    return args

def gl_auth(token):
    """ Set up authentication headers. """
    return {'Private-Token': token}

def all_pjs(headers):
    """ Fetch all projects from GitLab. """
    projects = []
    page = 1
    try:
        while True:
            resp = requests.get(f'{GL_URI}projects?page={page}', headers=headers)
            if resp.status_code != 200:
                raise Exception(f"Failed to fetch projects: {resp.status_code} {resp.reason}")
            data = resp.json()
            if not data:
                break
            projects.extend(data)
            page += 1
    except requests.RequestException as e:
        print(f"An error occurred while fetching projects: {e}")
    return projects

def get_project_variables(project_id, variable_keys, headers):
    """ Fetch specific variables for a given project. """
    variables = {}
    try:
        for key in variable_keys:
            resp = requests.get(f'{GL_URI}projects/{project_id}/variables/{key}', headers=headers)
            if resp.status_code == 200:
                var_data = resp.json()
                variables[var_data['key']] = var_data['value']
            else:
                print(f"Failed to fetch variable '{key}' for project {project_id}: {resp.status_code} {resp.reason}")
    except requests.RequestException as e:
        print(f"An error occurred while fetching variables for project {project_id}: {e}")
    return variables

def fetch_variables_for_all_projects(headers, variable_keys):
    """ Fetch and print variables for all projects. """
    projects = all_pjs(headers)
    for project in projects:
        project_id = project['id']
        variables = get_project_variables(project_id, variable_keys, headers)
        if variables:
            print(f"Project ID: {project_id}, Variables: {variables}")

def fetch_variables_for_defined_project(project_id, headers, variable_keys):
    """ Fetch and print variables for a defined project. """
    variables = get_project_variables(project_id, variable_keys, headers)
    if variables:
        print(f"Project ID: {project_id}, Variables: {variables}")

def main():
    """ Main function to orchestrate the fetching of projects and their variables. """
    args = parse_args()
    headers = gl_auth(args.token)
    variable_keys = ['VARIABLE_KEY1', 'VARIABLE_KEY2']  # Replace with your specific variable keys
    
    #search defined project
    fetch_variables_for_defined_project(args.project_id, headers, variable_keys)
    
    #search all projects
    #fetch_variables_for_all_projects(headers, variable_keys)

if __name__ == "__main__":
    main()

```