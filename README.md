[Adding to @pythoninthegrass 's answer:](https://stackoverflow.com/a/74727952/14343465)

A method I use frequently is generating project boilerplate code using [cookiecutter](https://github.com/cookiecutter/cookiecutter), which allows for all instances to be templated using jinja syntax

## for example

`pyproject.toml`
```toml
[tool.black]
target-version = ["py39"]
line-length = {{ cookiecutter.line_length }}

[tool.isort]
py_version = 39
line_length = {{ cookiecutter.line_length }}
```

along with your `cookiecutter.json` file

```js
{
  "project_name": "python-project",
  "line_length": 88
}
```

## using your example

`.flake8` file:

    max-line-length = {{ cookiecutter.line_length }}

`.isort.cfg` file:

    line-length = {{ cookiecutter.line_length }}

`.black` file:

    line-length = {{ cookiecutter.line_length }}

`.pylintrc` file:

    max-line-length = {{ cookiecutter.line_length }}

## execution

```bash
python3 -m pip install --user cookiecutter

```

`directory structure`

```bash
$tree . -a
.
├── .gitignore
├── README.md
├── cookiecutter.json
└── project-cc-template
    └── {{ cookiecutter.project_slug }}
        ├── .black
        ├── .flake8
        ├── .isort.cfg
        ├── .pylintrc
        └── pyproject.toml
```

- [cookiecutter docs](https://cookiecutter.readthedocs.io/en/stable/installation.html)