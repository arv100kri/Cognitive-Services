<!--
NavPath: KES
LinkLabel: Getting Started
Url: KES/documentation/start
Weight: 100
-->

# Getting Started
To allow the Dialog Engine to use your data, it should be organized as a collection of entities. Each entity has a collection of attributes. An attribute has a name and a value, such as a number, a text string, etc.
The Dialog Engine does not distinguish between different types of entities, but you can have some entities that have one set of attributes, and other entities with a different set of attributes, and these can all be part of a single collection of entities.

To use the Dialog Engine, you need to follow these steps:
1. Create a schema that describes the attributes of your entities. This is a JSON file.
2. Create entity data following the schema. This is a text file where each line is in JSON format.
3. Use the Index Builder to build an index from the schema and entity data. This creates a binary index file.
4. Create a grammar that describes how user input is parsed and translates it into index queries. The grammar file is an XML file in a format that is based on the SRGS standard.
5. Run the Dialog Engine web service to parse user queries
  * Can get completions
  * Can get matching entities
