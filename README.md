# actions.diy

A [GitHub Action](https://github.com/features/actions) to let you custom your action logic. It's like you can't do anything with it directly but you can do anything with it.(For me, I often use it to verify my prototype, then pub a official version if prototype works.)

## Usage

You can use this action after any other action. Here is an example setup of this action:

1. Create a `.github/workflows/diy.yml` file in your GitHub repo.
2. Add the following code to the `diy.yml` file.

```yml
on: push
name: Do it yourself action
jobs:
  DIY:
    name: Start
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    
    - name: Do it yourself
      uses: echoings/actions.diy@v0.1.0
```

3. Create a `.echo.actions.diy.js` file in your root project, and export an async function which's definition as follow, then **You can handle action logic yourself**

```Typescript
module.exports = async function DIY(
  options: {
    envs: process.env,
    ctx: github.context
  },
  utils: {
    axios: 'axios',
    core: '@actions/core',
    github: '@actions/github',
    exec: '@actions/exec',
    cache: '@actions/cache',
    artifact: '@actions/artifact',
    glob: '@actions/glob',
    io: '@actions/io',
    toolCache: '@actions/tool-cache'
  }
): {
  code?: number,
  data?: any,
  msg: string
}
```

`Tips: ` If you need more extra dependency package, please do and use [ncc](https://github.com/vercel/ncc#readme) to bundle them together.
