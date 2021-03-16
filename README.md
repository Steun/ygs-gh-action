# ygs-gh-action

This action is created to handle the deployment of a project on the Yummygum Staging Server.

This action currently prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

| Input          | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| `who-to-greet` | **Required** The name of the person to greet. Default `"World"`. |

## Outputs

| Output | Description              |
| ------ | ------------------------ |
| `time` | The time we greeted you. |

## Example usage

```yaml
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - name: Hello world action step
        id: hello
        uses: Steun/ygs-gh-action@v1
        with:
          who-to-greet: 'Big Tuna'
      # Use the output from the `hello` step
      - name: Get the output time
        run: echo "The time was ${{ steps.hello.outputs.time }}"
```

# Development

Install the dependencies using Yarn or NPM.

```shell
npm install
# OR
yarn
```

# Deployment

GitHub actions require you to push (compiled) `node_modules`. You can read more about this [here](https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action#commit-tag-and-push-your-action-to-github).

To deploy a new version of this GitHub Action, you need to compile the node modules to `dist/index.js` using `@versel/ncc`. Install it by running:

```shell
npm i -g @vercel/ncc
# OR
yarn add -g @vercel/ncc
```

Now we can build a new version using `npm run build` or `yarn build`.

It's best practice to also add a version tag for releases of your action. For more information on versioning your action, see "[About actions](https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/about-actions#using-release-management-for-actions)."

If you want to deploy version `@v1` you can run:

```shell
git tag -a -m "My action release" v1
git push --follow-tags
```
