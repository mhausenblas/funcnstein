# funcnstein

![funcnstein logo](img/funcnstein-logo.png)

_Kudos to Ashley McNamara, Renee French, and Mat Ryer for the logo, via [gopherize.me](https://gopherize.me/)._

---

Are you into serverless? Using, for example, [AWS Lambda](https://aws.amazon.com/lambda/) or [knative](https://github.com/knative/serving) or [Apache OpenWhisk](https://openwhisk.apache.org/)? When you're building a non-trivial app based on functions you potentially end up with dozens or hundreds of functions.

How do you manage them? Know what is running, what the dependencies between functions are? Maybe you're manually updating a spreadsheet or perhaps you have put together a nice little shell script that queries the state?

I believe we can do better, better as in great UX, ease of use, and powerful set of operations, but focused on the task of managing functions from an operational point of view. So, you would still use Serverless, CloudFormation, Terraform, or your own tooling to deploy, monitor, or debug your functions.

So this is what the idea of `funcnstein` is: a multi-platform tool for managing functions.

Sample interactions follow below—note, no matter if you're using the CLI tool against Lambda or OpenFaaS or kubeless or whatever target, the UX is always the same:

## Getting an overview of what is running

```bash
$ functl get
NAME                STATUS    INVOCATIONS   AGE
convertimg          Running   21k           42d
myfirstgofunction   Running   300           10m
```

## Examining a specific function

```bash
$ functl describe convertimg
Environment: AWS Lambda
Project: A paying customer, actually
State: Running (since 2018-06-25)
Language: Node.js
Invocations: 20988
Triggers: API Gateway, S3 
Labels: owner=mshelley
```

## Organizing stuff

```bash
$ functl label convertimg stage=prod
Labels: owner=mshelley, stage=prod
```

## Advanced queries

```bash
$ functl get --project='*paying*' --selector='owner=mshelley' --invocations='>20k'
NAME                STATUS    INVOCATIONS   AGE
convertimg          Running   21k           42d
```

## FAQ

Q: How is `functl` pronounced?<br />
A: fun-kuddle
