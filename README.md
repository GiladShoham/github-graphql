# github-graphql
A working example of https://bitsrc.io/giladshoham/github-graphql

This project aimed to show how you can use components created by bit using npm.  
This example show how quickly you can start working with react, apollo and graphql against GitHub graphql API.  
You can read the full context in this post: 

# Generate GitHub access token
To run this project you will have to generate a github token to access GitHub API.  
Read here: [creating-a-personal-access-token-for-the-command-line](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
# Running the project
Copy the generated token into `./src/App.js` instead of the 'YOUR TOEKN HERE' string  

```bash
npm i
npm start
```

# Modifying the component from this project
We installed the components from bit's registry and everything worked great, but now we have a bug or maybe we just want to change one of the components.
Of course we don't want to go to the original project but just change it from here.
Let's see how it works.
let's assume, we want to add the repo's labels list to our app.
```bash
# bring the component source code into your project
bit import giladshoham.github-graphql/queries/repo-info-issues
```
you can now see the source code under components/queries/repo-info-issues
open the `index.js` file and let's add the following code right below nameWithOwner:
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
Of course we need to change also our react component to present this list.
Let's import the react component as well.
```bash
# bring the component source code into your project
bit import giladshoham.github-graphql/react/repo-info-issues
```
you can now see the source code under components/react/repo-info-issues
now let's add the labels list to our react component.
under the issues ul add this:

```html
<ul style={{'listStyleType': 'none'}}>
  { repository.labels.edges.map( label => (
    <li style={{'textAlign': 'left', 'color':`#label.node.color`}} key={label.node.name}>{label.node.name}
    </li>) ) }
</ul>
```
now let's compile the new code:
```bash
bit build
```
As you can see, you don't have to install anything special, bit just knows to install everything needed for compiling the component.
now let's run the project
```bash
npm start
```
As you can see you have the new component rendered correctly.

The last step is to tag and export the modified components back to bitsrc.io, so you can use the updated version from any other project.
all you have to do is:
```bash
# see our status
bit status
# tag a new version of the modified components
bit tag -am "added labels list"
# export back to bitsrc.io
bit export [USERNAME.SCOPENAME]
```



