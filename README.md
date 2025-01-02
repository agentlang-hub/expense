# Example app - expense-report

An "expense report" example Agentic AI app that helps file an expense report.

It files an expense report by recognizing the text on a receipt image, so
you can just upload your receipt image on the Internet and refer to the file
hyperlink.

## Usage

You need a Unix-compatible (macOS, Linux or Windows [WSL](https://learn.microsoft.com/en-us/windows/wsl/install))
system to run this app. Open a terminal and execute the steps below:

You need to specify the OpenAI API key as shown below.

```shell
export OPENAI_API_KEY="FIXME"
```

You may run this app without making a local copy first (i.e. clone the repo) using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent clonerun https://github.com/agentlang-hub/expert.git
```

### Running a local copy of the app

If you have cloned the app and made a local copy on your computer,
You may run it using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent run
```

Alternatively, instead of Docker you may use the locally installed
[Agentlang CLI](https://github.com/agentlang-ai/agentlang.cli):

```shell
agent run
```

### Submitting expense report

You need to open another terminal and run the following command:

```shell
curl -X POST localhost:8080/api/Expense.Workflow/SaveExpenses \
  -H 'Content-type: application/json' \
  -d '{"Expense.Workflow/SaveExpenses": {"UserInstruction": "https://acme.com/bill/myexpense.jpg"}}'
```

You may get an output as follows:

```json
[{"status":"ok","result":null,"message":null}]
```

or,

```json
[{"status":"ok","result":[{"Title":"Expense Report 3","Amount":300.0,"Id":"74b1df98-aef5-4b3b-939d-535672e2af9c"}],"message":null,"type":"Expense.Workflow/Expense"}]
```

## License

Copyright 2024-2025 Fractl Inc.

Licensed under the Apache License, Version 2.0:
http://www.apache.org/licenses/LICENSE-2.0

