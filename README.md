```markdown
# Kingdom Combat API

A simple Flask-based backend for simulating kingdom battles with structures that have attack and defense scores. Players can create kingdoms, add structures, and battle against each other in real-time.

## Features
- Create players and their kingdoms.
- Add structures (with attack and defense scores) to a kingdom.
- Attack between two players, comparing their attack and defense scores to determine the winner.

## Tech Stack
- **Backend Framework**: Flask (Python)
- **API Type**: RESTful
- **Language**: Python
- **Package Management**: pip

## Installation

Follow these steps to set up the project locally.

### 1. Clone the repository
Clone this project to your local machine.

```bash
git clone https://github.com/yourusername/kingdom-combat-api.git
cd kingdom-combat-api
```

### 2. Create and activate a virtual environment (optional but recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install dependencies
Install the required dependencies from the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 4. Run the Flask app
Run the Flask application with the following command:

```bash
python app.py
```

By default, the server will start on `http://127.0.0.1:5000/`.

## API Endpoints

### 1. **Create a Player**
Create a new player by providing a name.

**Endpoint**: `POST /create_player`

**Request Body**:
```json
{
  "name": "PlayerName"
}
```

**Response**:
- Success:
  ```json
  { "message": "Player created successfully" }
  ```
- Error (Player already exists):
  ```json
  { "error": "Player already exists" }
  ```

### 2. **Add a Structure to a Player's Kingdom**
Add a structure (with defense and attack values) to a player's kingdom.

**Endpoint**: `POST /add_structure`

**Request Body**:
```json
{
  "player_name": "PlayerName",
  "structure_name": "StructureName",
  "defense": 20,
  "attack": 10
}
```

**Response**:
- Success:
  ```json
  { "message": "Structure added successfully" }
  ```
- Error (Player does not exist):
  ```json
  { "error": "Player does not exist" }
  ```

### 3. **Attack Another Player**
Initiate an attack between two players. The player with the higher attack score wins.

**Endpoint**: `POST /attack`

**Request Body**:
```json
{
  "attacker_name": "Player1",
  "defender_name": "Player2"
}
```

**Response**:
- Success (if attacker wins):
  ```json
  { "message": "Player1 wins!" }
  ```
- Success (if defender defends successfully):
  ```json
  { "message": "Player2 defends successfully!" }
  ```
- Error (One or both players do not exist):
  ```json
  { "error": "One or both players do not exist" }
  ```

## Testing the API

### 1. **Postman Collection**
You can import the provided [Postman Collection](kingdom_api.postman_collection.json) to quickly test the API endpoints.

### 2. **Python Script for Testing**
You can also use the provided Python script to test the API.

```python
import requests

base_url = "http://127.0.0.1:5000"

# Create Players
requests.post(f"{base_url}/create_player", json={"name": "Player1"})
requests.post(f"{base_url}/create_player", json={"name": "Player2"})

# Add Structures
requests.post(f"{base_url}/add_structure", json={
    "player_name": "Player1",
    "structure_name": "Barracks",
    "defense": 10,
    "attack": 25
})

requests.post(f"{base_url}/add_structure", json={
    "player_name": "Player2",
    "structure_name": "Wall",
    "defense": 30,
    "attack": 5
})

# Attack
response = requests.post(f"{base_url}/attack", json={
    "attacker_name": "Player1",
    "defender_name": "Player2"
})

print("Attack result:", response.json())
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing
If you'd like to contribute to this project, feel free to fork the repository, create a branch, and submit a pull request. Please ensure your code follows PEP 8 guidelines.

---

Enjoy your kingdom-building and combat game!
```

---

### To Do:
- Replace the link to the GitHub repo with the actual one if you plan to host the project.
- Optionally include the **LICENSE** file if you intend to make it open-source.
