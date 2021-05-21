# Setting up Poetry for your project

Poetry is a dependency management and packaging tool that lets you declare libraries in your projects and install/update at will. The dependency management will be similar to Ruby and yarn with `pyproject.toml` \(python dependencies\) and `poetry.lock` \(python packages with hashes\).

## Installation:

* Recommended method is to run: `curl -sSL https://raw.githubusercontent.com/sdispater/poetry/master/get-poetry.py | python`. This adds `.poetry` folder in your system. \(Tested for Mac and Linux based systems\)
* Next step is to add: `source $HOME/.poetry/env` to `.bashrc` or `.zshrc`
* `poetry --version` should provide you with the version required
* The other way is to `pip install --user poetry`. This will directly install poetry, no need for adding anything to `.bashrc` or `.zshrc`.

## Setting up poetry for a project:

* First thing that you'd want to do is run: `poetry init` for the project you'd want this setup to work.
* The setup commands would look as below:

![poetry-setup](../.gitbook/assets/poetry-setup.png)

* Once done, a `pyproject.toml` file would be generated. This will contain all the information related to the project, dependencies, dev-dependencies, build setup and poetry scripts \(more on poetry scripts later\)
* A standard `pyproject.toml` looks as follows:

```bash
[tool.poetry]
name = "test_app"
version = "0.1.0"
description = "Test api"
authors = ["Prathamesh Sarang <prathamesh@difference-engine.ai>"]

[tool.poetry.dependencies]
python = "3.7.3"
torch = "^1.3.0"
flask = "^1.1.1"
requests = "^2.22.0"
antspyx = "^0.2.2"
loguru = "^0.3.2"
torchvision = "^0.4.1"
simplejson = "^3.16.0"
opencv-python = "^4.1.1"

[tool.poetry.scripts]
train_mnist = "test_app.train.train_mnist:main"
client = "test_app.api_v1.client:run"
server = "test_app.api_v1.api:app"

[tool.poetry.dev-dependencies]
black = {version = "^19.3b0", allows-prereleases = true}
isort = "^4.3.21"
autoflake = "^1.3.1"
pytest = "^5.2.1"
jupyter = "^1.0.0"
flake8 = "^3.7.8"

[build-system]
requires = ["poetry>=0.12"]
build-backend = "poetry.masonry.api"
```

## Adding python packages:

* To add any python packages, the only command you need is: `poetry add <package-name>`. 
* To remove any python packages, it is as simple as: `poetry remove <package-name>`.
* You can search for packages as well, `poetry search <package-name>`.
* Once added, `poetry.lock` file would be generated that contains information about package:

  ```text
  [[package]]
  category = "main"
  description = "Advanced Normalization Tools in Python"
  name = "antspyx"
  optional = false
  python-versions = "*"
  version = "0.2.2"
  ```

and information of the version in metadata hashes:

```text
[metadata]
content-hash = "4979fafad1b359d661b8b925285826525a24f513d723415c4516f7108879c5c0"
python-versions = "3.7.3"

[metadata.hashes]
antspyx = ["93b9f54dfcae403b64bd4c52e7a237e3c3ab6c78bb86d244807bfedae4c403f5", "a8007c6dbd031d5c8497f23a68f8fed0d2a47814187d5ee34053a71c6efc0a7a", "c2bc9870c773a730f7bc703fbbbfbb4ff4a413ec8d42eaafe111511a21e95ff0"]
```

## Running python scripts using poetry:

* `poetry run python` will provide you with python shell required. 
* `poetry run python app.py` will run the python script for you.
* But you'd want to be smart about things! Poetry lets you be smart with poetry scripts.
* In `pyproject.toml`, you can add a section `[tool.poetry.scripts]` wherein you can add paths and functions that need to be run. 
* For example, you want to run a flask server with `app` initialized in `project-name/api/v1/server.py`. Add the following:

  ```text
  [tool.poetry.scripts]
  webserver = "project-name.api.v1.server:app"
  ```

* Run `poetry run webserver` and voila, you have a local Flask server running!
* Similarly you can run, linting and other cool services using poetry scripts.

## Building and publishing python packages \[TODO\]:

## Cookie-cutter projects with poetry setup \[TODO\]:

