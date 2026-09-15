# package-pin-auditor

Find package requirements missing an exact version in a normalized package list.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "packages": [
    {
      "name": "curl",
      "version": "7.81.0"
    },
    {
      "name": "tool",
      "version": "*"
    }
  ]
}
```

Result:

```json
{
  "issues": [
    {
      "package": "tool",
      "issue": "not-exactly-pinned"
    }
  ],
  "all_pinned": false
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Checks normalized version strings, not package-manager resolution or vulnerability status.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [certificate-inventory-reporter](https://github.com/sal-s-root/certificate-inventory-reporter), [ansible-task-tag-auditor](https://github.com/sal-s-root/ansible-task-tag-auditor).
