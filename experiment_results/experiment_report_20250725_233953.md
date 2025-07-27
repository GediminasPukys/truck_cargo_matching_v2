# Truck-Cargo Matching Optimization Experiment Report

Generated on: 2025-07-25 23:39:53

## Default Parameters Results

- **Total Trucks**: 54
- **Total Cargo**: 229
- **Successful Assignments**: 41
- **Assignment Rate**: 1.0%
- **Total Cost**: €7382.12
- **Total Distance**: 5254.39 km
- **Total Waiting Time**: 212.77 hours
- **Average Cost per Assignment**: €180.05

### Rejection Analysis

- **Total Rejected**: 4273
- **Rejected by Distance**: 4185
- **Rejected by Waiting Time**: 27
- **Rejected by Time Window**: 61

## Parameter Sensitivity Analysis

### Distance Limit Impact

| Max Distance (km) | Assignments | Total Cost (€) | Assignment Rate (%) |
|-------------------|-------------|----------------|--------------------|
| 200 | 36 | 5900.25 | 0.8 |
| 250 | 41 | 7382.12 | 1.0 |
| 300 | 52 | 10891.89 | 1.2 |
| 350 | 54 | 11664.98 | 1.3 |

### Waiting Time Limit Impact

| Max Waiting (hours) | Assignments | Total Cost (€) | Assignment Rate (%) |
|---------------------|-------------|----------------|--------------------|
| 12 | 38 | 6503.04 | 0.9 |
| 24 | 41 | 7382.12 | 1.0 |
| 36 | 42 | 7721.73 | 1.0 |
| 48 | 42 | 7721.73 | 1.0 |

## Route Planning with Rest Stops

| Truck ID | Deliveries | Total Distance (km) | Rest Stops |
|----------|------------|---------------------|------------|
| 1 | 2 | 321.2 | 0 |
| 2 | 5 | 729.7 | 1 |
| 3 | 8 | 978.3 | 2 |
| 4 | 6 | 1014.8 | 2 |
| 5 | 8 | 814.4 | 2 |

## Key Findings

1. The optimization algorithm successfully assigns cargo to trucks while minimizing total costs
2. Distance constraints have a significant impact on assignment success rate
3. Waiting time flexibility can improve assignment rates but increases costs
4. Route planning with EU rest regulations is integrated and functional
