# 🧠 Memory Systems API

The memory management system provides multi-layered memory architecture for SuperOptiX agents, supporting episodic, semantic, and working memory with various backend storage options.

## AgentMemory

The main memory manager that coordinates all memory components.

### Constructor

```python
class AgentMemory:
    def __init__(
        self,
        agent_id: str,
        backend: str = "sqlite",
        max_episodes: int = 1000,
        max_context_length: int = 4096,
        retention_days: int = 30,
        **kwargs
    )
```

**Parameters:**
- `agent_id` (str): Unique identifier for the agent
- `backend` (str): Memory backend ("sqlite", "redis", "file") - defaults to "sqlite"
- `max_episodes` (int): Maximum number of episodes to store - defaults to 1000
- `max_context_length` (int): Maximum context length in tokens - defaults to 4096
- `retention_days` (int): Days to retain memory - defaults to 30
- `**kwargs` (Any): Additional backend-specific configuration

### Core Methods

#### store_episode()
```python
def store_episode(
    self,
    episode_id: str,
    user_input: str,
    agent_response: str,
    metadata: Optional[Dict[str, Any]] = None,
    timestamp: Optional[datetime] = None
) -> str:
    """Store an episode in episodic memory."""
```

**Parameters:**
- `episode_id` (str): Unique episode identifier
- `user_input` (str): User's input message
- `agent_response` (str): Agent's response
- `metadata` (Dict[str, Any], optional): Additional episode metadata
- `timestamp` (datetime, optional): Episode timestamp

**Returns:** Episode identifier

#### retrieve_episodes()
```python
def retrieve_episodes(
    self,
    query: Optional[str] = None,
    limit: int = 10,
    include_metadata: bool = True
) -> List[Dict[str, Any]]:
    """Retrieve episodes from memory."""
```

**Parameters:**
- `query` (str, optional): Search query for semantic retrieval
- `limit` (int): Maximum number of episodes to retrieve - defaults to 10
- `include_metadata` (bool): Include metadata in results - defaults to True

**Returns:** List of episode dictionaries

#### store_semantic_memory()
```python
def store_semantic_memory(
    self,
    key: str,
    content: str,
    category: Optional[str] = None,
    metadata: Optional[Dict[str, Any]] = None
) -> str:
    """Store information in semantic memory."""
```

**Parameters:**
- `key` (str): Semantic memory key
- `content` (str): Content to store
- `category` (str, optional): Content category
- `metadata` (Dict[str, Any], optional): Additional metadata

**Returns:** Memory entry identifier

#### retrieve_semantic_memory()
```python
def retrieve_semantic_memory(
    self,
    query: str,
    category: Optional[str] = None,
    limit: int = 5
) -> List[Dict[str, Any]]:
    """Retrieve information from semantic memory."""
```

**Parameters:**
- `query` (str): Search query
- `category` (str, optional): Filter by category
- `limit` (int): Maximum results - defaults to 5

**Returns:** List of semantic memory entries

#### update_working_memory()
```python
def update_working_memory(
    self,
    key: str,
    value: Any,
    ttl: Optional[int] = None
) -> None:
    """Update working memory with temporary information."""
```

**Parameters:**
- `key` (str): Memory key
- `value` (Any): Value to store
- `ttl` (int, optional): Time-to-live in seconds

#### get_working_memory()
```python
def get_working_memory(
    self,
    key: str,
    default: Any = None
) -> Any:
    """Retrieve value from working memory."""
```

**Parameters:**
- `key` (str): Memory key
- `default` (Any): Default value if key not found

**Returns:** Stored value or default

#### get_context()
```python
def get_context(
    self,
    query: Optional[str] = None,
    max_tokens: int = 2048,
    include_episodic: bool = True,
    include_semantic: bool = True,
    include_working: bool = True
) -> str:
    """Get contextual information for agent responses."""
```

**Parameters:**
- `query` (str, optional): Query for relevant context
- `max_tokens` (int): Maximum tokens in context - defaults to 2048
- `include_episodic` (bool): Include episodic memory - defaults to True
- `include_semantic` (bool): Include semantic memory - defaults to True
- `include_working` (bool): Include working memory - defaults to True

**Returns:** Formatted context string

