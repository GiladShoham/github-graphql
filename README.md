# github-graphql

A working example of https://bitsrc.io/giladshoham/github-graphql

This project demonstrates how components shared with Bit and installed with NPM can be easily modified right from the consuming project's context.

This example also shows how quickly you can start using react, apollo and graphql with GitHub graphql API.  

Inside this project you can find components from GitHub's Graphql API installed with NPM after being shared from [this source project](https://github.com/GiladShoham/github-graphql-template).

Let's go through the simple workflow of making changes to these NPM packages' source code right from this project's context.

# 1. Generate GitHub access token

To run this project you will have to generate a github token to access GitHub’s API: [creating-a-personal-access-token-for-the-command-line](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).

# 2. Running the project

Copy the generated token into `./src/App.js` instead of the 'YOUR TOEKN HERE' string  and run the project.

```bash
npm i
npm start
```

# 3. Modifying the component from this project

We installed the components using NPM from bit's registry and everything worked great, but now we might have a bug or maybe we just want to change one of the components.

Naturally,  we really don't want to go to the original project just to change the code. Instead, let’s change it right from this project.

let's assume, we want to add the repo's labels list to our app 

First, let’s [initialize Bit](https://docs.bitsrc.io/docs/initializing-bit.html) for the project. (Don’t forget to [install Bit](https://docs.bitsrc.io/)!)

```bash
$ cd github-graphql 
$ bit init
```
Now, let’s use `bit import` the bring the component’s source code into this project
```bash
# bring the component source code into your project
bit import giladshoham.github-graphql/queries/repo-info-issues
```
you can now see the source code under components/queries/repo-info-issues
open the `index.js` file - let's add the following code right below nameWithOwner:
```
labels (last:10) {
  edges {
    node {
      name,
      color
    }
  }
}
```
This will change our query and add a list of 10 labels.

Now, we will also need to change also our react component to present this list.
Let's import the react component as well.

```bash
# bring the component source code into your project
bit import giladshoham.github-graphql/react/repo-info-issues
```
You can now see the source code under components/react/repo-info-issues. 
To add the labels list to our react component, let’s add this under the issues ul:

```html
<ul style={{'listStyleType': 'none'}}>
  { repository.labels.edges.map( label => (
    <li style={{'textAlign': 'left', 'color': `#${label.node.color}`}} key={label.node.name}>{label.node.name}
    </li>) ) }
</ul>
```
now let's compile the new code:

```bash
bit build
```
As you can see, you don't have to install anything special. Bit automatically installs everything needed for compiling the component.

Now let's run the project.

```bash
npm start
```
As you can see you have the new component rendered correctly.

The last step is to tag and export the modified components with Bit, so you can use it to update a version from any other project.

all you have to do is:
```bash
# see our status
bit status
# tag a new version of the modified components
bit tag -am "added labels list"
# export back to bitsrc.io
bit export [USERNAME.SCOPENAME]
```

And that’s it!
