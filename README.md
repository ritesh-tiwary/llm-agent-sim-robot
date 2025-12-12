![Python](https://img.shields.io/badge/Python-3.12%2B-blue?logo=python) ![ROS2](https://img.shields.io/badge/ROS2-Humble%20%2B-blue?logo=ros) ![NVIDIA%20Omniverse](https://img.shields.io/badge/NVIDIA-Omniverse-green?logo=nvidia) ![LLM](https://img.shields.io/badge/LLM-Experimental-orange?logo=ai) ![LangChain](https://img.shields.io/badge/LangChain-0.0.1-lightgrey?logo=langchain) ![OpenAI](https://img.shields.io/badge/OpenAI-API-black?logo=openai) ![License](https://img.shields.io/badge/License-MIT-green.svg) [![GitHub issues](https://img.shields.io/github/issues/ritesh-tiwary/llm-agent-sim-robot)](https://github.com/ritesh-tiwary/llm-agent-sim-robot/issues) [![GitHub stars](https://img.shields.io/github/stars/ritesh-tiwary/llm-agent-sim-robot)](https://github.com/ritesh-tiwary/llm-agent-sim-robot/stargazers)

# LLM Agent Controlling a Simulated Robot

A minimal example showing how a **Large Language Model (LLM)** can control a **simulated robot** using high‑level natural‑language instructions. The LLM outputs structured JSON actions like `move_forward`, `turn`, or `navigate`, which the agent executes inside a PyBullet simulation.

---

## 🚀 Features
- PyBullet-based lightweight robot simulation
- LLM Agent that plans actions based on observation
- JSON‑based structured action interface
- Minimal architecture for Digital Twins / Robotics AI demos
- Docker support + GitHub Actions CI
- Extendable to ROS2 / Omniverse

---

## 📁 Project Structure
```css

llm-agent-sim-robot/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── Dockerfile
├── docker-compose.yml
├── .github/
│   └── workflows/ci.yml
├── sim/
│   ├── __init__.py
│   └── sim_env.py
├── agent/
│   ├── __init__.py
│   ├── llm_agent.py
│   └── main.py
├── adapters/
│   ├── ros2_adapter.py
│   └── omniverse_adapter.md
└── examples/
└── sample_session.md

````

---

## 🧠 How It Works
1. `SimEnv` provides the simulation with a robot & a small object
2. The agent formats the observation into a prompt
3. The LLM returns a JSON array of actions
4. Each action is executed inside the simulation step-by-step

---

## ▶️ Quickstart (Local)
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
export OPENAI_API_KEY="sk-..."
python agent/main.py --episodes 3
````

---

## 🐳 Quickstart (Docker)

```bash
docker build -t llm-agent-sim-robot .
docker run --rm -e OPENAI_API_KEY="$OPENAI_API_KEY" llm-agent-sim-robot
```

---

## 🧩 Example Code Snippets

### `sim/sim_env.py`

```python
# minimal PyBullet simulation environment
import pybullet as p
import pybullet_data

p.connect(p.GUI)
p.setAdditionalSearchPath(pybullet_data.getDataPath())
plane = p.loadURDF("plane.urdf")
robot = p.loadURDF("r2d2.urdf")
while True:
    p.stepSimulation()
```


### `agent/llm_agent.py`

```python
# LLM agent converting observations into structured JSON actions

def llm_agent(observation: str) -> dict:
    """
    Convert natural-language robot observations into JSON-based actions.
    """
    # example placeholder logic
    return {
        "action": "move_forward",
        "distance": 0.5,
        "confidence": 0.92,
        "reason": "Based on obstacle-free path detected"
    }
```


### `agent/main.py`

```python
# entrypoint: agent ↔ simulation loop

def run():
    pass
```

---

## 🔄 GitHub Actions (CI)

```yaml
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Install deps
        run: |
          pip install -r requirements.txt
      - name: Lint
        run: flake8 .
      - name: Test
        run: pytest -q
```

---

## 📝 License

**[MIT License](LICENSE)**

---

## 📌 Next Steps

* Add unit tests for LLM agent & simulation
* Replace OpenAI with other LLM providers (Anthropic, Groq, etc.)
* Add GUI visualizations or trajectory plots
* Expand to ROS2 or NVIDIA Omniverse

---

If you want, I can generate:

* A ZIP export of this repo
* A ready-to-paste **GitHub repo creation script**
* A more advanced README with diagrams, badges, or GIF animations
