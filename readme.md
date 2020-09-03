

`npx swagger-to-graphql --swagger-schema=/path/to/swagger_schema.json > ./types.graphql`

```part of swagger.json
  {
		 "parameters": [
          {
            "in": "body",
            "name": "body",
            "description": "Pet object that needs to be added to the store",
            "required": true,
            "schema": {
              "$ref": "#/definitions/Pet"
            }
          }
        ],
        "responses": {
          "405": {
            "description": "Invalid input"
          }
        },
	}
```

covert to schema

```part of grapqhl schema
input PetInput {
  id: String
  category: CategoryInput
  name: String!
  photoUrls: [String!]!
  tags: [TagInput!]

  """pet status in the store"""
  status: String
}

type Query {
  """Multiple status values can be provided with comma separated strings"""
  findPetsByStatus(status: [String!]!): [Pet!]!

  """
  Muliple tags can be provided with comma separated strings. Use         tag1, tag2, tag3 for testing.
  """
  findPetsByTags(tags: [String!]!): [Pet!]!

  """Returns a single pet"""
  getPetById(petId: String!): Pet!

  """Returns a map of status codes to quantities"""
  getInventory: JSON!

  """
  For valid response try integer IDs with value >= 1 and <= 10.         Other values will generated exceptions
  """
  getOrderById(orderId: String!): Order!
  loginUser(username: String!, password: String!): String!
  logoutUser: JSON!
  getUserByName(username: String!): User!
}
```