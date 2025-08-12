# Vibe Python

A Python package that executes Python code using OpenAI API and returns command line results.

## Features

- 🚀 Execute Python code through OpenAI API
- ⚙️ Configurable API settings (API key, model, URL, temperature)
- 🏠 Local execution fallback option
- 🧪 Full pytest test suite
- 📦 Easy pip installation
- 🔧 Command line interface

## Installation

```bash
pip install vibepygo
```

Or install from source:

```bash
git clone https://github.com/qqqqqf-q/vibe_pygo.git
cd vibepygo
pip install .
```

## Quick Start

```python
import vibe_python

# Configure API settings
vibe_python.set_api_key("your_api_key_here")
vibe_python.set_model("gpt-4")
vibe_python.set_api_url("https://api.openai.com/v1")

# Execute Python code
result = vibe_python.run_vibe("print('Hello, World!')")
print(result)  # Output: Hello, World!
```

## Configuration

### Environment Variables

You can set configuration using environment variables:

```bash
export OPENAI_API_KEY="your_api_key_here"
export OPENAI_MODEL="gpt-4"
export OPENAI_API_URL="https://api.openai.com/v1"
```

### Programmatic Configuration

```python
import vibe_python

# Set API key
vibe_python.set_api_key("your_api_key_here")

# Set model name
vibe_python.set_model("gpt-4")

# Set API URL (for custom endpoints)
vibe_python.set_api_url("https://api.openai.com/v1")

# Set temperature (0.0 to 2.0)
vibe_python.set_temperature(0.7)

# Get current configuration
config = vibe_python.get_config()
print(config.get_config_dict())
```

## Usage Examples

### Execute Code String

```python
import vibe_python

# Configure
vibe_python.set_api_key("your_key")
vibe_python.set_model("gpt-4")

# Simple calculation
code = """
x = 10
y = 20
print(f"Sum: {x + y}")
"""
result = vibe_python.run_vibe(code)
print(result)  # Output: Sum: 30
```

### Execute Python File

```python
import vibe_python

# Configure
vibe_python.set_api_key("your_key")

# Execute a Python file
result = vibe_python.run_vibe("my_script.py")
print(result)
```

### Local Execution

```python
import vibe_python

# Execute locally without using OpenAI API
result = vibe_python.run_vibe("print('Local execution')", use_local=True)
print(result)
```

### Error Handling

```python
import vibe_python

# Code with error
error_code = "print(undefined_variable)"
result = vibe_python.run_vibe(error_code)
print(result)  # Will show the error message
```

## Command Line Interface

```bash
# Execute a Python file
vibepygo script.py

# With custom settings
vibepygo script.py --api-key your_key --model gpt-4

# Local execution
vibepygo script.py --local

# Custom API URL
vibepygo script.py --api-url https://custom-api.com/v1
```

## Configuration Options

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `api_key` | str | None | OpenAI API key |
| `model_name` | str | "gpt-5-mini" | Model to use |
| `api_url` | str | "https://api.openai.com/v1" | API endpoint URL |
| `temperature` | float | 0.1 | Sampling temperature (0.0-2.0) |
| `max_tokens` | int | 4096 | Maximum tokens in response |

## Testing

Run the test suite:

```bash
pytest tests/ -v
```

Test with your own settings:

```python
import vibe_python

# Configure with your settings
vibe_python.set_api_key("your_key")
vibe_python.set_model("gpt-4")
vibe_python.set_temperature(0.5)

# Test simple code
result = vibe_python.run_vibe("""
import math
print(f"Square root of 16: {math.sqrt(16)}")
for i in range(3):
    print(f"Count: {i}")
""")
print(result)
```

## Advanced Usage

### Custom Temperature Settings

```python
import vibe_python

# Set different temperature values for different use cases
vibe_python.set_temperature(0.0)  # Deterministic output
result1 = vibe_python.run_vibe("print('Deterministic')")

vibe_python.set_temperature(1.0)  # More creative output
result2 = vibe_python.run_vibe("print('Creative')")
```

### Batch Processing

```python
import vibe_python

# Configure once
vibe_python.set_api_key("your_key")
vibe_python.set_model("gpt-4")

# Process multiple files
files = ["script1.py", "script2.py", "script3.py"]
results = []

for file in files:
    try:
        result = vibe_python.run_vibe(file)
        results.append({"file": file, "result": result, "success": True})
    except Exception as e:
        results.append({"file": file, "error": str(e), "success": False})

# Print results
for r in results:
    print(f"{r['file']}: {'✓' if r['success'] else '✗'}")
```

## Error Handling

The package handles various error types:

- **API Key Issues**: Invalid or missing API key
- **Network Errors**: Connection problems
- **Code Execution Errors**: Python syntax or runtime errors
- **Timeout Errors**: Code execution timeout (30 seconds for local execution)

## Requirements

- Python 3.7+
- openai>=1.0.0
- requests>=2.25.0

## License

MIT License

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## Todos

 - Add streaming output