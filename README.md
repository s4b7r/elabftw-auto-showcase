# eLabFTW Automation Show Case

This is an example how you can extract metadata from "some file" (e.g. the raw data file of a measurement), and create a new experiment entry with it in your eLabFTW instance.

## Requirements / Setup

This example requires you to have access to an eLabFTW instance where you can create new experiments.

If you have your own Python environment to run this Jupyter notebook in, you can use the `environment.yml` file to find out about the used packages.

If you have your own conda installation, you can use the following command to create a new environment for this example.

```sh
conda env create -f environment.yml -n lab-test
```

If you do not have a Python environment at hand, ... sorry, I am still working on the mybinder environment.

## Technicalities

### Ipython Notebooks in Git

I do this because I like to clean up my Jupyter notebooks before commiting, e.g. to remove secrets.

Remeber to put the following filter into the repo's config:

```
[filter "nbstrip_full"]
        clean = "\"jq\" --indent 1 \
                '(.cells[] | select(has(\"outputs\")) | .outputs) = []  \
                | (.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
                | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
                | .cells[].metadata = {} \
                '"
        smudge = cat
        required = true
```

And also

```
*.ipynb filter=nbstrip_full
```

into `.gitattributes`.

Install [jq](https://stedolan.github.io/jq/) somewhere into `PATH`, if necessary.