#### clear_memory()
```python
def clear_memory(
    self,
    memory_type: Optional[str] = None,
    older_than_days: Optional[int] = None
) -> int:
    """Clear memory entries."""
```

**Parameters:**
- `memory_type` (str, optional): Type to clear ("episodic", "semantic", "working", "all")
- `older_than_days` (int, optional): Clear entries older than specified days

**Returns:** Number of entries cleared

#### get_memory_stats()
```python
def get_memory_stats(self) -> Dict[str, Any]:
    """Get memory system statistics."""
```

**Returns:** Dictionary with memory statistics

## Memory Components

### EpisodicMemory

Manages conversation history and interaction episodes.

```python
class EpisodicMemory:
    def __init__(self, backend: MemoryBackend, max_episodes: int = 1000)
    
    def store(self, episode_id: str, user_input: str, agent_response: str, 
              metadata: Optional[Dict[str, Any]] = None) -> str
    
    def retrieve(self, query: Optional[str] = None, limit: int = 10) -> List[Dict[str, Any]]
    
    def get_recent(self, limit: int = 5) -> List[Dict[str, Any]]
    
    def clear_old(self, older_than_days: int) -> int
```

### LongTermMemory

Manages persistent knowledge and semantic information.

```python
class LongTermMemory:
    def __init__(self, backend: MemoryBackend)
    
    def store(self, key: str, content: str, category: Optional[str] = None,
              metadata: Optional[Dict[str, Any]] = None) -> str
    
    def retrieve(self, query: str, category: Optional[str] = None, 
                 limit: int = 5) -> List[Dict[str, Any]]
    
    def update(self, key: str, content: str) -> bool
    
    def delete(self, key: str) -> bool
```

### ShortTermMemory

Manages temporary working memory for current session.

```python
class ShortTermMemory:
    def __init__(self, max_context_length: int = 4096)
    
    def update(self, key: str, value: Any, ttl: Optional[int] = None) -> None
    
    def get(self, key: str, default: Any = None) -> Any
    
    def delete(self, key: str) -> bool
    
    def clear(self) -> None
    
    def get_all(self) -> Dict[str, Any]
```

### ContextManager

Coordinates context retrieval and formatting.

```python
class ContextManager:
    def __init__(self, episodic_memory: EpisodicMemory, 
                 long_term_memory: LongTermMemory,
                 short_term_memory: ShortTermMemory)
    
    def get_context(self, query: Optional[str] = None, max_tokens: int = 2048,
                    include_episodic: bool = True, include_semantic: bool = True,
                    include_working: bool = True) -> str
    
    def format_context(self, episodes: List[Dict[str, Any]], 
                       semantic_entries: List[Dict[str, Any]],
                       working_memory: Dict[str, Any]) -> str
```

## Memory Backends

### MemoryBackend

Abstract base class for memory backends.

```python
class MemoryBackend(ABC):
    @abstractmethod
    def store(self, key: str, value: Any, metadata: Optional[Dict[str, Any]] = None) -> str
    
    @abstractmethod
    def retrieve(self, key: str) -> Optional[Any]
    
    @abstractmethod
    def search(self, query: str, limit: int = 10) -> List[Dict[str, Any]]
    
    @abstractmethod
    def delete(self, key: str) -> bool
    
    @abstractmethod
    def clear(self) -> int
```

### SQLiteBackend

SQLite-based memory backend.

```python
class SQLiteBackend(MemoryBackend):
    def __init__(self, db_path: str, table_prefix: str = "memory")
    
    def store(self, key: str, value: Any, metadata: Optional[Dict[str, Any]] = None) -> str
    
    def retrieve(self, key: str) -> Optional[Any]
    
    def search(self, query: str, limit: int = 10) -> List[Dict[str, Any]]
    
    def delete(self, key: str) -> bool
    
    def clear(self) -> int
    
    def get_stats(self) -> Dict[str, Any]
```

### RedisBackend

Redis-based memory backend.

```python
class RedisBackend(MemoryBackend):
    def __init__(self, redis_url: str = "redis://localhost:6379", 
                 db: int = 0, key_prefix: str = "memory")
    
    def store(self, key: str, value: Any, metadata: Optional[Dict[str, Any]] = None) -> str
    
    def retrieve(self, key: str) -> Optional[Any]
    
    def search(self, query: str, limit: int = 10) -> List[Dict[str, Any]]
    
    def delete(self, key: str) -> bool
    
    def clear(self) -> int
    
    def set_ttl(self, key: str, ttl_seconds: int) -> bool
```

