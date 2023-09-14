# Cognite Data Fusion Unit Catalog

This repository stores a comprehensive unit catalog for Cognite Data Fusion (CDF) with a focus on standardization, comprehensiveness, and consistency. The catalog is maintained in two primary JSON files:

1. `units.json`: Contains a list of units with their metadata.
2. `unitSystems.json`: Contains various unit systems and their quantities.

## Structure

### units.json

Each item in the `units.json` has the following structure:

```json
{
    "externalId": "string",
    "name": "string",
    "longName": "string",
    "aliasNames": ["string", ...],
    "quantity": "string",
    "conversion": {
        "multiplier": "float",
        "offset": "float"
    },
    "source": "string",
    "qudtReference": "URL"
}
```

- `externalId`: The external identifier for the unit. Its structure follows the pattern `{quantity}:{unit}` (e.g., `temperature:deg_c`), adhering to the **snake_case** convention.
- `name`: The primary symbol/name of the unit (e.g., `°C`).
- `longName`: A descriptive name for the unit (e.g., `degree Celsius`).
- `aliasNames`: An array of possible **aliases** for the unit.
- `quantity`: Specifies the physical quantity the unit measures (e.g., `Temperature`).
- `conversion`: An object containing **multiplier** and **offset** values for converting between units.
- `source`: The primary source of the unit (e.g., `qudt.org`).
- `qudtReference`: A URL reference to the unit definition on QUDT, if available.

### unitSystems.json

Each item in the `unitSystems.json` has the following structure:

```json
{
    "name": "string",
    "quantities": [
        {
            "name": "string",
            "unitExternalId": "string"
        },
        ...
    ]
}
```
- `name`: The name of the unit system (e.g., `default`, `SI`).
- `quantities`: An array containing the physical quantities and their associated units in the system.

## Validations and Tests

To ensure the integrity of the catalog, the following tests are conducted:

1. **Syntax Check**: Every unit item in `units.json` must have the specified keys.
2. **Unique IDs**: All unit `externalIds` in `units.json` must be unique.
3. **Reference Validation**: There should be no references to non-existent unit `externalIds` in `unitSystems.json`.
4. **Default Quantities**: All quantities must be present in the `unitSystems.json` for the default quantity.
5. **Consistent References**: All quantity references in `unitSystems.json` must exist in `units.json`.

## Contribution

To maintain the consistency and quality of the unit catalog, please ensure any contributions adhere to the established structure and guidelines. Before submitting any additions or modifications, ensure that all tests pass.