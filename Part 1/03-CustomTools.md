## Create Custom Tools

<br>

<b>Application :</b> Currency Converter


```python
from dotenv import load_dotenv
load_dotenv()
```




    True




```python
from crewai.tools import BaseTool

from pydantic import BaseModel, Field
from typing import Type
import requests
import os
```

### Creating Tools


```python
class CurrencyConverterInput(BaseModel):
    """Input schema for CurrencyConverterTool."""
    amount: float = Field(..., description="The amount to convert.")
    from_currency: str = Field(..., description="The source currency code (e.g., 'USD').")
    to_currency: str = Field(..., description="The target currency code (e.g., 'EUR').")


class CurrencyConverterTool(BaseTool):
    name: str = "Currency Converter Tool"
    description: str = "Converts an amount from one currency to another."
    args_schema: Type[BaseModel] = CurrencyConverterInput
    api_key: str = os.getenv("EXCHANGE_RATE_API_KEY") 

    def _run(self, amount: float, from_currency: str, to_currency: str) -> str:
        url = f"https://v6.exchangerate-api.com/v6/{self.api_key}/latest/{from_currency}"
        response = requests.get(url)
        
        if response.status_code != 200:
            return "Failed to fetch exchange rates."

        data = response.json()
        if "conversion_rates" not in data or to_currency not in data["conversion_rates"]:
            return f"Invalid currency code: {to_currency}"

        rate = data["conversion_rates"][to_currency]
        converted_amount = amount * rate
        return f"{amount} {from_currency} is equivalent to {converted_amount:.2f} {to_currency}."
```

### Creating Agents


```python
from crewai import Agent

currency_analyst = Agent(
    role = "Currency Analyst",
    goal = "Provide real-time currency conversions and financial insights.",
    backstory=(
        "You are a finance expert with deep knowledge of global exchange rates."
        "You help users with currency conversion and financial decision-making."
    ),
    tools = [CurrencyConverterTool()],  # Attach our custom tool
    verbose = True
)
```

### Creating Tasks


```python
from crewai import Task

currency_conversion_task = Task(
    description = (
        "Convert {amount} {from_currency} to {to_currency} "
        "using real-time exchange rates."
        "Provide the equivalent amount and "
        "explain any relevant financial context."
    ),
    expected_output = ("A detailed response including the "
                     "converted amount and financial insights."),
    agent = currency_analyst
)
```

### KickOff Crew


```python
from crewai import Crew, Process

crew = Crew(
    agents = [currency_analyst],
    tasks = [currency_conversion_task],
    process = Process.sequential
)

response = crew.kickoff(
    inputs = {
        "amount": 100, 
        "from_currency": "USD",
        "to_currency": "EUR"
    }
)
```

    [1m[95m# Agent:[00m [1m[92mCurrency Analyst[00m
    [95m## Task:[00m [92mConvert 100 USD to EUR using real-time exchange rates.Provide the equivalent amount and explain any relevant financial context.[00m
    
    
    [1m[95m# Agent:[00m [1m[92mCurrency Analyst[00m
    [95m## Thought:[00m [92mThought: I need to convert 100 USD to EUR using the Currency Converter Tool to get the real-time exchange rate and converted amount.[00m
    [95m## Using tool:[00m [92mCurrency Converter Tool[00m
    [95m## Tool Input:[00m [92m
    "{\"amount\": 100, \"from_currency\": \"USD\", \"to_currency\": \"EUR\"}"[00m
    [95m## Tool Output:[00m [92m
    100.0 USD is equivalent to 87.99 EUR.[00m
    
    
    [1m[95m# Agent:[00m [1m[92mCurrency Analyst[00m
    [95m## Final Answer:[00m [92m
    100 USD is equivalent to 87.99 EUR. The exchange rate reflects current market conditions, influenced by factors such as interest rates, economic stability, and geopolitical events. Currency values fluctuate continuously due to trading activities, and understanding these dynamics can aid in making informed financial decisions.[00m
    
    



```python
from IPython.display import Markdown
Markdown(response.raw)
```




100 USD is equivalent to 87.99 EUR. The exchange rate reflects current market conditions, influenced by factors such as interest rates, economic stability, and geopolitical events. Currency values fluctuate continuously due to trading activities, and understanding these dynamics can aid in making informed financial decisions.