### FileBackend

File-based memory backend.

```python
class FileBackend(MemoryBackend):
    def __init__(self, storage_dir: str, file_format: str = "json")
    
    def store(self, key: str, value: Any, metadata: Optional[Dict[str, Any]] = None) -> str
    
    def retrieve(self, key: str) -> Optional[Any]
    
    def search(self, query: str, limit: int = 10) -> List[Dict[str, Any]]
    
    def delete(self, key: str) -> bool
    
    def clear(self) -> int
    
    def backup(self, backup_path: str) -> bool
```

## Example Usage

```python
from superoptix.memory import (
    AgentMemory,
    SQLiteBackend,
    RedisBackend,
    FileBackend
)

# Initialize memory with SQLite backend
memory = AgentMemory(
    agent_id="my_agent",
    backend="sqlite",
    max_episodes=1000,
    max_context_length=4096
)

# Store an episode
episode_id = memory.store_episode(
    episode_id="ep_001",
    user_input="What is the weather like?",
    agent_response="I don't have access to real-time weather data.",
    metadata={"location": "New York", "timestamp": "2024-01-15"}
)

# Store semantic memory
memory.store_semantic_memory(
    key="weather_api",
    content="Weather data can be accessed via OpenWeatherMap API",
    category="apis",
    metadata={"url": "https://openweathermap.org/api"}
)

# Update working memory
memory.update_working_memory(
    key="current_session",
    value={"user_id": "user123", "session_start": "2024-01-15T10:00:00"},
    ttl=3600  # 1 hour
)

# Retrieve context for agent response
context = memory.get_context(
    query="weather information",
    max_tokens=2048,
    include_episodic=True,
    include_semantic=True,
    include_working=True
)

# Retrieve recent episodes
episodes = memory.retrieve_episodes(
    query="weather",
    limit=5,
    include_metadata=True
)

# Retrieve semantic memory
semantic_info = memory.retrieve_semantic_memory(
    query="weather API",
    category="apis",
    limit=3
)

# Get working memory
session_info = memory.get_working_memory("current_session")

# Get memory statistics
stats = memory.get_memory_stats()
print(f"Episodes: {stats['episodic_count']}")
print(f"Semantic entries: {stats['semantic_count']}")
print(f"Working memory keys: {stats['working_count']}")

# Clear old memory
cleared = memory.clear_memory(
    memory_type="episodic",
    older_than_days=30
)
print(f"Cleared {cleared} old episodes")

# Custom backend configuration
sqlite_backend = SQLiteBackend(
    db_path="/path/to/memory.db",
    table_prefix="agent_memory"
)

redis_backend = RedisBackend(
    redis_url="redis://localhost:6379",
    db=1,
    key_prefix="agent_memory"
)

file_backend = FileBackend(
    storage_dir="/path/to/memory/files",
    file_format="json"
)

# Use custom backend
custom_memory = AgentMemory(
    agent_id="custom_agent",
    backend=sqlite_backend,
    max_episodes=500
)
```

## Configuration Options

### SQLite Configuration

```python
sqlite_config = {
    "db_path": "/path/to/memory.db",
    "table_prefix": "memory",
    "max_connections": 10,
    "timeout": 30
}
```

### Redis Configuration

```python
redis_config = {
    "redis_url": "redis://localhost:6379",
    "db": 0,
    "key_prefix": "memory",
    "password": None,
    "ssl": False,
    "timeout": 5
}
```

### File Configuration

```python
file_config = {
    "storage_dir": "/path/to/memory",
    "file_format": "json",  # json, pickle, yaml
    "compression": False,
    "backup_enabled": True
}
```

## Memory Statistics

The memory system provides comprehensive statistics:

```python
stats = memory.get_memory_stats()

# Available statistics
{
    "episodic_count": 150,
    "semantic_count": 45,
    "working_count": 8,
    "total_size_bytes": 2048576,
    "oldest_episode": "2024-01-01T00:00:00",
    "newest_episode": "2024-01-15T10:30:00",
    "backend_type": "sqlite",
    "backend_stats": {...}
}
``` 