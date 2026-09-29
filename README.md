# Autonomous AI Racing Game (NEAT & Pygame)

An **AI-driven 2D self-driving car simulation** built using Python, Pygame, and the **NEAT** (NeuroEvolution of Augmenting Topologies) framework. The project applies genetic algorithms and artificial neural networks to teach a fleet of virtual cars how to navigate a custom race track autonomously without hitting walls.

This project is heavily inspired by the YouTuber *Cheesy AI* and optimized/commented by *NeuralNine (Florian Dedov)*.

---

## 🚀 How It Works

1. **Sensors (Radars):** Each car emits 5 distinct radar lines (from -90 to +90 degrees) to calculate the distance to the track's white boundaries (`BORDER_COLOR`).
2. **Neural Network Control:** Every frame, the car feeds these 5 distance values into its NEAT neural network. The network processes the data and outputs one of four actions:
   * **Turn Left**
   * **Turn Right**
   * **Slow Down**
   * **Speed Up**
3. **Fitness & Evolution:** Cars earn a reward (fitness score) based on how far and how fast they drive. If a car hits the white boundary, it crashes and dies.
4. **Generational Learning:** Once all cars crash or the time limit expires, NEAT selects the top-performing cars, applies mutations to their neural structures, and breeds a new, smarter generation.

---

## 🛠️ Project Structure

* `main.py` - The main Python script containing the game engine, car physics, radar geometry, and the NEAT execution loop.
* `config.txt` - The configuration file for the NEAT-Python library specifying population size, mutation rates, and neural network constraints.
* `map.png` - The custom race track image file. The window dynamically auto-scales to this file's dimensions.
* `car.png` - The sprite image asset used for the vehicles.

---

## 📦 Prerequisites & Installation

Make sure you have **Python 3.8+** installed on your computer. 

1. **Clone or download** this repository to your local machine.
2. Open your terminal or command prompt inside the project folder.
3. **Install the required packages** by running:

```bash
pip install pygame neat-python
```

---

## 🎮 Running the Simulation

Execute the main script to start the training process:

```bash
python main.py
```

### Important Configuration Note
If you face a `RuntimeError: Missing required configuration item`, ensure that the `[NEAT]` section inside your `config.txt` file includes this line:
```ini
[NEAT]
no_fitness_termination = False
```

---

## ⚙️ Key Customization Variables

You can easily tweak the training inside `newcar.py`:
* **Car Size:** Adjust `CAR_SIZE_X` and `CAR_SIZE_Y` constants to scale your car sprite.
* **Turn Angle & Speed Steps:** Modify the degree variables or the `speed += 2` parameters inside the `run_simulation` logic loop to change car maneuverability.
* **Generation Timeout:** The script is set to stop a generation after roughly 20 seconds (`counter == 30 * 40`). You can increase this value to allow longer trials.
