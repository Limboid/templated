# Templated

Templated provides a painless experience for developers looking to build semantic templated functions. With Templated, you can easily define a function with a Jinja2 template string, and use it to generate outputs with dynamic data passed as function arguments.

## Installation

Templated can be installed via pip:

```sh
pip install templated
```

## Usage

Here is an example of how to use Templated:

```python
from templated import Function

f = Function("Hello, {{name}}!")
result = f(name="world")
print(result)
```

The output of the above code will be:

```
Hello, world!
```

In this example, we have defined a function `f` with a Jinja2 template string `"Hello, {{name}}!"`. We then called this function with an argument `name="world"`, which filled in the `{{name}}` placeholder in the template, resulting in the output `"Hello, world!"`.

### Stateful Template Arguments

In Templated, you can also define stateful template arguments. Here is an example:

```python
f = Function("{{greeting}}, {{name}}!")
f(greeting="Hello")
f(name="world")
# Output: "Hello, world!"

f(greeting="Goodbye")
f()
# Output: "Goodbye, world!"
```

In this example, we have defined a function `f` with a Jinja2 template string `"{{greeting}}, {{name}}!"`. We then called this function with an argument `greeting="Hello"`, which filled in the `{{greeting}}` placeholder in the template. We then called the function again with an argument `name="world"`, which filled in the `{{name}}` placeholder in the template, resulting in the output `"Hello, world!"`.

We then called the function again with a different value for the `greeting` argument, `"Goodbye"`. We did not pass a value for the `name` argument, so it retained its previous value of `"world"`. This resulted in the output `"Goodbye, world!"`.

### Custom Language Models

In Templated, you can also use custom language models for generating output from templates. Here is an example:

```python
from langchain.chat_models import ChatOpenAI
from templated._utils.chat2vanilla_lm import Chat2VanillaLM
from templated.function import Function

LLMChatOpenAI = Chat2VanillaLM(ChatOpenAI)
f = Function("Hello, {{name}}!", llm=LLMChatOpenAI)
result = f(name="world")
print(result)
```

In this example, we have defined a custom language model `LLMChatOpenAI` that wraps a `ChatOpenAI` language model. We then defined a function `f` with a Jinja2 template string `"Hello, {{name}}!"`, and passed our custom language model as the `llm` argument to the `Function` constructor.

## Contributing

We welcome contributions to Templated! Please refer to the [contributing guidelines](CONTRIBUTING.md) for more information.

### Tests

```bash
poetry run py.test --doctest-modules
```

## License

Templated is licensed under our [Modified MIT License](LICENSE).