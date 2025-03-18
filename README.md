# README: Conversational Agents for Weather and Computation Assistance

## Setup Instructions

### Prerequisites
- Python 3.7+
- An OpenAI-compatible API
- Weather API credentials (WeatherAPI)
- Required dependencies: `openai`, `requests`, `python-dotenv`

### Installation Steps
1. Clone this repository or download the `conversational_agent.py` file.
2. Install the required dependencies using pip:
   ```sh
   pip install openai requests python-dotenv
   ```
3. Set up your `.env` file with the following keys:
   ```sh
   API_KEY=your_openai_api_key
   BASE_URL=your_openai_api_base_url
   LLM_MODEL=your_model_name
   WEATHER_API_KEY=your_weatherapi_key
   ```
4. Run the script interactively:
   ```sh
   python conversational_agent.py
   ```
5. Choose between running a single agent or performing a comparative evaluation.

## Implementation Steps

### 1. Basic Agent
- The assistant responds to user queries about the weather using the WeatherAPI.
- Uses predefined functions for current weather and forecast retrieval.
- No advanced reasoning is applied; it simply retrieves and presents the requested information.

### 2. Chain of Thought (CoT) Agent
- Enhances reasoning by structuring responses step-by-step.
- Breaks down complex queries into smaller tasks.
- Incorporates a calculator tool for additional numerical computations.

### 3. ReAct (Reasoning + Acting) Agent
- Implements a structured process:
  1. Thought: Determines the required actions.
  2. Action: Uses available tools (weather, calculator, web search) to gather data.
  3. Observation: Reviews the results and adjusts the approach if needed.
  4. Final Answer: Provides a reasoned response.
- Simulates web searches for broader knowledge retrieval.

## Example Conversations

### Basic Agent
```
User: What's the weather like in Paris today?

Weather Assistant: The current weather in Paris is mostly sunny with a temperature of 11.1°C (or 52.0°F). The humidity is 40% and there's a gentle wind blowing at 18.4 km/h.     
```

### Chain of Thought Agent
```
User: Compare the temperatures of New York and London and tell me the difference.

Weather Assistant: To find the temperature difference between New York and London, we need to subtract the temperature of one city from the temperature of the other.

First, let's get the temperatures:
- New York temperature: 35.1°F
- London temperature: 50.0°F

Now, let's calculate the difference:
50.0°F (London) - 35.1°F (New York) = 14.9°F

So, the temperature difference between New York and London is 14.9°F.
```

### ReAct Agent
```
User: What's the probability of rain in Tokyo tomorrow, and how does it compare to New York?

Weather Assistant: Thought: I need to find the probability of rain in Tokyo and New York tomorrow, and then compare the two values.
Action: Use get_weather_forecast for Tokyo and New York.
Observation: The probability of rain in Tokyo tomorrow is 97%, while in New York it is 0%.
Thought: Now I can compare the two probabilities.
Action: None needed, as I have both probabilities.
Observation: Tokyo has a significantly higher chance of rain compared to New York.
Final Answer: The probability of rain in Tokyo tomorrow is 97%, which is much higher than in New York, where the chance of rain is 0%.
```

## Analysis: Effect of Reasoning Strategies on Response Quality

| Agent Type     | Strengths | Limitations |
|---------------|-----------|-------------|
| **Basic** | Fast responses, simple structure | Limited reasoning, cannot handle multi-step queries |
| **Chain of Thought** | Step-by-step reasoning, better for numerical problems | Still lacks adaptability to dynamic queries |
| **ReAct** | Dynamically chooses tools, provides explicit reasoning | More complex implementation, requires more API calls |

- The **Basic Agent** is useful for direct weather queries but lacks depth.
- The **CoT Agent** improves performance in multi-step reasoning but does not adapt dynamically.
- The **ReAct Agent** provides the best responses in complex scenarios by integrating reasoning and tool usage.
