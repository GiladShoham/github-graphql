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
```bash
# bring the component source code into your project
bit import giladshoham.github-graphql/react/repo-info-issues
```
you can now see the source code under components/react/repo-info-issues
now let's make some change, for example - let's add the text "stars count" before the stars counter:
replace the line:
```html
<span style={{marginRight: '10px'}}> {repository.stargazers.totalCount} </span>
```
with 
```html
<span style={{marginRight: '10px'}}> stars count: {repository.stargazers.totalCount} </span>
```
now let's compilie the new code:
```bash
bit build
```
As you can see, you don't have to install anything special, bit just knows to install everything needed for compiling the component.
now let's run the project
```bash
npm start
```
As you can see you have the new component rendered correctly.

The last step is to export it back to bitsrc.io, so you can use the updated version from any other project.
all you have to do is:
```bash
bit export [USERNAME.SCOPENAME]
```



