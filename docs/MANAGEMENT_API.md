# Management API Reference

The LumeAi Platform exposes a management API under `/v0/management`.
This API is used by the `lumeai-management-center` frontend.

**Base URL**: `http://<host>:<port>/v0/management`

## Authentication

Requests to the management API must include the `management-key` (configured in `config.yaml` as `secret-key`) or a logged-in session token (if enabled).

Headers:
- `Authorization: Bearer <management-key>`

## Endpoints

### Configuration

#### GET `/config`
Returns the current full configuration.

#### PUT `/debug`
Enable/Disable debug mode.
- Payload: `{"value": true/false}`

#### PUT `/proxy-url`
Set an upstream proxy URL (e.g. for accessing OpenAI via a VPN).
- Payload: `{"value": "http://user:pass@proxy:port"}`

#### DELETE `/proxy-url`
Remove the upstream proxy configuration.

### System Settings

#### PUT `/request-retry`
Set the number of retries for failed requests.

#### PUT `/quota-exceeded/switch-project`
Enable/Disable switching projects when quota is exceeded.

#### PUT `/usage-statistics-enabled`
Enable/Disable usage tracking.

#### PUT `/ws-auth`
Enable/Disable WebSocket authentication.

### Logs

#### GET `/logs`
Retrieve server logs. Supports filtering and pagination.

#### PUT `/logging-to-file`
Enable/Disable saving logs to the `logs/` directory.

#### PUT `/logs-max-total-size-mb`
Set the maximum size for log files.

### OpenAI Compatibility

(Further endpoints exist for managing OpenAI-compatible providers, keys, and model mappings. Refer to `providers.ts` in the frontend source code for more details).
