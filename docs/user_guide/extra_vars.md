# Extra Vars

## Extra Vars

Extra Vars is a way to read runtime arguments to your code. Whe you launch a job, you can add JSON data. If the task contains a schema, the data must comply to the schema spec.

Kriten presents the data as a JSON string stored in an environment variable called EXTRA_VARS. To use EXTRA_VARS in your code, you need to read the environment variable and load the JSON string as an object.

Python example:

```python
import os
extra_vars = os.environ.get('EXTRA_VARS')
if extra_vars:
    extra_vars_data = json.loads(extra_vars)
```

While developing, you may want to set EXTRA_VARS manually. Note that you need to escape the double quotes, for example:

```console
export EXTRA_VARS="{\"fabric\":\"ukdc1\"}"
```
