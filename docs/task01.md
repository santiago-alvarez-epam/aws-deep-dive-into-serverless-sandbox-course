# Task01 - Hello World Lambda Function

## Generate project files

```bash
syndicate generate project --name "task01" --path .
```

Output:

```bash
Project name: task01
Project path: .
```

## Creating configuration files for environment

```bash
cd task01
syndicate generate config --name "dev" \           
    --region "eu-central-1" \
    --bundle_bucket_name "syndicate-education-platform-custom-sandbox-artifacts-sbox02/b2cc4bb2" \
    --prefix "cmtr-b2cc4bb2-" \
    --extended_prefix True \
    --iam_permissions_boundary "arn:aws:iam::905418349556:policy/eo_role_boundary" \
    --access_key $AWS_ACCESS_KEY \
    --secret_key $AWS_SECRET_KEY \
    --session_token $AWS_SESSION_TOKEN
```

Output:

```bash
2024-05-09 21:26:16,048 [WARNING] USER:santiago_alvarez generator.py:93:generate_configuration_files LOG: The "project_path" property is not specified. The working directory will be used as a project path. To change the path, edit the syndicate.yml by path /Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev
2024-05-09 21:26:16,056 [INFO] USER:santiago_alvarez generator.py:155:generate_configuration_files LOG: Syndicate initialization has been completed. 
Set SDCT_CONF:
Unix: export SDCT_CONF="/Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev"
Windows: setx SDCT_CONF /Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev
```

Execute:

```bash
export SDCT_CONF="/Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev"
```

## Creating lambda files

```bash
syndicate generate lambda --name "hello_world" --runtime "python" --project_path .
```

Output:

```bash
Configuration used: /Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev
Lambda names: ('hello_world',)
Runtime: python
Project path: .
2024-05-09 21:35:17,929 [INFO] USER:santiago_alvarez lambda_function.py:146:generate_lambda_function LOG: Lambda hello_world has been successfully added to the project.
```

## Deployment

```bash
syndicate create_deploy_target_bucket
syndicate build
syndicate deploy
```

Output:

```bash
# syndicate create_deploy_target_bucket
Configuration used: /Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev
Create deploy target sdk: syndicate-education-platform-custom-sandbox-artifacts-sbox02
Deploy target bucket was created successfully

# syndicate build
Configuration used: /Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev
Running tests...
test_success (test_hello_world.test_success.TestSuccess) ... ok

----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
Tests passed.
Building artifacts, bundle: task01_240509.213800
Command assemble python: project_path: src 
Looking in indexes: https://artifactory.solutions.corelogic.com/artifactory/api/pypi/clgx-pypi-snapshot-libs-virtual/simple, https://pypi.org/simple
Python artifacts were prepared successfully.
Package meta, bundle: task01_240509.213800
Meta was configured successfully.
Upload bundle: task01_240509.213800
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2/2 [00:01<00:00,  1.41nap/s]
Bundle was uploaded successfully

# syndicate deploy
Configuration used: /Users/santiago_alvarez/Learning/aws-deep-dive-into-serverless-sandbox-course/task01/.syndicate-config-dev
2024-05-09 21:39:20,295 [INFO] USER:santiago_alvarez helper.py:240:resolve_default_value LOG: Resolved value of deploy_name: task01
2024-05-09 21:39:21,464 [INFO] USER:santiago_alvarez helper.py:240:resolve_default_value LOG: Resolved value of bundle_name: task01_240509.213800
2024-05-09 21:39:26,058 [INFO] USER:santiago_alvarez deployment_processor.py:85:_process_resources LOG: Processing iam_policy resources
2024-05-09 21:39:27,587 [INFO] USER:santiago_alvarez deployment_processor.py:85:_process_resources LOG: Processing iam_role resources
2024-05-09 21:39:32,648 [INFO] USER:santiago_alvarez deployment_processor.py:97:_process_resources LOG: Processing lambda resources
2024-05-09 21:39:39,265 [INFO] USER:santiago_alvarez deployment_processor.py:348:create_deployment_resources LOG: AWS resources were deployed successfully
2024-05-09 21:39:39,265 [INFO] USER:santiago_alvarez deployment_processor.py:353:create_deployment_resources LOG: Dynamic changes were applied successfully
2024-05-09 21:39:39,279 [INFO] USER:santiago_alvarez group_tagging_api_resource.py:62:apply_tags LOG: No tags are specified in config. Skipping...
2024-05-09 21:39:39,280 [INFO] USER:santiago_alvarez deployment_processor.py:358:create_deployment_resources LOG: Going to create deploy output
2024-05-09 21:39:41,165 [INFO] USER:santiago_alvarez deployment_processor.py:364:create_deployment_resources LOG: Deploy output for task01 was created.
Backend resources were deployed.
```
