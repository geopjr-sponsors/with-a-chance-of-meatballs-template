# with-a-chance-of-meatballs-template

A template for [with-a-chance-of-meatballs](https://github.com/GeopJr/with-a-chance-of-meatballs) to create services like [is-a.dev](https://www.is-a.dev/) & [js.org](https://js.org/).

## How it works

Create a repo secret named `CF_TOKEN` with your CloudFlare token.

In the `domains` folder, create a folder for each domain you want to include named as that. Inside of it users will be able to create `<anything>.json` files with their records.

The JSON files have the following format:

```json
{
  "contact": {
    "email": "String?",
    "twitter": "String?",
    "fediverse": "String?",
    "discord": "String?",
    "matrix": "String?",
    "session": "String?",
    "wire": "String?",
    "telegram": "String?"
  },
  "records": {
    "<A/AAAA/CNAME/TXT>": [
      {
        "name": "String",
        "content": "String",
        "ttl": "Int32?",
        "description": "String?"
      }
    ]
  }
}
```

> Browse the [`/domains`](/domains) folder for some examples.

The `contact` part exists as a way for you to contact the record submitter when needed.

Remember to write down simple TOS so submitters know what is and isn't allowed.

The workflow gets triggered manually. It first downloads [sponsors.cr](https://github.com/GeopJr/sponsors.cr), runs it with the `domains/` folder as input, uploads the exported jsons to artifacts and exports an env var with the output of the find command in an array format to be consumed by the next job.

The next job uses the previously exported env var as a matrix (eg. `["example.com", "anotherexample.com"]`) in an attempt to run the job in a "loop". It then downloads the jsons from the artifacts and runs with-a-chance-of-meatballs for each one.

**IMPORTANT**: Both sponsors.cr and with-a-chance-of-meatballs are version or commit locked. Since the action uses your CF token, this is the safest/most secure approach. If you are having issues, take a look if the repos have had any new releases or commits and update them manually after auditing them.

## Sponsors

<p align="center">

[![GeopJr Sponsors](https://cdn.jsdelivr.net/gh/GeopJr/GeopJr@main/sponsors.svg)](https://github.com/sponsors/GeopJr)

</p>
