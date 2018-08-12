# React Apollo Snippet Library

This snippet library is currently geared at users of `apollo-boost`. If you're setting things up the old way and would like to add a snippet or two feel free to make suggestions or toss up a PR. If anyone has any suggestions whatsoever on anything I've done here let me know. I tried to create a few useful snippets for common React Apollo patterns I kept running into, but things can always be better :)

# Commands
## App Set Up

### `abc` ( Apollo Boost Client )

```javascript
import ApolloClient from "apollo-boost"

const client = new ApolloClient({
  uri: "endpoint"
});
```

### `abcc` (Apollo Boost Client w/ clientState)

```javascript
import ApolloClient from "apollo-boost"

const client = new ApolloClient({
  uri: "endpoint",
  clientState: {
    defaults,
    resolvers,
    typeDefs
  }
});
```

### `aba` (Apollo Boost App w/ Client)

```javascript
import React from "react";
import { render } from "react-dom";
import { ApolloProvider } from "react-apollo";
import ApolloClient from "apollo-boost"

const client = new ApolloClient({
	uri: "endpoint"
});

const App = () =>
  <ApolloProvider client={client}>
    <div></div>
  </ApolloProvider>

render(<App/>, document.getElementById("root"));
```

## Elements / Pieces

### `gql` ( GraphQL query/mutation variable )

```javascript
const MY_QUERY = gql`

`;
```

### `qc` ( Query Component )

```javascript
<Query
  query={ MY_QUERY }
  variables={{}}>
  {({ data, loading, error, refetch, networkStatus }) => {
      if (loading) return 'Loading';
      if (error) return `Error!: ${error}`;
      return (
        <div> </div>
      )
  }}
</Query>
```
### `mc` ( Mutation Component )
```javascript
<Mutation
	mutation={ MY_MUTATION }>
  {(mutationFunc, { data, loading, called, error }) => {
    return (
      <div>
        <button onClick={(e)=>{
          e.preventDefault();
          mutationFunc({
            variables: { }
          })
        }}/>
      </div>
    )
  }}
</Mutation>
```
### `ac` ( ApolloConsumer Component )
```javascript
<ApolloConsumer>
	{ client => (
	  <div>
	    <button
	      onClick={async () => {
	        const { data } = await client.query({
	          query: MY_QUERY,
	          variables: { }
	        });
	      }}
	    />
	  </div>
	)}
</ApolloConsumer>
```
### `or` ( optimisticResponse )
```javascript
optimisiticResponse: {
	__typeName: "Mutation",
	updateThing: {
	  id: "",
	  __typeName: "Thing",
	  content: "Lowered expectations"
	}
}
```

## Components
### `qcc` ( React Class Component w/ Query )
```javascript
import React, { Component } from "react";
import { Query } from "react-apollo";
import { gql } from 'apollo-boost';

export default class MyComponent extends Component {
  render(){
    return (
      <Query
        query={MY_QUERY}>
        {({ data, loading, error, refetch, networkStatus }) => {
          if (loading) return 'Loading';
          if (error) return `Error!: ${error}`;
          return (
            <div> MyComponent </div>
          )
		  }}
	  </Query>
    )
  }
}

const MY_QUERY = gql`
  query {

  }
`;
```
### `qcf` ( React Functional Component w/ Query )
```javascript
import React from "react";
import { Query } from "react-apollo";
import { gql } from 'apollo-boost';

const MyComponent = (props) => {
  return (
    <Query
      query={MY_QUERY}>
      {({ data, loading, error, refetch, networkStatus }) => {
        if (loading) return 'Loading';
        if (error) return `Error!: ${error}`;
        return (
          <div> MyComponent </div>
        )
		  }}
  	</Query>
  )
}

const MY_QUERY = gql`
  query {

  }
`;
```
### `mcc` ( React Class Component w/ Mutation )
```javascript
import React, { Component } from "react";
import { Mutation } from "react-apollo";
import { gql } from 'apollo-boost';

export default class MyComponent extends Component {
  render(){
    return (
      <Mutation
        mutation={ ${2:MY_MUTATION} }>
        {(mutationFunc, { data, loading, called, error }) => {
          return (
            <div>
              <button onClick={(e)=>{
                e.preventDefault();
                mutationFunc}({
                  variables: { }
                })
              }}/>
            </div>
          )
        }}
      </Mutation>
    )  
  }
}

const MY_MUTATION = gql`
  mutation {

  }
`;
```
### `mcf` ( React Functional Component w/ Mutation )
```javascript
import React from "react";
import { Mutation } from "react-apollo";
import { gql } from 'apollo-boost';

const MyComponent = (props) => {
  return (
    <Mutation
      mutation={ ${2:MY_MUTATION} }>
      {(mutationFunc, { data, loading, called, error }) => {
        return (
          <div>
            <button onClick={(e)=>{
              e.preventDefault();
              mutationFunc}({
                variables: { }
              })
            }}/>
          </div>
        )
      }}
    </Mutation>
  )
}

const MY_MUTATION = gql`
  mutation {

  }
`;
```
### `acc` ( React Functional Component w/ ApolloConsumer )
```javascript
import React from "react";
import { ApolloConsumer } from "react-apollo";
import { gql } from 'apollo-boost';

const MyComponent = (props) => {
  return (
    <ApolloConsumer>
      { client => (
        <div>
          <button
            onClick={async () => {
              const { data } = await client.query({
                query: MY_QUERY,
                variables: { }
              });
            }}
          />
        </div>
      )}
    </ApolloConsumer>
  )
}

export default MyComponent;
```
### `acf` ( React Class Component w/ ApolloConsumer )
```javascript
import React, { Component } from "react";
import { ApolloConsumer } from "react-apollo";
import { gql } from 'apollo-boost';

export default class MyComponent extends Component {
  render(){
    return (
      <ApolloConsumer>
        { client => (
          <div>
            <button
              onClick={async () => {
                const { data } = await client.query({
                  query: MY_QUERY,
                  variables: { }
                });
              }}
            />
          </div>
        )}
       </ApolloConsumer>
    )
  }
}
```
## Imports
### `igql` ( import gql )
```javascript
import { gql } from "apollo-boost";
```
### `iqc` ( import Query component )
```javascript
import { Query } from "react-apollo";
```
### `imc` ( import Mutation component )
```javascript
import { Mutation } from "react-apollo"
```
### `iap` ( import ApolloProvider )
```javascript
import { ApolloProvider } from "react-apollo"
```
### `icg` ( import compose, graphql )
```javascript
import { compose, graphql } from "react-apollo";
```
### `ig` ( import graphql )
```javascript
import { graphql } from "react-apollo";
```
## Exports
### `edc` ( export default Compose, GraphQL )
```javascript
export default compose(
  graphql(MY_QUERY)
)(MyComponent)
```
### `edg` ( export default GraphQL )
```javascript
export default graphql(MY_QUERY)(MyComponent)
```
