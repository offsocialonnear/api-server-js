# NEAR Social API Server JS

A JavaScript-based API server for the NEAR Social platform, providing data access and indexing capabilities for social data stored on the NEAR blockchain.

## Features

- RESTful API for accessing social data
- Real-time data synchronization from NEAR blockchain receipts
- Data indexing capabilities
- Block height and timestamp tracking
- Caching for improved performance

## Prerequisites

- Node.js (v14 or higher)
- Yarn package manager
- PostgreSQL database
- NEAR blockchain indexer data

## Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   yarn install
   ```

## Configuration

Create a `.env` file in the project root with the following variables:

```env
DATABASE_URL=postgresql://username:password@localhost:5432/database_name
PORT=3000
```

## Database Schema

The server expects a PostgreSQL database with a `receipts` table containing:
- `block_height` (integer)
- `outcome_index` (integer)
- `account_id` (text)
- `method_name` (text)
- `status` (text)
- `args` (text/JSON)
- `block_timestamp` (text)

## Usage

### Development Mode
```bash
yarn dev
```

### Production Mode
```bash
./run.sh
```

The `run.sh` script is the recommended way to run the server in production as it:
- Automatically creates log directories
- Logs output to dated files in the `logs` directory
- Maintains organized logs by date

### Direct Execution
```bash
yarn start
```

## API Endpoints

### GET /get
Retrieve social data by keys.

Parameters:
- `keys` (array|string): Data keys to retrieve
- `blockHeight` (number, optional): Specific block height to query

### POST /get
Retrieve social data by keys (POST version for complex queries).

Body:
- `keys` (array): Data keys to retrieve
- `blockHeight` (number, optional): Specific block height to query
- `options` (object, optional): Query options

### GET /keys
Retrieve keys from social data.

Parameters:
- `keys` (array|string): Key patterns to match
- `blockHeight` (number, optional): Specific block height to query

### POST /keys
Retrieve keys from social data (POST version for complex queries).

Body:
- `keys` (array): Key patterns to match
- `blockHeight` (number, optional): Specific block height to query
- `options` (object, optional): Query options

### GET /index
Query indexed data.

Parameters:
- `key` (object): Index key to query
- `action` (string): Action to filter by
- `accountId` (string, optional): Account ID to filter by

### POST /index
Query indexed data (POST version for complex queries).

Body:
- `key` (object): Index key to query
- `action` (string): Action to filter by
- `accountId` (string, optional): Account ID to filter by
- `options` (object, optional): Query options

### GET /time
Get timestamp for a block height.

Parameters:
- `blockHeight` (number): Block height to query

### POST /time
Get timestamp for a block height (POST version).

Body:
- `blockHeight` (number): Block height to query

## Scripts

- `yarn start`: Start the server
- `yarn dev`: Start the server in development mode with auto-reload
- `yarn snapshot`: Generate a data snapshot from the NEAR blockchain

## License

This project is licensed under the MIT License - see the LICENSE file for details.