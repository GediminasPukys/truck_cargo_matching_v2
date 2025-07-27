# Truck-Cargo Matching Optimization System

Automated system for optimizing truck-cargo assignments using linear optimization algorithms.

## Overview

This application optimizes the assignment of trucks to cargo loads by:
- Minimizing total costs (distance + waiting time)
- Respecting time windows for pickup and delivery
- Matching truck and cargo types
- Implementing EU driving regulations for route planning

## Features

- **Smart Assignment Algorithm**: Uses Hungarian algorithm for optimal truck-cargo matching
- **Cost Optimization**: Balances distance and waiting time costs
- **Route Planning**: Multi-delivery routes with automatic rest stop calculation
- **Interactive Visualization**: Real-time map visualization with Folium
- **Configurable Parameters**: Adjustable distance limits, waiting times, and speeds

## Installation

1. Clone the repository:
```bash
git clone https://github.com/your-repo/truck_cargo_matching_v2.git
cd truck_cargo_matching_v2
```

2. Create virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Running the Application

```bash
streamlit run streamlit_app.py
```

The application will open in your browser at `http://localhost:8501`

### Data Format

#### Trucks CSV
Required columns:
- `truck_id` - Unique identifier
- `truck type` - Type (General/Frozen/Liquid)
- `Address (drop off)` - Drop-off location
- `Latitude (dropoff)`, `Longitude (dropoff)` - Coordinates
- `Timestamp (dropoff)` - When truck becomes available
- `avg moving speed, km/h` - Average speed
- `price per km, Eur` - Cost per kilometer
- `waiting time price per h, EUR` - Waiting cost per hour

#### Cargo CSV
Required columns:
- `Origin` - Pickup location name
- `Origin_Latitude`, `Origin_Longitude` - Pickup coordinates
- `Available_From`, `Available_To` - Time window for pickup
- `Delivery_Location` - Delivery location name
- `Delivery_Latitude`, `Delivery_Longitude` - Delivery coordinates
- `Cargo_Type` - Type (General/Frozen/Liquid)

### Configuration

Key parameters can be adjusted in the sidebar:
- **Max Distance**: Maximum allowed distance for assignments (default: 250 km)
- **Max Waiting Time**: Maximum waiting time at pickup (default: 24 hours)
- **Standard Speed**: Vehicle speed for calculations (default: 73 km/h)

## Project Structure

```
truck_cargo_matching_v2/
├── streamlit_app.py          # Main application
├── utils/
│   ├── time_cost_calculator.py   # Optimization algorithms
│   ├── route_planner.py          # Route planning with rest stops
│   ├── visualization.py          # Map visualization
│   └── data_loader.py           # Data validation and loading
├── data_sample/             # Sample data for testing
│   ├── trucks.csv
│   └── cargos.csv
├── docs/                    # Documentation
├── requirements.txt         # Python dependencies
└── README.md               # This file
```

## Algorithm Details

The system uses the Hungarian algorithm (scipy.optimize.linear_sum_assignment) to find the optimal assignment that minimizes total cost. The cost matrix considers:
- Distance between truck location and cargo pickup
- Waiting time if truck arrives before cargo availability
- Type matching constraints

## Performance

- Handles up to 1000 vehicles efficiently
- Computation time: < 5 seconds for typical datasets
- Memory usage: < 100 MB

## Documentation

- [EKSPERIMENTO_ATASKAITA.md](EKSPERIMENTO_ATASKAITA.md) - Experiment report (Lithuanian)
- [VEIKLOS_REZULTATAI.md](VEIKLOS_REZULTATAI.md) - Activity results (Lithuanian)

## License

This project is part of InoBranda business feasibility study.

## Contact

For questions and support, please contact the InoBranda project team.
