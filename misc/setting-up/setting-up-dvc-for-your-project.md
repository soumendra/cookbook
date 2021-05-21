# Setting up DVC for your project

## Installation

* For usage in any repository/project, one needs to add it via `pip install dvc` or if using poetry: `poetry add dvc`
* It is likely that you'd want to use it with remote connection. In this repository we are using `s3` as the remote location where all the _dvc pushed files_ will be stored.
* To add `s3` plugin, use:
  * Via `pip`: `pip install dvc[s3]`
  * Via `poetry`: `poetry add dvc --extras "s3"`

## Setting up DVC in your repository/project

* Once you have followed the steps above, run: `dvc init` to initialize DVC for system. You'll get the following output

![](../.gitbook/assets/dvc-init.png)

* Next step is to setup S3 buckets required, consider if you have a bucket named: `project-data` and inside that two folders: `data` and `models`
* After `dvc init`, a folder called `.dvc` will be created with `.dvc/config` file present.
* We need to add the remote s3 bucket to `config` using:
  * Remote data folder: `dvc remote add -d project-data s3://project-data/data`
  * Remote models folder: `dvc remote add -d project-models s3://project-data/models`
* Along with the remote links, we also need to add s3 credentials and region \(optional\)
* Create a `s3_credentials` file as follows \(save it to folder you want\):

  ```bash
  [default]
  aws_access_key_id=12313123adasdas
  aws_secret_access_key=asda8d713dasdhasd
  ```

* Add region using the following commands:
  * `dvc remote modify project-data region us-east-1`
  * `dvc remote modify project-models region us-east-1`
* So that DVC can access the s3 credentials, add:
  * `dvc remote modify project-data credentialpath ./s3_credentials`
  * `dvc remote modify project-models credentialpath ./s3_credentials`
* DVC has a lot of configs, but two things suggested to be used are:
  * `dvc config core.loglevel info`: Used for dvc logging
  * `dvc config core.analytics false`: _To help better understand how DVC is used and improve it, DVC captures and reports anonymized usage statistics._ Turn it off for sensitive data.
* Finally, your `.dvc/config` file should look like:

  ```bash
  ['remote "project-models"']
  url = s3://etl-out/project-models
  region = us-east-1
  credentialpath = ./s3_credentials
  [core]
  loglevel = info
  analytics = false
  ['remote "project-data"']
  url = s3://etl-out/project-data
  region = us-east-1
  credentialpath = ./s3_credentials
  ```

* To check remote location list, run: `dvc remote list`

![](../.gitbook/assets/dvc-list1.png)

## Pushing files to DVC remote

* To add files for tracking use: `dvc add data/data.zip`
* After running the above command, a `data.zip.dvc` file will be generated. The contents of the file would be of the the type:

```bash
md5: 48a015ad905cb8947eaeee259eec4fb8
outs:
- md5: 9bc20a696092024abe52696ee6c5837f
  path: data.zip
  cache: true
  metric: false
  persist: false
```

* For purpose of tracking these files via `git`, we'll only add the `*.dvc` files in our repo: `git add data/*.dvc`
* To actually push the data to remote S3, run the command: `dvc push --remote project-data data/*.dvc`. 

![](../.gitbook/assets/dvc-push.png)

## Pulling files to local via DVC remote

* It is as simple as, cloning the `git` repository and doing a `dvc pull`
* **NOTE:** `dvc pull` will download all the folders to your local. If you want to download a very specific file, run: `dvc pull --remote project-data data.zip`

This document provides bare minimum information for setting up DVC and working with AWS S3. For more detailed understanding, please read the [DVC documentation](https://dvc.org/doc/get-started)

