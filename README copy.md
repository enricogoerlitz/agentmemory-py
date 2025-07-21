# AgentMemory Package

[![CI](https://github.com/enricogoerlitz/agentmemory-py/actions/workflows/ci.yml/badge.svg)](https://github.com/enricogoerlitz/agentmemory-py/actions/workflows/ci.yml)
[![release](https://github.com/enricogoerlitz/agentmemory-py/actions/workflows/release.yml/badge.svg)](https://github.com/enricogoerlitz/agentmemory-py/actions/workflows/release.yml)

## Description

- implementiert ein datenmodell für agentmemory longterm und shortterm
    - persona
    - conversation
    - conversation_items
    - workflows
    - workflow_items

- bietet cache an


## Get started

### Install package

```bash
$ pip install agentmemory-py
or
$ uv add agentmemory-py
```

### Quick start

**Create memory object**

```python
from agentmemory import AgentMemory
from agentmemory.connection import AgentMemoryConnection
from agentmemory.connection.longterm import MongoDBConnection
from agentmemory.connection.shortterm import RedisConnection

con = AgentMemoryConnection(
    longterm_con=MongoDBConnection(
        mongo_uri="mongodb://localhost:27017",
        database="support-agentmemory"
    ),
    shortterm_con=RedisConnection(
        host="localhost"
    )
)

memory = AgentMemory("support-agentmemory", con=con)
```

#### Conversations

**Create Conversation**

```python
from agentmemory.schema.conversations import Conversation

conversation = Conversation(
    title="New Conversation",
)

created_conversation = memory.conversations.create(conversation)

print(created_conversation)
```


**List Conversations**

```python
# Get all
conversations = memory.conversations.list()

# Get 5 conversations
conversations = memory.conversations.list(limit=5)

# Query conversations
conversations = memory.conversations.list(query={"title": "title1"})
```


**Get and Update Conversation**

```python
id = "<ID>"
conversation = memory.conversations.get(id)

conversation.title = "Updated title"

memory.conversations.update(conversation)
```


**Delete Conversation**

```python
id = "<ID>"
memory.conversations.delete(id)
```

#### ConversationItems


#### Persona


#### Workflow


#### WorkflowSteps


### Custom Caching

```python
memory.cache.keys("*")
memory.cache.get("<KEY>")
memory.cache.set("<KEY>", "value")
memory.cache.clear("<PATTERN>")
```
