# ScrapeGraphAI_LLama3
Run the best python-based scraper with your personal LLAMA3 to scrape anything off the web for free (no tokens).
For that we have to install Ollama, llama3, and few python dependencies. 

## Download Ollama from ollama/download 
Ollama is an open-source software platform designed to simplify running and managing various LLMs locally on your own computer. It acts as a bridge between you and the powerful capabilities of LLMs.

Llama3 is a specific family of LLM models developed by Meta AI. It represents the next generation of their open-source LLMs, offering significant advancements in capabilities and performance compared to previous models.

### Install Ollama from the exe file downloaded, and check if it is running in taskbar. 
now run in terminal - ```ollama run llama3``` to download llama3 (4.7 GB)

and then, ```ollama pull llama3``` and ```ollama pull nomic-embed-text```

## Now we move to VSCODE. Launch VSCODE and create a new folder for the python project.
In terminal run these to setup a virtual environment, ```python venv env``` and ```env\Scripts\activate```

In case of permission error, open a terminal/powershell in admin mode, and run this ```Set-ExecutionPolicy -ExecutionPolicy Unrestricted```

Now try : ```env\Scripts\activate```

## Now copy paste the requirement text from here onto your folder (you can download as well), and run ```pip install requirement.txt``` to install dependencies of the scraper.

After this, in the VSCODE terminal : ```playwright install``` 

Next, we write the scraper code in app.py 

```from scrapegraphai.graphs import SmartScraperGraph

import nest_asyncio

nest_asyncio.apply()

  

# Configuration dictionary for the graph

graph_config = {

    "llm": {

        "model": "ollama/llama3",

        "temperature": 0,

        "format": "json",  # Ollama needs the format to be specified explicitly

        "base_url": "http://localhost:11434",  # set Ollama URL

    },

    "embeddings": {

        "model": "ollama/nomic-embed-text",

        "base_url": "http://localhost:11434",  # set Ollama URL

    },

    "verbose": True,

}

  

smart_scraper_graph = SmartScraperGraph(

    prompt="List me the projects with descriptions", // You can change this 

    # also accepts a string with the already downloaded HTML code

    source="https://perinim.github.io/projects",  // you can change this to other URLs 

    config=graph_config

)

  
  
  

result = smart_scraper_graph.run()

print(result)

  

# Prettify the result and display the JSON

import json

  

output = json.dumps(result, indent=2)  # Convert result to JSON format with indentation

  

line_list = output.split("\n")  # Split the JSON string into lines

  

# Print each line of the JSON separately

for line in line_list:

    print(line)
```

This is the o/p : 

```--- Executing Fetch Node ---
--- Executing Parse Node ---
--- Executing RAG Node ---
--- (updated chunks metadata) ---
--- (tokens compressed and vector stored) ---
--- Executing GenerateAnswer Node ---
Processing chunks: 100%|████████████████████████████████████████████| 1/1 [00:00<00:00, 999.83it/s] 
{'projects': [{'name': 'Rotary Pendulum RL', 'description': 'Open Source project aimed at controlling a real life rotary pendulum using RL algorithms'}, {'name': 'DQN Implementation from scratch', 'description': 'Developed a Deep Q-Network algorithm to train a simple and double pendulum'}, {'name': 'Multi Agents HAED', 'description': 'University project which focuses on simulating a multi-agent system to perform environment mapping. Agents, equipped with sensors, explore and record their surroundings, considering uncertainties in their readings.'}, {'name': 'Wireless ESC for Modular Drones', 'description': 'Modular drone architecture proposal and proof of concept. The project received maximum grade.'}]}
{
  "projects": [
    {
      "name": "Rotary Pendulum RL",
      "description": "Open Source project aimed at controlling a real life rotary pendulum using RL algorithms"
    },
    {
      "name": "DQN Implementation from scratch",
      "description": "Developed a Deep Q-Network algorithm to train a simple and double pendulum"   
    },
    {
      "name": "Multi Agents HAED",
      "description": "University project which focuses on simulating a multi-agent system to perform environment mapping. Agents, equipped with sensors, explore and record their surroundings, considering uncertainties in their readings."
    },
    {
      "name": "Wireless ESC for Modular Drones",
      "description": "Modular drone architecture proposal and proof of concept. The project received maximum grade."
    }
  ]
}
```
